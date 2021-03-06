---
layout: post
title: "为什么我选择计算机科学2 计算思维"
comments: true
mathjax: true
excerpt: "computer science"
date: 2017-08-15 +0727
categories: lecture
---

我准备交替地发布《我为什么选择计算机科学》系列，强调计算机领域的特性和有意思之处（劝进）；以及《从0开始的计算机科学》，强调一些基础知识（劝退）。

这次我们将讨论一种思维模式：计算思维。

下面的内容以例子为主。当你学完本科阶段学完后，再来看这些例子，就会越发意识到其中的重要性。

## 什么是计算思维

这里引用 Jeannette M. Wing [1] 的观点(选择了一部分内容)。

计算思维建立在对计算这个过程本身的能力和限制的理解之上。

计算思维不仅是计算机学家，也是每个人的基本技能。为了更好地进行阅读、写作、算术我们需要将计算思维作为孩子分析能力的一部分。

恰如出版社促进了3R（阅读、写作、算术这种教育体系）的传播，计算和计算机加速了计算思维的传播。

计算思维透过计算机科学的基本观念解决问题，设计系统，理解人类行为。它包含一些理念上的能够折射出计算机科学纵深的工具。

（如果）需要解决一个特定问题，我们或许会问：它难度有多大？解决它的最好办法是什么？计算机科学基于坚实的理论基础来精确回答这些问题。

计算思维通过规约，嵌入，变换或者模拟的方法，可以将一个难题转变为我们知道如何解决的问题。

计算思维使用抽象和分解来对付一个大的复杂的任务或者设计一个复杂系统。这是一种对事务的分离。计算思维为问题选择合适的表述形式或者为问题各方面的关联建模来使得它易于处理。

这些话或许过于抽象，我们需要看一些具体的例子。


## 分离与接口

所谓分离，是指把大的变成小的，把整体变成部分的思想；而接口，则是把小的和部分的粘成整体的一种结构，往往简单灵活。

其关键思想在于，一个复杂的整体结构，如果能够分为小的部分，那么其逻辑上的复杂性会大大降低，而可控性和统一性会大大增强。

### 策略和机制的分离

这边我们的一个例子是一类非常有代表性的发明：多功能螺丝刀。

一般螺丝刀是个整体，就像下面一样：

![IMAGE](/static/the_computational_thinking/D59484CC74E6FC9A47C551BBEF4A0D06.jpg)

这类螺丝刀一般都是小型的，或者家用的。

在工业使用中，螺丝的种类非常多，而为了提供更大的力矩，螺丝刀体积也很大。如果需要都带上，那么是累人且不现实的。

于是发明了多功能螺丝刀（类似的工具很多）：

![IMAGE](/static/the_computational_thinking/E9703E1492651F70515D40DCEEB17118.jpg)

其本质就是策略和机制的分离：

![IMAGE](/static/the_computational_thinking/1CC3C92502E7E93FDC81D5A74B879026.jpg)

策略和机制的分离在计算机等非常多的领域应用极为广泛：

![IMAGE](/static/the_computational_thinking/0493928DEDAE46BB6CEBE48F543FE27F.jpg)

### 功能的分离

这里的例子是天宫一号

![IMAGE](/static/the_computational_thinking/0C1D020E2109E567C763E87D0AA7138A.jpg)

可以看到，它是由各个功能模块“拼”成的。

另外一个典型的例子是人的内脏器官。自然界进化中，较高等动物统一的特点是出现独立的器官和系统，这绝对不是进化的巧合，而是必然的因素。

还有一个例子在于，现代建筑的分化。一个居民用房，往往会划分为各个房间，而各个房间会起不同的作用；办公楼这些也一样。

为什么？

因为在不分离的时候，各个功能在空间上会形成耦合，相互影响。这是不可避免的事情。如果卧室和厨房放在一起，很难不共享气味；如果返回舱和控制室放到一起，降落的时候很难不受后者影响增加质量；而人体内脏如果发生损坏泄露，也会干扰到其他系统（比如肝脏损坏会导致转氨酶融入血液，较严重的时候色素会引起眼睛的黄斑）

我们可以看一下一个不分离的耦合情况：

![IMAGE](/static/the_computational_thinking/9E6B12FEB07E192AA2EF80272AE2C459.jpg)

虽然只有12个点，但是由于相互影响复杂性极高，难以控制。

而如果我们进行分离，点数是同样的，但是复杂性要小非常多：

![IMAGE](/static/the_computational_thinking/FDA0EA41B436B4CB86FE8E9CB9EE1ABD.jpg)

这样各个封闭的整体（例如器官，或者房间）可以在内部处理和发挥自己的功能，而不用担心对外部的影响。

当然相对独立的功能之间仍然有所谓“接口”相互连接。比如对于房间，接口是各个房间的门或者出口；对于器官是接入的体液系统和神经系统；对于空间站是各个连接结构。接口是一种相对弱的关联，但是将它们形成一个能够正常工作的整体。

这种接口在程序中非常常见，所谓的 `API` 就是 “应用程序接口” 的简称，而接口背后连接的是各个功能的实现，通过调用各个接口，我们提供了各种功能。

这也暗示了在功能的分离中，接口还起到了“指代功能”的作用。比如对于一个场所，有某个房间的钥匙，就等价于有使用其功能的能力；而器官也只在于器官提供的功能，而不管是机械的还是移植的，这也是为什么透析和移植能够救人的原因。

### 层次的分离

在功能分离的基础上，有一种特殊的方式称为层次的分离。这种分离往往基于单向的依赖，或者上下层的依赖。

一个例子是电力系统

![IMAGE](/static/the_computational_thinking/707BA1B13C9F80F6E58EA4D96974BEB6.jpg)

这个时候上面的东西依赖下面的东西。比如获得电能，需要化学能（煤炭，石油）等的支持。

同样的，各个分离的层之间也有类似“接口”的东西。这里的接口一种的意义是被动的，表示“转换”，比如各种原始能源转换为电能，以及电能转到电网；另外一种意义是主动的，表示“暴露”，这种意义下底层向上层（在逻辑上）掩盖了其原来的性质，转而变成另外一种形式，比如电网向城市分配电量时，只是将“电”作为一个数字而已，这个数字就代表了电网服务的对象。

这种东西不一定是实际上的设备，比如计算机组成原理中会提到的计算机组成的层次：

![IMAGE](/static/the_computational_thinking/E843EEA7897D9D45898B1EE58D751851.jpg)

以及非常著名的计算机网络 OSI 7层模型

![IMAGE](/static/the_computational_thinking/AF25163F0DAE53129025F6A2624FEC96.jpg)

分层是为了各个之间的灵活组合，避免复杂的内部变得更加复杂（分层的OSI模型内部都已经如此复杂了）：

![IMAGE](/static/the_computational_thinking/233578AE98CF31F744983D377E6E4CF2.jpg)

### 任务的分离

想象一下如果你遇到一件倒霉的事情，比如说

![IMAGE](/static/the_computational_thinking/0661D7344D2F70268F7A9198B2934634.jpg)

然后你要搬砖，然后发现路不好走没法用机器

![IMAGE](/static/the_computational_thinking/3A003B079A19B8A61A6F492EEFC0C52A.jpg)

然后怎么办？？？

你可能是这样的

![IMAGE](/static/the_computational_thinking/4D156B3DB0F193E4A89C8C4B2E774B90.jpg)

你也可能找到一个这样的帮手

![IMAGE](/static/the_computational_thinking/12FD998CBAD48843BDDA07EC1589C643.jpg)

当然世上或许总会有逆天之人：

![IMAGE](/static/the_computational_thinking/AB42829588556B87361A1797D2168C55.jpg)

(咦？好像看到了不对劲的东西？)

然而如果你是真心想最快地搬砖，那么可能是这样的：

![IMAGE](/static/the_computational_thinking/7562703CA74312520C8C19DEA6FAD760.jpg)

也就是会有一群人一起搬砖。

可以同时执行任务的多个部分的前提在于任务可以良好分离。

如果任务没有很好的分离，那么可能就会是这样的结果：

![IMAGE](/static/the_computational_thinking/4035CD3D660DE15C4A9C9BAFC1C184D8.jpg)

或者这样的结果：

![IMAGE](/static/the_computational_thinking/3F4F37786A43670EE8AF82D8F44349CA.jpg)

说到这个，另外一个有趣的例子是CPU（中央处理器）和GPU（图形处理单元，图形卡，显卡）。

常玩大型游戏的同学应该明白GPU对游戏性能的决定性影响，CPU却很难带动高品质的画面（没有核心显卡的CPU几乎带不动游戏）。但是他们有什么区别吗？

最显著的区别是，CPU可能2核，4核，8核；但是GPU通常可能有上千个核（每一个最小的绿色格子可以认为是一个）：

![IMAGE](/static/the_computational_thinking/BB90AF236FDAEED331023D3AE10B8829.jpg)

GPU拥有如此多个可以独立处理数据的核心的原因在于，游戏等图形学任务是易于分离成若干个小任务的。

考虑一个简单的场景：3D画面的平移旋转缩放（最常见的3D游戏中视角变换）

![IMAGE](/static/the_computational_thinking/C54BEA8431302A49FAFE9EF9C3EAF920.jpg)

如图所示，其中画面中每个点的移动都是独立的（空间的整体性导致的），因而变换每个点的位置可以作为独立的任务。尤其高分辨率画面中有数百万计的点，这就非常适合核数较多的 GPU 做这种事。而另外一些难以划分的日常任务（办公软件等的操作），还是主要靠CPU。

另外 GPU 也非常适合矩阵和高阶张量运算，这也使得 GPU 在最近几年广泛用于深度学习等任务中（比如我用的某台4路TITAN X Pascal机是用来跑神经网络的）。

### 分离复用

你会不会在世界上所有的螺帽上都固定一个扳手？比如像这样：

![IMAGE](/static/the_computational_thinking/36752D0908C409023EE2A55279C8FFC9.jpg)

在大多场合肯定不会。这样很傻。因为扳手是可以“复用”的。它可以用于这个，也可以用于那个。

这个在程序设计中是最基本的一种思路。写程序不同于盖房子：建筑通常有很多相同的部分形成，比如瓷砖和混凝土块；而一个好的程序则通常含有尽可能少的相同的部分。这在结构化程序设计中就会提到（比如C语言的学习中）

以下是个比较大小的例子。基于著名的未解数学问题 [考拉兹猜想 (Collatz conjecture)](https://en.wikipedia.org/wiki/Collatz_conjecture)。它又称为奇偶归一猜想、3n＋1猜想、冰雹猜想、角谷猜想、哈塞猜想、乌拉姆猜想或叙拉古猜想，是指对于每一个正整数，如果它是奇数，则对它乘3再加1，如果它是偶数，则对它除以2，如此循环，最终都能够得到1。

下面的图片中的树显示了各种各样数归结到1的过程。

![IMAGE](/static/the_computational_thinking/01A51770657B6912BB319D9114C7BD25.jpg)

我们称一个数归结到1经历的迭代次数为一个数的Collatz序数。

现在假设有 a, b 两个数，尝试得到对应 Collatz 序数更大的那个数。

一种解决方案是：

{% highlight c %}
int collatz_max(int a, int b) {
    int n1 = 0;
    int n2 = 0;
    while (a > 1) {
        a = (a & 1) ? 3 * a + 1 : a >> 1;
        n1++;
    }
    while (b > 1) {
        b = (b & 1) ? 3 * b + 1 : b >> 1;
        n2++;
    }
    return n1 > n2 ? a : b;
}
{% endhighlight %}

上面的方法是没有错的，但是从复用角度来说是尴尬的。就好像每个螺帽都配一个扳手一样。我们可以考虑复用计算 collatz 序数的代码，将其变成一个函数：

{% highlight c %}

int eval_collatz(int k) {
    int n;
    for (n = 0; k > 1; n++) k = (k & 1) ? 3 * k + 1 : k >> 1;
    return n;
}

int collatz_max(int a, int b) {
    return eval_collatz(a) > eval_collatz(b) ? a : b;
}

{% endhighlight %}

这样一来我们就实现了复用，并且逻辑更加清楚：`eval_collatz` 计算 collatz 序数，而 `collatz_max` 比较大小并返回对应 collatz 序数更大的那个数。

如果这时候需求突然改了，要求返回小的那个，或者要求返回序数的差，也只用改动 `collatz_max`，而不需要小心操作以免波及 `eval_collatz` 的代码。

更近一步，如果已经有了 `eval_collatz` 这个“扳手”，你可以直接在 `collatz_max` 里面使用它，这也是多人项目合作的基础。尤其是一个稍复杂的程序，里面可能有成百上千个函数，如果不复用而是把一个功能重复很多次，复杂程度会急剧上升，并且逻辑性难以控制。

下面就是一个例子（因为代码总是自上而下一个方向写的，所以这里用串代替代码）：

![IMAGE](/static/the_computational_thinking/91A92376911EECF99CF171F5B6B4CFD1.jpg)

注：如果你是C语言初学者，可能更习惯这样的写法：

{% highlight c %}

int eval_collatz(int k) {
    int n = 0;
    while (k > 1) {
        if (k % 2 == 1) {
            k = 3 * k + 1
        } else {
            k = k / 2;
        }
        n = n + 1;
    }
    return n;
}

int collatz_max(int a, int b) {
    if (eval_collatz(a) > eval_collatz(b)) {
        return a;
    } else {
        return b;
    }
}

{% endhighlight %}

这两种写法是等价的。你学习完C语言后应该能适应上面的写法。

### 问题的分离

有时候将问题划分为多个部分求解可能有奇效。这部分我不准备细讲，详情参考 [分治算法](https://en.wikipedia.org/wiki/Divide_and_conquer_algorithm)。它是快速排序、快速傅立叶变换等划时代的算法的重要设计思想，这些算法在解决现实问题中起到了无法估量的成效。

## 局域性原理（广义）

所谓局域性原理，是指的一种时间、空间或者分布上的集中性特征。这是现实中常常会有的情况。之所以称为原理，是因为它不是一种定律，但是却在实际中非常稳定地出现。它告诉了我们 “数学上无解的，现实中总是有解” 的道理。

举一个虚构的例子。

![IMAGE](/static/the_computational_thinking/C951A26BDA3DE3988059DA9EB081159C.jpg)

假设大厅有4扇贵重的门，两侧是楼梯。每天人很多，过一段时间门可能坏掉，维修费用高昂。一个有效的应对方案是加固门，但是如果加固所有的门，也会带来极大的开销。

但是，事实上发现通过两侧门的人数大大多于中间的。于是实际中的解决方案是只加固两侧的门。

![IMAGE](/static/the_computational_thinking/F67708ABD496E230B762B927894F75B4.jpg)

可能之后经过分析，发现原因可能是两侧更靠近楼梯，大家愿意走短点，所以通过两侧门人数更多。但是有可能在另外一个地方，由于另外一些内在原因，人们的行动又呈现另外的分布。出现不同分布的原因可能各种各样，并不服从单一的数学定律，难以预先预测，但是大多数都导致了不平均的分布，而利用这种分布我们可以达到目的。

### 时空局域性

一个司空见惯的例子是，你带着书包上学。但是你想过为什么带书包就可以，而不是每次需要搬家呢？

原因是，在上学期间，你主要只会在学校活动，需要的大多数资源也集中在书包内。你一般不会需要家里的花瓶，厨房，电视。。。

只要有 “距离” 和 “演化” 概念的系统中，几乎都会出现在某个时间段内频繁在某个地点活动的现象。其根本原因在于由于距离的约束，为了规避距离对时间（进而对效率）的浪费，我们选择在同一个地方布置特定的资源。这塑造了我们社会的一切：各种工厂，学校，机构等社会单位；以及省、市等行政区划分；以及语言、文化、种族。如果任何人从家到学校不需要消耗任何时间，那么就没有理由设立这个实体机构（实际上一个例子是网上学校，这种情形下就不需要有实体的机构，也不需要带书包）。

时空局域性是为了效率本身产生的一种现象，因为只有在时空上是局域的，才能最大地发挥效能，但是如果把它作为一种原理来看，那么就可以用来解决实际问题。

这在计算机中有着非常多的应用。计算机体系中有件很蛋疼的事情：（在同样稳定的前提下）容量和速度是矛盾的（容量又大速度又快这种免费午餐不太可能出现）。比如机械硬盘现在几个TB的很常见，但是很慢；固态硬盘现在同等价格的容量也就 256 GB 左右，但是速度很快；内存要更快，但是价格适中的也就 8GB 左右；CPU 中的 Cache 非常快，但是一般价格的处理器中的cache容量几十KB封顶了；CPU中的所谓“寄存器”的元件几乎是所有东西里面最快的（每秒可以存取数十亿次），但是容量要按照字节计算。

然后现在你希望能够有最快的速度，同时有最大的容量，这个表面看上去是痴人说梦。但是局域性原理让这件事情变得可行。计算机中的局域性是因为，绝大多数程序在运行的过程中，几乎总是会在一定时间内访问物理上临近的数据。比如下面的循环(对数组a的元素求和)：

{% highlight c %}

int sum(int a[], int n) {
    int s = 0;
    for (int i = 0; i < n; i++) {
        s += a[i];
    }
    return s;
}

{% endhighlight %}

首先程序执行本身就是局域的：一个程序总会运行一段时间才结束。由于循环的关系，执行的代码是局域的，总是在for里面转圈；同时，由于累加的原因，s 的数值会被反复的更新；由于顺序访问的原因，a的内容的访问也是随着循环慢慢往前的。其无意中就有了大量的局域性。

我们来看看我们怎么让这个程序变得如此之快的：

1. 我们无法将硬盘的所有数据加载到内存里面，但是执行程序是局域的，所以我们可以将要执行的程序从硬盘读取放到内存当中，内存是可以存下程序的二进制代码和产生的活跃数据的（不活跃使用的数据可能会被放到硬盘里面特定的位置，称为“虚拟内存”）。
2. 我们无法把程序的所有代码放到CPU的cache中，但是由于循环部分的代码就那么一点，于是我们把这部分循环的代码放到cache里面；同时我们知道对数组a的访问是顺序的，所以可以预先把将要使用的部分也从内存整体移动（而不是单个移动，但是一样快）到cache中；
3. 代码和数组无法放入到寄存器中，但是变量s和变量i却可以，于是它们被分配到寄存器中。

这样一来在每个阶段，我们都使用了最快的硬件来完成任务，而将数据从慢速的存储器读取到快速的存储器中往往就一两次操作，相比那些局域的执行了非常多次的操作而言其性能开销可以忽略。

这些操作是由操作系统以及计算机硬件，以及编译器自动完成的。它完成的方式是通过某些统计和预先设定的预测，来选择“局域”的内容。有的时候硬件本身不能良好预测，就需要人工优化，时空局域性原理是人工优化的重要手段。

另外一个重要的优化发生在3D游戏中。同时渲染大型游戏中的所有画面内容是一般计算机难以接受的。一个常见的手段是只渲染画面中较近的且在视野中的部分，而远处的部分大多偷工减料（或者换成低廉的贴图），只有等用户靠近再渲染细节，因为大部分游戏中用户视角位置的移动是局域的，不会频繁地出现在没有良好渲染的地方。

### 性能局域性

整体性能往往取决于较小部分，这些部分被称为“瓶颈”。

一个著名的例子是CISC和RISC指令集。CPU执行的一个操作单位称为一个“指令”。由于早期编程比较困难，为了方便，Intel等CPU提供了大量的各种各样的指令，称为复杂指令集（CISC）。但是随后人们发现，在如此众多的指令中，常用的仅仅不到20%，但是却占据了超过80%的性能开销。于是RISC（精简指令集）思想诞生了，RISC大大减少了指令的数量，但是对这些指令进行了高度的优化并且提高了稳定性，同时功耗很低；而CISC中有的一些指令被RISC使用简单指令的组合替代，虽然性能差一些，但是因为使用频率少不影响整体。现在仍然有大量的基于RISC的芯片广泛用于低功耗、嵌入式以及航天航空。

当然Intel也没有认输。Intel采用了“虚拟化”的策略，将CISC指令转化为RISC微码然后再执行，这样既保证了原来指令集的兼容性，同时性能上也有了提高。

另外常见的现象是程序“热点”，也就是程序中往往20%的代码造成了超过80%的性能开销（被称为2/8定律）。所以需要针对热点优化，而不是把整个程序优化一通，这样是低效且不划算的。优化会增加程序的复杂性，并损失一定的逻辑性，所以很多工程实现上强调“不要过早优化”，而是应该在工程稳定后进行热点分析，尽可能少地改动代码。

## 虚拟化

所谓虚拟，相对于真实。真实不一定是指“现实”，而是相对虚拟而言的真实。

虚拟掩盖和扭曲了原来的真实，转而以另外一种视角呈现给我们。但是，这种虚拟的视角恰恰能够帮助我们更好地认知和控制我们的事实。

### 软件定义世界（software defined world）

这里我们探讨计算机对生活中的实物和事务的虚拟化。

这个例子来自 [为什么你招聘不到程序员，以及软件如何定义现实世界](http://chuansong.me/n/2071378)。它从停车场信息化角度谈论了软件和对世界的虚拟化。

当我们用一套停车场管理系统，替代了停车场管理员（那个老大爷）之后，整件事情改变了什么？它并不仅仅是节约了一个老大爷的人力成本这么简单，仅仅节约人力成本的价值并不大，因为基层体力劳动的人力成本是相当有限的，节约20个老大爷的工资，也未必能比得上一个程序员的工资支出。

![IMAGE](/static/the_computational_thinking/92E0C39E695789B5709238D29358C2C0.jpg)

比节约一个人的人力成本更重要的是，我们用软件来规范了停车场的行为，即所谓“定义”。在使用软件之前，停车场管理员是有很大权利的，很多人都知道，给停车场管理员塞一包烟，他可能就会少收你20块钱停车费。甚至很多停车场管理员会直接把停车费塞到自己口袋里面，如果你没要停车发票的话。停车场的运营是没办法监督这种行为，要监督，就需要付出巨大的人力，甚至冒很大风险。有了软件系统之后，一切都不一样了。不再需要去监督这种往自己口袋里面塞钱的行为了，只要软件没有能被他们找到的漏洞，一切都变成了非常规范的行为。开车来的车主进入停车场的时候取卡，系统拍下车牌照，出停车场的时候自动计时收费，付钱之后停车场出口才打开，车才能离开。这个过程可以完全没有人力参与，就算是保留那个停车场老大爷的职位来做应急工作，他的行为也是严格被软件规范的。不交钱，停车场出口不打开，车就没法离开停车场，这是一条被明确定义了的基本规则，除非暴力去破坏停车场设施，否则，一切都是被软件管理的，人改变不了什么。从此，整个过程中不会再有钱的损耗，停车场运营方会获得更多收益。这些收益中的一部分，就变成了软件公司的利润，软件公司利润的一部分，变成了程序员工资。

这就是软件企业为何有巨大盈利，程序员工资为什么这么高的原因。仅从这个例子看，软件没有创造新的价值，但是在若干传统行业中，软件夺回了一部分人本来不应该拿到的钱，把这些钱重新变成了利润，程序员分享了这部分利润。在这个停车场的例子中，按道理说，停车场管理员的收入只应该是一份工资，不包括偷偷塞到口袋里面的停车费，但是如果没有软件，这种行为是没法阻止的，一定会有很大一笔钱流到不应该获得它们的人手里。另外一方面看，在车主这边，他们的行为也被定义了。过去很多人是愿意接受10块钱买一包烟，省20块钱停车费这种设定的。但在软件管理之下，这种利益交换没机会发生了。在这个停车场的案例中，参与业务的两方行为都被软件重新规范和定义了。
整个过程可以这样看：在软件企业的帮助下，现实世界的资金流向被重新分配了。这就是“软件定义现实世界”。软件重新定义了社会规则，定义了人的行为。当然，目前软件还只是体现了业务人员的意愿，在这个阶段，更确切的说法是：软件帮助人们重新定义社会规则。

这只是个开始。我们站的高一点看这个已经被软件接管了的停车场。你会发现，关于它的细节都被隐藏了，你只知道它存在着接口（Interface）。所谓接口，就是对资源的一种抽象，我们知道它提供什么，比如在这里例子中，可能是停车场有多少空车位，已经停有多少车，每天有多少收益，停车场的位置在哪…等等，具体的细节，被装进了一个黑箱子里面，我们不再关心它。比如，一个软件管理的停车场还有没有看车老大爷，这就算细节，在这种视角下，我们不再关心这个人是否存在，也不关心他在做什么，因为已经用软件定义好了他的行为，这时候我们只关心提供结果的接口即可。

在软件世界中，知道了接口，就可以使用这一份资源。从此，我们把这个停车场可以看作软件世界里存在的一个单元（Unit），刚才说了，它的现实状况已经被装进黑箱子屏蔽掉了。如果你只有一个这样的单元，它只能用来规范基本行为，但如果你在相邻街道再有一个这样的“停车场单元”，这时候就能开始有一些新的变化了。比如，停车场单元A已经几乎停满了，但停车场单元B还空着一半车位，这时候就可以通过软件来调整资源，让车主尽量往停车场B停。具体手段有很多，比如通过智能手机发送一条消息，告诉正在开来的车主，停车场A要排队10分钟，停车场B排队1分钟就可进入。自然可以分流一部分人到停车场B。甚至是把停车场B的停车价格降价10%，吸引更多人前往。这些实时的，根据资源剩余情况的动态配置，利用传统手段是不可能做到的。一方面是传统手段没法快速反馈信息，另外一方面，传统方式的审批决策流程过长，要降价总要有个负责人批准一下吧？从而让实时的动态调整变得不可能。但在一个被软件定义的世界里面，是可以做到的。在这种模式下，如果我们再屏蔽掉具体的引导办法（降价，排队时常通知之类），甚至可以把A和B两个停车单元合并成一个看，即，在软件层面上，我们有了一个更大的停车场单元。

再继续下去，如果有更多的资源具有了接口，他们之间还可以发生什么交互？比如，两个停车场旁边有两个规模和品质相似的餐馆A和餐馆B，它们也具有了接口，软件世界里面，我们抽象出餐馆单元A和B，知道它们的座位有多少空余，知道今天厨房有什么材料，知道价格…那么，停车单元A报告自己已经满了的时候，这时候餐馆B是不是愿意暂时降价10%来吸引更多客源？如果餐馆B通过降价，成功把自己空余的资源卖掉了，他是否愿意分享一部分利润给停车场，以及分享一部分利润给帮助进行资源配置的软件运营方？

这些都是会在未来发生的事情。越来越多的现实世界资源通过一个接口，接入软件世界，成为一个抽象的单元，它们会直接发生相互的作用，这就是我们多年所说的“智能化”。所有的这一切，最终都需要软件实现。把一个现实资源抽象成接口这件事，在软件行业称之为“虚拟化”，一个60年代软件行业就使用的概念。通常这个词被用于云计算行业，云计算产业在真正的物理计算机上虚拟出了计算机、路由器、内存…把这些资源弹性分配给需要的用户使用。但实际上，现实世界的一切都是可以通过这种方式被虚拟化的。这就是未来被软件定义的现实世界。对于这样的世界，如果找一个更容易理解的例子，最适合的是游戏。未来的一切都像即时战略游戏所表现的那样，如果你玩过星际争霸，大概会记得拿鼠标点一下，派出一个SCV去采矿，用鼠标点一下工厂，坦克就开始被生产出来。在这个过程中，操作者只需要知道点鼠标下达指令，之后收获指令的结果。点一下鼠标，几分钟之后得到一辆坦克，至于工厂里面具体如何生产一辆坦克，SCV如何获得矿石，这些细节被屏蔽掉，不用在关心。将来现实世界，传统行业的一切都会变成这样，甚至连下达指令的（玩游戏）的这个操作者早晚也会被软件替代。

我并不是在写科幻小说，在今天，很多行业已经实现了类似的效果。比如航空业，这个行业里面很多部分已经是高度虚拟化的了，他们已经可以用一个指挥系统调动各种地勤和支持资源去完成航空行业运转的各种流程。当然，他们也需要好多程序员来开发和维护这个系统…

我们再站高一点，看之前描述的场景。现在我们有了若干的资源单元，他们分布在不同的行业，这些单元已经被软件定义好了，我们看作是黑箱。在软件之下，又定义了无数具体工作人员的行为。刚才的例子里面，除了停车场管理员，还有厨师，服务员…沿着这个思路继续想，还会有给餐馆进货，供应原材料的供应商，维修停车场设施的公司…所有这些，会会被虚拟化成软件世界中的一个单元。然后是各种被提供服务的人（所谓用户），他们有接收信息的方式，大到计算机，小到智能手机，或者各种嵌入式系统，比如特斯拉电动车驾驶舱里面的那块大屏幕…一个使用手机的用户，或者一辆特斯拉，同样都可以被抽象成一个带有接口的资源单元。所有资源单元的行为，都是被软件定义的，他们之间的交互方式和可能产生的结果，同样是被软件定义和调配的。这其中的每一层，每一部分，都需要大量程序员的工作。越来越多的现实资源被虚拟化，也就产生了更多的交互和更多的可能性，这些一样需要程序员去实现。今天，人类社会被虚拟化成软件的资源还只有极少的部分，我没有具体统计的数字，但大家只要想想自己每天的现实生活所需所用，至少能有个大概的感知，恐怕被虚拟化的资源连1%都不到。未来的空间有多大？几乎是无限量的大。

现实世界能被虚拟化到什么程度呢，我之前几次推荐过科幻小说《雪崩》里面描述了未来的世界只剩下三种职业：娱乐业、程序员和Pizza快递员。这本写于90年代初的小说，早年看起来非常震撼，今天看起来…觉得他还不够极端。因为现在我们已经确知了，Pizza快递员的工作会被无人机改变，娱乐业会被VR/AR改变。最后干脆现实世界只剩下了程序员这一种职业…软件并没有吞噬掉现实世界，而是重新定义了现实世界的所有资源。

所以，今天一切关于软件/互联网泡沫的看法都是过时的。现实世界的虚拟化已经快到了相当的程度，我们真的需要大量的程序员，未来仍然需要，有多少都不够用。因为程序员职业缺口太大了，早就不是有钱就能招聘到的了，甚至一个程序员因为公司要打卡，就会选择另外一家企业，因为他们可选择的余地实在太大了。很多企业远远没意识到问题的严重性，而聪明的企业，已经在忙着做“企业技术文化”工作了。如果你不是BAT，又不是一个很酷的新公司，程序员们根本对你没有兴趣，到这个境地，花别人一倍的钱也未必能雇到人，所以就需要做技术文化工作，去宣传我们也是很酷的，我们也是能改变世界的…从而不至于在这种竞争中落后。

最近一段时间，我周围很多其他行业的朋友都跑来问我，是不是他们应该学写一点程序。我通常都回答，只要你有兴趣，学的下去，那就当然应该。就算不能成为职业程序员，在这个软件定义一切的行业里面，理解程序如何产生，理解程序员如何工作，那就一定会有一份更好的职业机会等着你。为什么不学呢？

### 模拟（Simulation）

虚拟化的一种重要特例是模拟。为什么要模拟？

一种原因是控制上面的。在各种动力学，化学反应等等中，我们很难在实际中造出精确的模型，让每个分子或者流体初态在我们预定的位置。即使我们可以控制，有些实验是破坏性的，比如纳米材料经过处理后就失效了，我们不希望这样；有些是危险的，比如核爆炸，或者测试计算机病毒。这些都要求我们使用“虚拟”的环境进行测试。

下面是宇宙学模拟的结果（早期大尺度网状宇宙）：

![universe simulation](/static/the_computational_thinking/3A2A26D4D4C625C559485A928740385B.jpg)

计算机科学的一个重要断言是 `图灵-丘奇命题 (Church-Turing hypothesis)`：

> 通用计算机能够模拟任意实际的物理过程 [2]

然而上面的结论只说了原则上可行，而没有说实际上可行（考虑到效率）。考虑到最近量子计算机的可能性，它的加强版是：

> 经典计算机能够有效模拟任意经典（指非量子）物理过程，量子计算机能够有效模拟任意考虑到量子效应的物理过程。（并且）以同种物理性质为其基础状态而制造的通用计算机总是能够有效地模拟同种物理性质下的物理过程。

至今为止这个断言没有反例。这也是为什么各种各样的现实问题能够用计算机模拟的原因。

一个特殊的例子是计算机模拟计算机，提供这种功能的软件称为 “虚拟机软件”，有的时候我们说 “在虚拟机里面装Linux” 意思就是在虚拟机软件虚拟的计算机上安装Linux。

更加特殊的例子是自己模拟自己。在程序上这种程序称为 `quine`。比如下面是一个 C 语言的 quine，它的运行结果是输出自己的代码：

{% highlight c %}
{% raw %}
#include <stdio.h>
char *program = "#include <stdio.h>%cchar *program = %c%s%c;%cint main()%c{%cprintf(program, 10, 34, program, 34, 10, 10, 10, 10, 10, 10);%c    return 0;%c}%c";
int main()
{
printf(program, 10, 34, program, 34, 10, 10, 10, 10, 10, 10);
return 0;
}
{% endraw %}
{% endhighlight %}


## 回溯

想象一下下面一种情况：

如果一个粗心的孩子在回家的时候发现手套不见了，但是希望找回，那么他会怎么办呢？

他很可能会倒着原来走的路走一遍。

很多时候，我们的“到达”只是触发事件的动机，而“回溯”的过程才是得到结果的方式。这样的事情其实相当多，比如侦查案件这些都是。

另外回溯常常用于搜索。比如一种 OOXX 的小游戏（轮流下O和X，然后谁先连成3个的直线就赢）。

它是否有必胜策略呢？一种寻找方式就是像下面的图一样列出所有可能的游戏情况，只要一直写下去，就一定能得到某些情况下有一方赢了或者输了。（这张图中我们把每一个情形称为一个“结点”，结点下面连着的结点称为它的“孩子”）

![Game Tree](https://upload.wikimedia.org/wikipedia/commons/d/da/Tic-tac-toe-game-tree.svg)

那么怎么知道是否有必胜策略呢？答案是回去找。对于每个X赢的结果，从下往上画一条线；如果你发现，无论怎么选择O，你总有办法选择某些X，使得这些O和X落在线上（实际上有更高明的MINMAX算法），那么就意味存在必胜策略。

这也是计算机下棋的重要方法之一（后来有了各种改进，比如 alpha-beta 剪枝，以及 monte-carlo tree search 等）。

回溯还常常用于调试等寻求错误原因的过程中。

另外回溯的一种特例是递归，它在计算，甚至数理逻辑中起到了非常根本的作用，和计算机打交道的过程中会反复遇到它。


## 形式化语言

我们日常用的语言并不是那么严格，容易发生偏差。著名的实验是世界各地都举办过的传话游戏。传话游戏是一个古老的多人游戏，为从队伍首端通过耳语或肢体语言传达一句话至队尾，通常游戏结束时最初的那句话已变得面目全非。这个从侧面表现了自然语言的不稳定性。我们在日常对话中不会感觉到是因为我们往往一次只在少数中间交流，且出错很容易被别人纠正。但是一个严格的系统中很难有这种假设，我们日常说话的态度对待一些性命攸关的控制系统并不是好的行为。

数学和物理为了严格地描述领域内的东西，都发明了一套符号系统。而计算机则是用一套类似自然语言，但是严格的语言系统来严格地描述程序的行为。这些语言被称为编程语言(programming language)，它们是形式化语言的一种。

关于编程语言我们会在后面细讲。

## 还有哪些没有提到？

### 并发

并发是非常重要的一种模式，其对性能有着非常重要的影响，并反映到生活中我们处理一些成规模的事件的态度。我们会在后面细讲。

### 编译

广义的编译是指将一种形式化语言转变成另外一种形式化语言，同时保留原来的执行逻辑的行为。这部分概念比较大也会在后面讲。

### 复杂度

算法复杂度的思想直接关系到问题是否能够有效解决，当代的诸多安全性问题和此相关。复杂度部分还有著名的 $\text{NP}\neq\text{P}$ 这个未解的数学难题。

### 开源和社区

如何鼓励人们自由贡献？计算机领域的开源精神和社区模式给出了一种解答。Wikipedia，Reddit等等都直接或者间接受益于此。

### 版本控制和持续集成

如何远程开展合作？如何以最快的速度推进开发？如何在频繁的迭代更新下保持正确性？如何快速发现错误？如果快速撤销错误的决定？版本控制和持续集成给了我们一些答案。


## 写后感

唉，怎么写都不够淋漓尽致啊。


## 附注

[1] Jeannette M. Wing  曾是卡内基梅隆大学（宾夕法尼亚州匹兹堡）计算机学院的首席教授和学院负责人，美国国家自然基金会计算与信息科学工程部助理部长。曾任Microsoft研究院副总裁，负责监督全球核心研究实验室和Microsoft Research Connections。她也是 ACM 和 IEEE Fellow。著有非常短但是被引用极多的计算思维相关论述： https://www.cs.cmu.edu/~15110-s13/Wing06-ct.pdf。由于这篇文章的影响，多个国家自06年后开展了较为普遍的针对所有 K-12 教育机构的计算机教育，以及将计算思维作为方法论隐含地融入教育体系之中。

[2] 当然首先这个物理过程本身是有限的。热力学系统中降温到绝对零度的过程本身就需要无限长时间，和模拟无关。相关内容参见 Deutsch, D. (1985, July). Quantum theory, the Church-Turing principle and the universal quantum computer. In Proceedings of the Royal Society of London A: Mathematical, Physical and Engineering Sciences (Vol. 400, No. 1818, pp. 97-117). The Royal Society.