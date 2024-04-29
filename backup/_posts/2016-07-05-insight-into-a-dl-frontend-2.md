---
layout: post
title:  深入理解 Deep Learning 前端框架 (II)
mathjax: true
comments: true
excerpt: "深入理解 Deep Learning 前端框架 (II)"
date:   2016-07-15 +2200
categories: deep_learning
---

`技术篇` `理论篇`

> 此篇侧重介绍计算图（Computational Graph）

## 概述

计算图是一种计算模型，可以用于表示符号计算。

在传统的数值计算中，很多表达式的推导和计算流程无关，因而不需要特定的数据结构对计算流程进行表示。而符号计算中，很多流程（比如求梯度）都需要对计算流程或者表达式进行分析。这个时候就需要对计算流程进行表示，一般采用(有向)计算图或者(有向)计算网络(Computational Graph)。

这篇blog给出了计算图的一种表示和处理方式，其他形式的原理大致相同。

## 用计算图表示计算流程

在Deep Learning中，计算图的主要运算对象是张量(Tensor)。一个诸如`D=Tanh(W*x+C)`的运算可以表示为以下的一个图：

![](/static/insight-into-a-dl-frontend/Computational_Graph1.svg)

我们发现，诸如D之类的东西逻辑上并不是一个自由的变量，而是依赖于前面的结果的，这类东西称为`Placeholder`（图中标记为圈），而变量称为`Variable`。显然依赖于外界输入的量是Placeholder。如果`D=Tanh(W*x+C)`中x是源于输入的，那么可以重新表示为：

![](/static/insight-into-a-dl-frontend/Computational_Graph2.svg)

(可以发现它们的特征是Variable和用于输入的Placeholder在图中的入度为0，流程中的Placeholder入度为1。值得注意的是，在先前的图中我们忽略了一些Placeholder，因为它们没有“名字”)

连接各种量的是各种各样的运算，在图中称为`Operation node`(在图中标记为六角形)

## 计算图求值过程

Placeholder正如其名，它是可以被Fill值的(比如在输入时)。

计算图可以按照以下的逻辑求值：

0. 如果是Variable或者Filled的Placeholder, 直接返回值。
1. 如果是未Filled的Placeholder，Fill其Parent的值并返回。不能满足则出错。
2. 如果是Operation node, 返回它的输入经过Operation node运算后的值。

可见这是一个递归求值过程，Placeholder保持一些临时状态，保持Filled可以避免重复运算。计算图可以从任何位置求值的必要条件是所有用于输入的Placeholder（即入度为0的）均已经填充相应的值。

## 计算图更新过程

计算图中的Variable和Placeholder（尤其是那种入度为0的，即用于输入的）可以使用不同的方式改变其值。

Variable的更新可以来源于Placeholder，即对一个Placeholder求值，并将值赋给Variable(图中虚线)。这往往构成了一次迭代。

Placeholder一般使用外部输入作为更新，作为其Fill的值。

更新Variable／Placeholder后，会递推地将其后所有的Placeholder内容清空（使无效），以保证逻辑的正确性。显然更新入度为1的Placeholder会导致下一次求值时在此Placeholder处“短路”（因为按照求值过程求到此处时Placeholder为Filled，直接返回而不继续回溯）。因此有些实现不允许非输入的Placeholder更新。

以下是一个带更新的计算图（这实际上是一个真实的训练模型）：
    
![](/static/insight-into-a-dl-frontend/Computational_Graph3.svg)

## 用计算图表示函数

函数和一般的计算流程不同，它显式地要求指出相应地输入输出。输入输出是外界的东西，比如numpy array，Placeholder的存在为我们提供了一种进行函数抽象的方法。

我们可以指定一些Placeholder为Input（相当于函数的参数列表）, 另外一些为Output（相当于函数的返回值）。每次调用函数的过程就是先用一些输入更新相应的Input，然后对Output进行求值，并更新要求更新的Variable（更新Variable可以视为更新函数的内部变量）。

一个训练模型可以表示为一个函数：

![](/static/insight-into-a-dl-frontend/Computational_Graph4.svg)

但是需要注意的是，这样的函数输入输出均为numpy array这些具体的数值，而不是Placeholder这样的符号。所以一个函数就是一个封闭的计算图，而不是可以级连的图的一部分。不过函数仅仅是规定了强制赋值和求值，因而将其变为图的一部分是非常容易的－－实际上我们倒着做这件事，即将一个不封闭的图变成函数从而封闭其功能，这往往是实际应用中实现的最后一步。

## 图生成过程

图的逻辑可以直接来源于代码。

比如a*b这些语句实际上是运算符重载，比如a.\__mul__(b)。这些函数将它的操作数作为Operation node的输入，返回一个Placeholder。如此一系列操作可以构成一个图。

需要注意的是，由于图生成过程是依赖代码的执行流程的，所以下面的语句不能如愿实现效果：
{% highlight python %}
c = a * b if mul_op else a + b
{% endhighlight %}
如果执行这句时mul_op为true, 那么在计算图中就生成了c = a * b, 而和之后的mul_op变化无关；反之亦然。
如果需要在计算图中实现“分支”，需要专门的操作。在Keras中是keras.backend.switch，在TensorFlow后端中它封装了这样的操作：
{% highlight python %}
def switch(condition, then_expression, else_expression):
    '''Switches between two operations depending on a scalar value (int or bool).
    Note that both `then_expression` and `else_expression`
    should be symbolic tensors of the *same shape*.

    # Arguments
        condition: scalar tensor.
        then_expression: TensorFlow operation.
        else_expression: TensorFlow operation.
    '''
    x_shape = copy.copy(then_expression.get_shape())
    x = tf.python.control_flow_ops.cond(tf.cast(condition, 'bool'),
                                        lambda: then_expression,
                                        lambda: else_expression)
    x.set_shape(x_shape)
    return x
{% endhighlight %}



## 流模型

对计算图的求值更新可以视作一个流式计算的过程，这也是`TensorFlow`中`Flow`的来源。下图是一个具体的例子：

![](/static/insight-into-a-dl-frontend/tensors_flowing.gif)

## Keras对计算图的实现

Keras实现了对计算图中操作的封装，实现了variable, placeholder, function。

下面的代码是对TensorFlow的封装。可以看到Keras在传入参数的时候进行了若干检查
以保证使用的时候在Keras这一层就可以发现问题，这是和后端独立的要求。
（在后端发生问题使用者就很难找出错误的原因）。

TensorFlow使用Session来表示当前的执行上下文（包括计算图，将计算分发到不同设备等）。对于输入使用feeddict实现，更新变量用tf.assign实现赋值操作。

{% highlight python %}

def variable(value, dtype=_FLOATX, name=None):
    '''Instantiates a tensor.

    # Arguments
        value: numpy array, initial value of the tensor.
        dtype: tensor type.
        name: optional name string for the tensor.

    # Returns
        Tensor variable instance.
    '''
    v = tf.Variable(np.asarray(value, dtype=dtype), name=name)
    if tf.get_default_graph() is get_session().graph:
        try:
            get_session().run(v.initializer)
        except tf.errors.InvalidArgumentError:
            warnings.warn('Could not automatically initialize variable, '
                          'make sure you do it manually (e.g. via '
                          '`tf.initialize_all_variables()`).')
    else:
        warnings.warn('The default TensorFlow graph is not the graph '
                      'associated with the TensorFlow session currently '
                      'registered with Keras, and as such Keras '
                      'was not able to automatically initialize a variable. '
                      'You should consider registering the proper session '
                      'with Keras via `K.set_session(sess)`.')
    return v


def placeholder(shape=None, ndim=None, dtype=_FLOATX, name=None):
    '''Instantiates a placeholder.

    # Arguments
        shape: shape of the placeholder
            (integer tuple, may include None entries).
        ndim: number of axes of the tensor.
            At least one of {`shape`, `ndim`} must be specified.
            If both are specified, `shape` is used.
        dtype: placeholder type.
        name: optional name string for the placeholder.

    # Returns
        Placeholder tensor instance.
    '''
    if not shape:
        if ndim:
            shape = tuple([None for _ in range(ndim)])
    x = tf.placeholder(dtype, shape=shape, name=name)
    x._keras_shape = shape
    x._uses_learning_phase = False
    return x

class Function(object):

    def __init__(self, inputs, outputs, updates=[]):
        assert type(inputs) in {list, tuple}, 'Input to a TensorFlow backend function should be a list or tuple.'
        assert type(outputs) in {list, tuple}, 'Output to a TensorFlow backend function should be a list or tuple.'
        assert type(updates) in {list, tuple}, 'Updates in a TensorFlow backend function should be a list or tuple.'
        self.inputs = list(inputs)
        self.outputs = list(outputs)
        with tf.control_dependencies(self.outputs):
            self.updates = [tf.assign(p, new_p) for (p, new_p) in updates]

    def __call__(self, inputs):
        assert type(inputs) in {list, tuple}
        names = [v.name for v in self.inputs]
        feed_dict = dict(zip(names, inputs))
        session = get_session()
        updated = session.run(self.outputs + self.updates, feed_dict=feed_dict)
        return updated[:len(self.outputs)]


def function(inputs, outputs, updates=[], **kwargs):
    '''Instantiates a Keras function.

    # Arguments
        inputs: list of placeholder/variable tensors.
        outputs: list of output tensors.
        updates: list of update tuples (old_tensor, new_tensor).
    '''
    if len(kwargs) > 0:
        msg = [
            "Expected no kwargs, you passed %s" % len(kwargs),
            "kwargs passed to function are ignored with Tensorflow backend"
        ]
        warnings.warn('\n'.join(msg))
    return Function(inputs, outputs, updates=updates)

{% endhighlight %}


> 当然，计算图本身的结构还意味着一些更加高级的功能，例如求某些量的梯度。此方面有著名的反向传播算法（back-propagation）。这个在下篇说明。


---

This is an 'open-sourced' page created by Si-Yuan Zhuang. For reference, plz keep it open & free, thanx.

Some pictures may be picked from the Internet. If the origin author would like to claim its authority, plz contact me.

This work is licensed under a [Creative Commons Attribution-NonCommercial 3.0 Unported License](http://creativecommons.org/licenses/by-nc/3.0/).

![Creative Commons Licence](https://i.creativecommons.org/l/by-nc/3.0/88x31.png)

