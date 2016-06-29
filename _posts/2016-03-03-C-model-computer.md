---
layout: post
title:  C语言计算机模型
mathjax: false
comments: true
excerpt: "C语言计算机模型"
date:   2016-03-03 +0800
categories: 计算机组成原理
---

> C语言是一种高级语言，对于使用者来说是一种抽象和虚拟。使用者原则上只需关心其语法结构和和平台接口。下面将对C语言（虚拟）计算机从各个层面进行思辨性的讨论。


### C语言虚拟的目的

虚拟有不同的目的。虚拟机和沙盒更多的目的是隔离环境－－里面的操作基本不会对外面的环境造成影响。

C语言可以通过接口访问底层的硬件，可以嵌入汇编代码（内联汇编），也经常用来写操作系统。可见C语言的虚拟和抽象主要是为了“好用”。

### C语言虚拟的层次

虚拟有着不同的层次。ISA将软件完全隔离在它之上；操作系统几乎完全控制着硬件资源；虚拟机软件将虚拟机内部和外部的环境隔离开来。这些是完全的虚拟。

C语言有所不同。C语言可以跑在操作系统之上，也可以用来写操作系统（当年主要的目的即是编写UNIX系统，从而增强可移植性）。它的显然的一个目的是对汇编语言进行虚拟。

例如一个循环，在x86汇编下面是：

{% highlight ASSEMBLY %}
XOR EAX, EAX
START_LOOP:
CMP EAX, N
JBE END_LOOP
; <YOUR CODE>
INC EAX
JMP START_LOOP
END_LOOP:
{% endhighlight %}

C语言的语法结构将其抽象为：

{% highlight C %}
for(int i = 0; i < N; i++)
{
  // Your Code
}
{% endhighlight %}

C语言的语法结构还有助于算法和数据结构的实现。其内存分配和数组掩盖了很多寻址操作，比如下面是一个典型的并查集的实现（初始化）：

{% highlight C %}
#define COUNT 1000
// funtion body skipped
int findset[COUNT];
for(int i = 0; i < COUNT; i++) findset[i] = i;
{% endhighlight %}

在接近汇编的层次会变成这样：

{% highlight C %}
// ebp points to findset
int i = 0;
start_loop:;
if(i >= 1000) goto end_loop;
*(ebp + i) = i;
i = i + 1;
goto start_loop;
end_loop:;
{% endhighlight %}

显然上面一种结构更适合描述算法和数据结构。所以目前大家的算法和数据结构课程没有使用汇编语言表述。

当然，随着时代发展，C语言很多时候不是用于写底层接口，而是上层硬件

当然这些接口背后是非常复杂的操作系统接口。
比如如果你试图看看printf是如何工作的，你可以一直跟踪到用户层的底层：

{% highlight gdb %}
(gdb) b write
Function "write" not defined.
Make breakpoint pending on future shared library load? (y or [n]) y
Breakpoint 1 (write) pending.
(gdb) r
Starting program: /home/zsy/hello

Breakpoint 1, write () at ../sysdeps/unix/syscall-template.S:81
81	../sysdeps/unix/syscall-template.S: No such file or directory.
(gdb) bt
#0  write () at ../sysdeps/unix/syscall-template.S:81
#1  0x00007ffff7aa7473 in _IO_new_file_write (f=0x7ffff7dd72a0 <_IO_2_1_stdout_>, data=0x7ffff7ff5000, n=12) at fileops.c:1253
#2  0x00007ffff7aa6b33 in new_do_write (fp=0x7ffff7dd72a0 <_IO_2_1_stdout_>, data=0x7ffff7ff5000 "Hello world!", to_do=12) at fileops.c:530
#3  0x00007ffff7aa82a5 in _IO_new_do_write (fp=<optimized out>, data=<optimized out>, to_do=12) at fileops.c:503
#4  0x00007ffff7aa991e in _IO_flush_all_lockp (do_lock=do_lock@entry=0) at genops.c:848
#5  0x00007ffff7aa9a7a in _IO_cleanup () at genops.c:1013
#6  0x00007ffff7a6ab7b in __run_exit_handlers (status=0, listp=<optimized out>, run_list_atexit=run_list_atexit@entry=true) at exit.c:95
#7  0x00007ffff7a6ac15 in __GI_exit (status=<optimized out>) at exit.c:104
#8  0x00007ffff7a54b4c in __libc_start_main (main=0x400506 <main>, argc=1, argv=0x7fffffffeaf8, init=<optimized out>, fini=<optimized out>,
    rtld_fini=<optimized out>, stack_end=0x7fffffffeae8) at libc-start.c:321
#9  0x0000000000400439 in _start ()
(gdb)
{% endhighlight %}

为了避免此种麻烦，系统和C语言标准库提供了C语言一组API，从而实现对功能的虚拟。

### 为什么要虚拟和抽象?

首先，虚拟是一种包装，很多时候要损失性能。

但是更多时候我们是为了获得新的“自由”。

比如我们常用的printf，它的打印文字到屏幕上面的部分是如此复杂：

{% highlight gdb %}
#0  write () at ../sysdeps/unix/syscall-template.S:81
#1  0x00007ffff7aa7473 in _IO_new_file_write (f=0x7ffff7dd72a0 <_IO_2_1_stdout_>, data=0x7ffff7ff5000, n=12) at fileops.c:1253
#2  0x00007ffff7aa6b33 in new_do_write (fp=0x7ffff7dd72a0 <_IO_2_1_stdout_>, data=0x7ffff7ff5000 "Hello world!", to_do=12) at fileops.c:530
#3  0x00007ffff7aa82a5 in _IO_new_do_write (fp=<optimized out>, data=<optimized out>, to_do=12) at fileops.c:503
#4  0x00007ffff7aa991e in _IO_flush_all_lockp (do_lock=do_lock@entry=0) at genops.c:848
#5  0x00007ffff7aa9a7a in _IO_cleanup () at genops.c:1013
{% endhighlight %}

以至于我们宁愿直接调用printf，而不是对它的底层进行优化。底层是显然可以优化的，比如当一个程序监测到它在独占屏幕时，完全可以直接对屏幕设备进行写入，而不必要标准输出文件描述符的帮助，这样绕过操作系统这层，效率肯定会好一点。

然而，我们如此频繁的调用这些功能，并且环境十分复杂，所以最终通过操作系统支持有了所谓“C语言标准库”。在这里通用性和易用性比损失一点点性能更重要。而虚拟和抽象可以做到者一点，所以我们选择如此。

但是虚拟不仅有性能代价的，高级语言还付出了语法代价，例如：

汇编语言语法：

{% highlight asm %}
cmd [op1, op2, ...]
cmd [op1, op2, ...]
cmd [op1, op2, ...]
cmd [op1, op2, ...]
cmd [op1, op2, ...]
cmd [op1, op2, ...]

{% endhighlight %}

C语言语法就可以复杂相当多：

{% highlight C %}
int *(*func(int *f(), char **))...
z = a && b || c - !d | e & f ^ g + ~h * (i = 3)  + (j++) + (++k) %(*p)  / l? (*f)() : (int)(*t->k()), sizeof*ptr;
{% endhighlight %}

再高级的语言有了更加复杂和丰富的语法结构。但是语法结构带来了对算法和数据结构描述的方便性。再高级的语言还带来了对象生命周期管理，序列化，元编程，反射等功能，使得其在应用方面更加得心应手（比如APP／网页很少用C语言写，更不可能是汇编）。

所以，虚拟抽象很像一种“再均衡”，用以满足上层要求。

### 反思：虚拟 & 工程思维？

我们注意到，“虚拟”和“抽象”很多地方是类似的，然而“虚拟”似乎主要用于计算机领域。

虚拟和抽象非常不同的一点是：虚拟是非常完整的抽象和重构，很多时候保持原来功能的完备性。比如虚拟机软件能够保证一个系统完成它在实体机里面能够完成的所有任务；C语言虚拟机照样可以完成汇编能完成的一切算法，Java，Python，Lisp，Scala，Haskell均是如此。连JavaScript都可以在网页中模拟Linux操作系统，或者编译C语言程序。

抽象是不一样的。抽象往往会丢失一些属性，它试图总结共性而丢弃另外一些东西。

虚拟之所以在计算机领域盛行，是因为我们**希望通用的，硬件结构相同的计算机在各个场合下均高效且便于使用**，这带来的结果就是虚拟：我们不能通过软件改变硬件结构，同时为了适合各个场合我们显然要保证功能的完全性。

虚拟的结果就是：如果某种东西普遍适用且有好处，我们倾向于将它加入硬件系统，比如Cache, 内存分页，保护模式，开机硬件流程，DMA等等。其它则依赖于软件，且一定是各种各样不同的软件，因为不可能有一种软件可以适应所有情况，如果是，就会被加入硬件中来提高总体性能，因为硬件相比软件性能要高得多。软件所做的事情是将它负责的那个功能实现。后来又为了提高软件的效率，协作性和资源分配的平衡性，又引入了操作系统。操作系统的某些需求后来又刺激了硬件的变革（比如保护模式）。

所以，虚拟更多时候是适应它的应用而产生的，这是一种计算思维，或者工程思维。



---

This is an 'open-sourced' page created by Si-Yuan Zhuang. For reference, plz keep it open & free, thanx.

Some pictures may be picked from the Internet. If the origin author would like to claim its authority, plz contact me.

This work is licensed under a [Creative Commons Attribution-NonCommercial 3.0 Unported License](http://creativecommons.org/licenses/by-nc/3.0/).

![Creative Commons Licence](https://i.creativecommons.org/l/by-nc/3.0/88x31.png)

