---
layout: post
title:  操作系统演示视频
mathjax: false
comments: true
excerpt: "操作系统演示视频"
date:   2016-03-03 +0800
categories: Operation_System
---

`技术篇` 

##### [关于标签](/about/tags)

### 简介

**这是个操作系统相关视频教程，目的主要是教学，旨在揭示程序从API到内核入口的整个机制。**

#### **[> 视频地址](http://player.youku.com/player.php/sid/XMTQ4ODA1MjE3Ng==/v.swf)**

内容基本上是原创的，网上很难找到相似内容。

**涉及的具体内容有：**

* 汇编语言（略）
* 基本Linux操作（略）
* Linux编辑文件（VIM，略）
* Linux编译程序（带调试符号，详）
* Linux反汇编（objdump，详）
* Linux调试（GDB，主要）
* Windows盲调试（Ollydbg，主要）
* 对调试后得到的猜想的验证（略）

**另外间接提到的内容：**

* 调试思路
* 调用堆栈
* 内存分页
* Linux下用GDB控制程序的行为（重定向stderr/stdout到当前屏幕）
* Windows动态运行库
* 类Unix系统和Windows系统设计思路差异


## 背景知识

### 保护模式

为了保护内核环境，现代操作系统在硬件的协助下建立一个叫`保护模式`(Protect Mode)的机制。

在保护模式下，Intel系列芯片提供了`Ring0-Ring3`这4个运行模式。

Ring0权限最高，拥有完全的硬件控制权。Ring3最低，一切设备／中断相关操作都会引发错误。

一般操作系统只使用Ring0和Ring3两个运行级别。内核环境使用Ring0，其它使均用Ring3，因此Ring0称为“内核态”，而“Ring3”称为“用户态”。

在保护模式下，用户如何调用操作系统功能呢？

试想，如果用户程序触发一个错误，这个信息会被谁捕捉？－－显然是内核环境，因为用户态无法对错误进行更深入的处理。用户态程序触发错误时，会产生当前环境参量的快照（包括错误原因），然后强制切换到内核态的指定位置。这时候操作系统便可以处理这个程序，比如发生段错误时，这个程序基本上死定了，会被操作系统终止。但是如果程序触发特定错误，比如执行int 0x2e，操作系统发现是这种错误时，会视为程序进行了系统调用。这时候程序当前环境参量（某些特殊的寄存器，以及堆栈）表示了请求的上下文（context），然后在内核态中完成相应操作。这样用户态就通过触发错误实现了系统调用。这种机制也称为“陷阱门”。

但是显然通过错误来调用是低效的。所以当前Intel指令集中增加了专用指令sysenter/syscall，专门用来实现该类系统调用。

所以现在计算机的模型是:

**[User Mode]-[sysenter/syscall]-[Kernel Mode]-[Ring0-Only ISA]-[Hardware]**

操作系统内核一般跑在Ring0上，但是组成操作系统的绝大部分却是运行在Ring3上。

### 从操作系统API到内核

操作系统的API主要存放于一些动态链接库中。

目前绝大多数程序并没有对操作系统API对应的运行库进行静态编译－－因为这个会使得程序很大且夸平台可能遇到问题。

每个平台下都会有一些核心的动态运行库。这些运行库最终会使用到系统调用。

一般来说，动态运行库的调用系统中断的最后或者倒数第二个函数，和内核中的函数是对应的。

---

This is an 'open-sourced' page created by Si-Yuan Zhuang. For reference, plz keep it open & free, thanx.

Some pictures may be picked from the Internet. If the origin author would like to claim its authority, plz contact me.

This work is licensed under a [Creative Commons Attribution-NonCommercial 3.0 Unported License](http://creativecommons.org/licenses/by-nc/3.0/).

![Creative Commons Licence](https://i.creativecommons.org/l/by-nc/3.0/88x31.png)

