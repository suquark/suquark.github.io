---
layout: post
title:  深入理解 Deep Learning 前端框架 (I)
mathjax: true
comments: true
excerpt: "深入理解 Deep Learning 前端框架 (I)"
date:   2016-07-04 +1900
categories: deep_learning
---

`技术篇` `理论篇`

> `Deep Learning`（即深度学习，DL） 作为机器学习的一个分支，自06年以来飞速发展。与机器学习的发展史相比，DL仍然非常年轻，但是在诸多领域（计算机视觉，语音，增强学习，甚至计算机艺术） DL对于其他模型已经到了碾压的地步，并且目前仍然没有明确看到它的能力的极限。DL 同样非常与众不同的一点是它需要前所未有的计算能力，高性能计算领域的发展（NVIDIA GPU，FPGA，Infiniband，专用芯片，分布式计算框架）恰如其分的给了DL前所未有的发展动力，成为其坚实的基础。而后一些支持并行计算的软件模型在其上建立起来，比如 Theano, Torch(库部分), TensorFlow, CNTK等等，为DL提供了研究环境。近来为了满足快速实现以方便研究，一些更加高层的框架基于先前的模型建立起来，如果说这些高层框架是前端，那么它基于的部分就是后端。这一系列Blog针对前端框架Keras进行分析，通过代码说明DL的基本原理和实现方法，以期望加深读者的理解。

本篇侧重介绍张量基础和后端接口。

<!--content-->

## 概述


* #### 这篇blog目的何在?
目的不仅仅在于对Keras进行分析，更重要的在于通过这些分析，了解DL的原理和具体实现。


* #### Keras是什么?
Keras是一个建立在Theano或者TensorFlow之上的深度学习库，但是实现上和它们是脱耦的（前后端分离是也）。它追求最小化，模块化，可拓展性和快速实现（从想法到实现的速度决定了研究效率）。使用Python，同时支持2和3。


* #### 框架层次
其实Torch和TensorFlow也有各自的“前后端”，只是抽象程度可能没有Keras高而已，并且Keras属于晚辈，层次结构上有些地方稍微好于前者。
关于层次结构，熟悉HPC（高性能计算）这一套的人可能非常担心抽象和层次对程序性能的影响。抽象程度越高，就离硬件接口越远，对硬件的控制能力越低，最终带来非常可观的性能损失。同样，抽象程度越低，编程难度越大，实现周期长且易于出现难以察觉的错误。所以这是个两难问题，解决它的办法不是使用一种两边都不讨好的语言（这时候“中庸”反而是一种最差的方案），而是像计算机存储结构一样引入“层次”的概念来掩盖和均衡损失。
![层次示例](/static/insight-into-a-dl-frontend/DL-Arch1.svg)

* #### DL需要哪些数据结构？
DL主要需要 `Tensor`(张量，类似于多维数组) 和 `Computational Graph`（计算图，用于组织模型） 这两个数据结构。前者非常有利于并行，而基于后者可以进行分布式、异步流处理。实际上TensorFlow等框架正致力于这点。下面是TensorFlow的计算流程示意图。
![TensorFlow GIF](/static/insight-into-a-dl-frontend/tensors_flowing.gif)

## 张量基础

张量是对高维数据的一种抽象，在计算机中可以以多维数组为基础构建张量。
描述张量的一个重要指标是shape。比如floatx T\[3]\[7][4] 对应的shape是(3,7,4)。
shape的元素个数称为张量的维数，张量的每一个下标称为一个轴。
维数为0表示一个标量。维数为1是向量，维度为2是矩阵。

一个图像显然可以表示为一个2维张量：
![](/static/insight-into-a-dl-frontend/T2.png)

彩色图像有RGB三个通道，如果希望区分，最好表示为一个3维张量：
![](/static/insight-into-a-dl-frontend/T3.png)


显然张量的各个轴的排列不是唯一的，可以任意改变轴的顺序，使用中保持一致即可：
![](/static/insight-into-a-dl-frontend/T3-2.png)

一个训练集有多个彩色图像，它们构成4维张量：
![](/static/insight-into-a-dl-frontend/T4.png)

而如果训练集分组，就构成了5维张量：
![](/static/insight-into-a-dl-frontend/T5.png)

可以沿着不同轴拼接张量：
![](/static/insight-into-a-dl-frontend/concat.png)

可以沿着不同轴规约张量（求和等）：
![](/static/insight-into-a-dl-frontend/reduce.png)

张量可以有空的维度, 这些维度不影响数据，是可以随意增减的：
![](/static/insight-into-a-dl-frontend/empty_dims.png)

张量可以改变形状（只要不影响内容），
特例是flatten,它把张量变成向量；
batch_flatten保留一个维度，把张量变成矩阵：
![](/static/insight-into-a-dl-frontend/flatten.png)

张量可以沿着某个轴抽取数据重新组合：
![](/static/insight-into-a-dl-frontend/gather.png)

二维及以下的张量显然可以按照矩阵的方式点乘。
高维张量间的乘法操作是对矩阵乘法的拓展。（orz 我为了搞清楚这个又啃了广义相对论的剩饭）

为了便于抽象我们使用指标标记：如果T的shape是(A,B,C)那么标记T为 $T_C^{AB}$

A行B列的矩阵标记为$T_B^A$

矩阵乘法可以表示为指标缩并（可以想象成上下抵消了）: $X_B^AY_C^B=M_C^A$

向量内积有了很漂亮的表示（1可以不写）: $X_BY^B=C$

推广一下可以得到张量的乘法规则：
$$X_{I}^{ABC}Y_{F}^{DEI}=Z_{F}^{ABCDE}$$

具体算法是：$$Z[a,b,c,d,e,f]=\sum_i{X[a,b,c,i]*Y[d,e,i,f]}$$

张量还有更多非常非常丰富的操作，这些操作足以保证张量这种数据结构能够胜任DL的计算。

## 后端接口

后端接口包括了DL所需要加速的核心操作，如果你想要设计相关的平台、专用芯片或者FPGA软核，就应该注意这些。

#### 全局

learning_phase() # 标志训练阶段
epsilon(), set_epsilon(e) # 默认fuzz factor, 用于处理“近似0”，“除以0”，“log 0”等问题
floatx() # 获取默认类型
image_dim_ordering(),set_image_dim_ordering(dim_ordering) # 图像颜色通道和像素点的排布方式
cast_to_floatx(x) # 设置numpy数组为默认类型

#### Activation function(激活函数)

{% highlight python %}
# logical-like ，用于表示概率分布
tanh(x)
sigmoid(x) # 1/(1+exp(-x))
hard_sigmoid(x) # faster sigmoid
softmax(x) # X_i <- exp(X_i)/sum(exp(X[])), sigmoid的延伸

# ReLU-like，线性修正单元
relu(x, alpha=0.0, max_value=None) # 即 min(max(alpha*x,x)),max_value)，(注：alpha<1.0)
softplus(x) # ReLU连续近似
{% endhighlight %}

#### Map 函数(n=>n)

这些操作是逐张量元素的

square(x),abs(x),sqrt(x),exp(x),log(x),round(x),sign(x),pow(x, a),sin(x),cos(x),clip(x, min_value, max_value)


#### Map 函数(2n=>(bool)n)

equal(x, y),not_equal(x, y),maximum(x, y),minimum(x, y)


#### Reduce 函数 (n=>1)

这些操作满足归约性质, keep_dims表示沿着指定的axis归并为1个元素后仍然保留维度（e.g. keep_dims时 sum([1 2 3 4])->[10]而不是10）

{% highlight python %}
max(x, axis=None, keepdims=False)
min(x, axis=None, keepdims=False)
sum(x, axis=None, keepdims=False)
prod(x, axis=None, keepdims=False)
var(x, axis=None, keepdims=False)
std(x, axis=None, keepdims=False)
mean(x, axis=None, keepdims=False)
any(x, axis=None, keepdims=False) # logical OR
all(x, axis=None, keepdims=False) # logical AND
argmax(x, axis=-1) # Returns the index of the maximum value along a tensor axis.
argmin(x, axis=-1) # Returns the index of the minimum value along a tensor axis.
{% endhighlight %}

#### 张量创建

{% highlight python %}
zeros(shape, dtype='float32', name=None)
ones(shape, dtype='float32', name=None)
eye(size, dtype='float32', name=None)
# 这两个“模仿”张量的形状
zeros_like(x, name=None)
ones_like(x, name=None)
variable(value, dtype='float32', name=None) # numpy array -> tensor

# 描述了输入张量的“接口形状”，相当于定义了“张量类型”
placeholder(shape=None, ndim=None, dtype='float32', name=None) 
{% endhighlight %}

#### 张量转换

{% highlight python %}
eval(x),get_value(x),batch_get_value(xs[]) # Tensor -> numpy array
set_value(x, value),batch_set_value(tuples(x,value)[]) # numpy array->Tensor
cast(x, dtype) # Casts a tensor to a different dtype.
{% endhighlight %}

#### 张量属性

{% highlight python %}
int_shape(x) # 返回张量的形状，以int-tuple形式呈现
shape(x) # 返回张量的形状，以符号形式呈现
count_params(x) # 张量元素个数
dtype(x) # 张量数据类型
ndim(x) # 张量的维数（阶数）
{% endhighlight %}

#### 张量运算

{% highlight python %}
# 包括张量间逐元素的 +, -, /, *, +=, -=, *=, /=
transpose(x) # Transpose a matrix
gather(reference, indices) # return reference[indices]

# 对于向量是内积运算，矩阵是标准矩阵乘法，
# 更高维度的是沿着x.shape[-1]和y.shape[-2]这两个轴求积之和
dot(x, y)


# 沿着某个轴展开，里面内容分别进行dot运算（向量化的dot）
batch_dot(x, y, axes=None)

{% endhighlight %}

#### 张量拓扑

{% highlight python %}

# 改变张量的形状为shape。前后两个shape元素个数必须一样，
#   利用这个约束可以放入至多一个-1来自动计算该维度的尺寸
reshape(x, shape) 
flatten(x) # 把张量变成向量，相当于reshape(x, [-1])。是reshape高效具体实现
# 除了第一个维度外，剩余的都flatten作为第一个维度的元素, 最终构成一个矩阵。
#    是reshape高效具体实现
batch_flatten(x) 

permute_dimensions(x, pattern) # 将张量轴按照序号pattern重新排序


concatenate(tensors, axis=-1) # 沿轴拼接张量
# 层叠一个矩阵，形状(samples, dim) -> (samples, n, dim)。
repeat(x, n) 
# 沿轴重叠元素，不改变形状。If x has shape (s1, s2, s3) and axis=1, 
#    the output will have shape (s1, s2 * rep, s3)
#    是concatenate高效具体实现
repeat_elements(x, rep, axis)


# 加入一个空的维度，例如2->[2]; [4,5,6]->[[4,5,6]]或者[[4],[5],[6]]
expand_dims(x, dim=-1) 
# 去掉指定的size为1的轴(意味着没有)，比如 [[0]]->0 。和expand_dims互为逆操作
squeeze(x, axis)


{% endhighlight %}

#### 损失函数

损失函数指出正确和错误结果间的差异

{% highlight python %}
# 这些损失以交叉熵形式为主，在信息学上有信服的解释。后面文章会解释这一点。

categorical_crossentropy(output, target, from_logits=False) # Categorical crossentropy between an output tensor and a target tensor, where the target is a tensor of the same shape as the output.

sparse_categorical_crossentropy(output, target, from_logits=False) # Categorical crossentropy between an output tensor and a target tensor, where the target is an integer tensor.

binary_crossentropy(output, target, from_logits=False)# Binary crossentropy between an output tensor and a target tensor.
{% endhighlight %}

#### 卷积／池化操作

{% highlight python %}
conv2d(x, kernel, strides=(1, 1), border_mode='valid', dim_ordering='th', image_shape=None, filter_shape=None)
pool2d(x, pool_size, strides=(1, 1), border_mode='valid', dim_ordering='th', pool_mode='max')
{% endhighlight %}

#### 控制流

{% highlight python %}
# If condition then_expression else else_expression, 形成计算图中的分支
switch(condition, then_expression, else_expression):

def in_train_phase(x, alt):
    x = switch(_LEARNING_PHASE, x, alt)
    x._uses_learning_phase = True
    return x

def in_test_phase(x, alt):
    x = switch(_LEARNING_PHASE, alt, x)
    x._uses_learning_phase = True
    return x


# 表示一个计算图中的变换
'''Instantiates a Keras function.
inputs: list of placeholder/variable tensors.
outputs: list of output tensors.
updates: list of update tuples (old_tensor, new_tensor).
'''
function(inputs, outputs, updates=[], **kwargs)

# 获取变量相对损失的梯度
gradients(loss, variables)

# 循环网络，在图中相当于一个环
def rnn(step_function, inputs, initial_states,
        go_backwards=False, mask=None, constants=None,
        unroll=False, input_length=None):
    '''Iterates over the time dimension of a tensor.

    # Arguments
        inputs: tensor of temporal data of shape (samples, time, ...)
            (at least 3D).
        step_function:
            Parameters:
                input: tensor with shape (samples, ...) (no time dimension),
                    representing input for the batch of samples at a certain
                    time step.
                states: list of tensors.
            Returns:
                output: tensor with shape (samples, ...) (no time dimension),
                new_states: list of tensors, same length and shapes
                    as 'states'.
        initial_states: tensor with shape (samples, ...) (no time dimension),
            containing the initial values for the states used in
            the step function.
        go_backwards: boolean. If True, do the iteration over
            the time dimension in reverse order.
        mask: binary tensor with shape (samples, time, 1),
            with a zero for every element that is masked.
        constants: a list of constant values passed at each step.
        unroll: with TensorFlow the RNN is always unrolled, but with Theano you
            can use this boolean flag to unroll the RNN.
        input_length: not relevant in the TensorFlow implementation.
            Must be specified if using unrolling with Theano.

    # Returns
        A tuple (last_output, outputs, new_states).

        last_output: the latest output of the rnn, of shape (samples, ...)
        outputs: tensor with shape (samples, time, ...) where each
            entry outputs[s, t] is the output of the step function
            at time t for sample s.
        new_states: list of tensors, latest states returned by
            the step function, of shape (samples, ...).
    '''


{% endhighlight %}




#### 其他

{% highlight python %}
# Sets entries in x to zero at random, while scaling the entire tensor.
dropout(x, level, seed=None) 

# 沿着一个轴除以L2范数，即x/T.sqrt(T.sum(T.square(x), axis=axis, keepdims=True))
l2_normalize(x, axis)

# 调整图像尺寸和格式
# Resizes the images contained in a 4D tensor of shape 
# - [batch, channels, height, width] (for 'th' dim_ordering) 
# - [batch, height, width, channels] (for 'tf' dim_ordering) 
# by a factor of (height_factor, width_factor). 
# Both factors should be positive integers.
resize_images(X, height_factor, width_factor, dim_ordering)


# 沿着一个3D Tensor 中间的轴镶边
temporal_padding(x, padding=1)

# 给图像集(4D Tensor)镶边
spatial_2d_padding(x, padding=(1, 1), dim_ordering='th')


{% endhighlight %}


---

This is an 'open-sourced' page created by Si-Yuan Zhuang. For reference, plz keep it open & free, thanx.

Some pictures may be picked from the Internet. If the origin author would like to claim its authority, plz contact me.

This work is licensed under a [Creative Commons Attribution-NonCommercial 3.0 Unported License](http://creativecommons.org/licenses/by-nc/3.0/).

![Creative Commons Licence](https://i.creativecommons.org/l/by-nc/3.0/88x31.png)

