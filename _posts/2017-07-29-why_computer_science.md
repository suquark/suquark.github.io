---
layout: post
title: 为什么我选择计算机科学
comments: true
mathjax: true
excerpt: "computer science"
date:   2017-07-29 +1627
categories: lecture
---

作为一个即将毕业的学长，这些年很受科大照顾，多次出国比赛交流。而我这个人呢也很直，希望能够帮到新生。从15级开始我每年开学都会给新生做若干次交流（包括不限于新生活力社团讲座，去年讲了量子计算和深度学习；14级经验交流等等），本人也在各个年级新生班群中看着新生会怎么发展。去年还担任了计院程序设计课程的助教（虽然因为比赛等原因我个人觉得自己不是很尽职）。

我花费这么多时间做这些事情，动机（基于对教育学的兴趣）还在于希望了解为什么新生选择 Computer Science，以及什么样性格和态度的人会发展的很好，做的很好。

经过对 13, 14, 15, 16 这4个年级的了解，我得出了至少下面一些有待商榷的结论：
- 不是所有人都适合学习 CS，甚至不适合的比例不小。有一部分人在后期会对课程比较厌恶或者怠惰（除去课程质量本身的原因）
- 对 CS 感兴趣但不过于钻牛角尖的人大多发展比较成功，他们自学和独立解决问题能力较强
- 自 15 级开始全校转 CS 的兴趣暴增。报名转院的人数接近本院原先人数的 80%，转入本院的人数接近 60%
- 暴增的人中一部分是因为学原来专业学不下去而转CS，这部分学生中有相当一部分成绩和能力平平（不过他们未来收入还是很可能远高平均）；另外一部分是看好了CS收入高或者讨厌原来的专业，这部分大致的水平要稍微高一点。
- 新生年级会有相当大一批人入学时不知道为什么来了科大，也不知道为什么学了计算机，也对自己的学科不甚了解

这些现象让我觉得，有必要让新生在现在就对计算机有个详尽的了解。

然后根据不少人的反馈，在我所有形式的报告中（习题课，公开课视频，讲座交流，面对面谈，板书...），我写blog的水平最高，内容也最为完整严密。所以这次我准备些一篇长篇 blog。

# 编程篇

![IMAGE](/static/why_computer_science/A9B5E93EDEBAD190EF0261B53EA2B9F7.jpg)

## 对CS的误解

CS 是不是主要就是编程？结论是否定的。说CS主要是编程，就如同说数学主要是解方程。不过新生对于编程的熟悉程度远远不如解方程。

以下是编程和解方程的共同之处：

- 它们都遵循一定的规范，服从一些经验，有方法和套路。
- 它们都有例可偱，有“经典”问题
- 它们都从浅入深，随着能力增强可以解决越来越复杂的问题。
- 不懂数学的人很可能认为他们整天在解“1+1”，稍懂计算机的人认为他们整天在写代码，完全不懂计算机的人认为他们整天在修电脑。

以下是区别：

- 编程更多是解决“元问题”，即解决怎样解决问题的问题。因此编程可以解方程，这时候编程的内容就是“描述如何解方程”，而不是解方程本身，而编好的程序本身在计算机上运行的时候才执行真正的解方程流程。大量的科学计算软件就是做的这种事情，可以说现如今最繁杂的一些方程都是计算机根据程序的描述解的，这些方程如果要人工求解足以耗尽全世界的人力。
- 编程是更加创造式和构建式的。编程一开始入手写的内容可能和题意相去甚远（为了实现一些基础构件），尤其是非常大的项目。
- 编程是迭代式推进的。编程会一步一步地将东西构建完成，可能反复撤销更改，甚至要重构；解方程一般不会如此。
- 编程很多时候涉及到多人协作和版本控制的问题（记录保持几百个版本很正常）。解方程除了特殊时期特殊需求一般不会如此。
- 编程的问题类型远远多于方程的分类，基本是什么需求就有什么问题。
- 编程很多时候能够一眼看到底，因为它的目的是完成需求而不是得出解。
- 编程依赖的基础工具是编程语言。一种编程语言类似于一套数学符号或者物理规范，不同的语言可能适合不同场合下的编程。
- 编程的过程性更加强。方程解对了，中间各个过程都正确，也没有什么再太苛求的地方。编程更近似于一种社会劳动，有协作和继承的特性，因此极其注重中间质量。比如 [PEP8](https://www.python.org/dev/peps/pep-0008/) 标准对 python 这种语言的格式要求的内容写了接近1000行的描述。
- 有些方程解起来的难度可能非常大（不过因此有些解也会用程序近似）
- 只会编程可能工资还挺高，但是只会解方程。。。



好了，看了这眼花缭乱的一段，让自己休息一下吧~

看了这么多描述，你可能觉得编程并不是一件简单的事情。实际上也是如此，我们至今仍然不知道我们设计程序能力的上限，我们知道我们的程序能够发射火箭控制卫星，调度全国的电网，支撑起整个互联网，构建电子金融和电商平台，完成比特币交易，控制核电站运转，调度整个物流系统，能放音乐能放电影能跑游戏，能跑在每一部智能手机上面，跑在（电子锁的）小黄车里面，能扫描二维码能水群能禁言，能识别物体能识别语音能翻译文字，能下围棋能完美驱动两个脚是轮子的机器人，能支持核打击系统和导弹防御系统，能让当代军用加密系统难以出现二战德国Enigma那样的事故，能处理引力波数据，能模拟化学反应模拟风洞模拟刚体形变模拟核反应模拟弹道轨迹，能画函数图像能P图能用数位板画画，能设计奥运会鸟巢钢架结构，能导航能规划路线，能“嘀！学生卡”，也能像 WannaCry 一样让人不能毕业。

我们用了什么魔法？或许正如《西部世界》中所说，只有魔术师才知道这不是魔法，而常人已经意识不到当今社会高效运转严重依赖各种各样的程序，人编出来的程序。而下一步一些人推崇的 IoT（物联网） 正是希望让 “万物联网”，让几乎一切都在程序的驱动之下。

## Why money loves computer science?

### 因为懒惰

我们想象一下没有计算机前和之后，远程购物（现在基本上是网上购物）的区别。

![IMAGE](/static/why_computer_science/6169FBF2159F9BE2182F59592963831C.jpg)

如果我们需要买一个本地没有的东西，首先我们需要到处打听它在哪里的消息。但是，买东西的人数往往远远多于常见的被买的物品的种类。我们于是懒一点，每个物品做一个网页，然后被若干人看若干遍不就行了。

其次我们需要付账。付账就是把我们的钱从一个账户转到另外一个账户里。账户和钱会因为数量和所有者不同（在一般付款的意义下）有本质的区别吗？并没有。我们于是懒一点，做一套交易系统，所有人都通过同一套系统给别人转账（比如支付宝，或者微信支付）。

然后收款方需要发货。然而发货的本质只是将物品从一个地方运到另一个地方。我们同样可以使用同一套系统进行物流分发。

收到货物后需要确认。这也是一套基本相同的操作，于是我们可以用同一套系统完成。

这里我们看到的是，**很多现实中的任务都是机械的、重复的**，它们作为社会规律或者社会形式会存在相当长的时间；但是解决它们的方法，却是相对固定的；而解决解决问题方法的方法，目前我们知道的为数不多的东西叫编程，而被如此大批量的使用且如此成功的，恐怕也只有编程。

![IMAGE](/static/why_computer_science/37E314B9F2C3FA5CCE0F2FFB39DFBEE7.jpg)

### 因为它是灵魂而不是肉体

作为程序的存在，可以跑在光纤里，可以跑在无线电波里，跑在电缆里，睡在硬盘里，光盘里，U盘里；可以以光速移动，可以塞入细小的晶粒，可以随意复制，可以随意分享。

损坏的身体和机械，多数难以修复，但是损坏的软件或许只需要重装。

工厂（由于内部设计问题）出了导致生产全面停止的故障，一般很难在短期内恢复；但是一个宕机的网站，却往往能在几个小时内恢复。

### 因为方法免费

解决现实问题，总是要费用的。但是相当一部分程序或者服务却是免费的。人们很愿意使用这些服务（比如各类搜索引擎，比如各类网上商城）；开发者也很乐意使用其中的一些免费程序，特别是所谓的开源程序。

### 因为代码也免费

IT业界这些年发展推动的一个重要动力是，开源(open source)。即开放程序的源代码，这样我们得以知道写程序的具体流程，可以稍微修改以用于不同的问题。

就 Github 上面的开源的工程就超过 10,000,000 个，包含数亿万行代码；而 Linux 等操作系统上大部分组件都是开源的。很可能这些开放的代码的量级和 Wikipedia+百度百科 的文本内容总量相当。

在这些开源项目的推动下，整个IT业界的更新换代速度是极其快的，远远超过传统工厂设备更换的速度。

### 因为是真正的“无产阶级”

你要造一个瓷杯子，你需要什么？可能你需要锻造炉，一些黏土，燃料，钳子，模具...，这些都是实在的资产，并且需要你亲自接触它们。

你要写一个程序，你需要什么？无论何时何处，一台电脑，一个WiFi，一个电源，足矣。

你产出的是什么？不是一个证明和构想，而是一个解决方案。

然后后者却往往可以卖更多钱。

## 编程与理性，逻辑

唉，等等，万一这些程序突然全部失效怎么办？刷学生卡“交易失败”，导弹漫天飞，反导系统打自家基地，电网损毁大面积停电，毕业论文被删的一干二净，听什么音乐都是永恒的东风，银行存款变成随机数。。。

![IMAGE](/static/why_computer_science/D1ACEC7203AF29A0CE7FAD2A72D45152.jpg)

但是，这些几乎都没有发生，虽然历史上有过程序错误造成的惨痛教训，但是比起实际中数以万亿计的程序的表现几乎可以忽略。

现在我们仍然讨论的是CS中冰山一角的编程。编程是什么？程序怎样保证它的正确性？

![IMAGE](/static/why_computer_science/C4C69D18ADB67B8611B6789A3CA34E2E.jpg)

## 插曲：正确的蓝屏

以下是经典的蓝屏界面（新的系统中变得更加友好），系统出问题的时候会显示。

![IMAGE](/static/why_computer_science/D024AC0048E38BBE6044E46D15472DDD.jpg)

但是如果你曾经仔细看过，就会发现第一行写的是：

> A problem has been detected and windows has been shutdown to prevent damage to your computer.

也就是说，蓝屏的作用是为了保护计算机不受破坏。这个时候系统发现了某些意外情形，觉得无法处理，感到害怕(panic)，于是终止一切任务防止意外情形破坏系统逻辑并显示蓝屏。

不同系统会有不同的“蓝屏”，一般来说 Linux/*nix 这些操作系统会显示 `Kernel panic` 字样。

![IMAGE](/static/why_computer_science/6357BC09C933F9EFBF8B51008B6885BC.jpg)

![IMAGE](/static/why_computer_science/BC3BCF1BC5480119F05849FE6618FADB.jpg)

在今后你们的编程中，会出现各种各样的“异常”和“错误”，请庆幸它们的发生，这说明你的错误被正确的发现了。如果一切顺利而结果不对，才是最致命的问题。

### 模型与面向对象

我有一个苹果，又叠一个苹果，那么我有几个苹果？

这个如果不是一个无聊的脑筋急转弯那么显然 1 + 1 = 2。数学总是对的。

![IMAGE](/static/why_computer_science/10FA403951AB11F04C6559AFFCB23901.jpg)

我有一块橡皮泥，又叠一块橡皮泥，那么我有几块橡皮泥？这个时候可能需要三思了。一个合理的答案可能是1。这里如果用 1 + 1 = 2 似乎就不对了。

但是 1 + 1 = 2 对不对？如果1是整数1，+是对整数意义的加，2是整数2，=是整数意义下的等词，那么它是对的。

但是这样它也是一个废话，除了形式以外没有任何的意义(而在逻辑上就是没有意义，因为逻辑不在乎它的具体形式)。如果你熟悉皮亚诺公理，就应当知道 1 + 1 = 2 是一些“显然正确的公理”推导出来的必然正确的内容。如果你把这些“废话”当成有意义的东西就会造成所谓 [废话谬误](https://zh.wikipedia.org/wiki/%E5%BB%A2%E8%A9%B1%E8%AC%AC%E8%AA%A4) 

那么，难道数学除了公理和定义都是废话？显然不是。问题在于，如果赋予形式化的数学内容以个体对象，那么这个数学系统就是某种数学模型（Mathematical model）[1] 

数学的有用之处在于能够将世间诸多现象用一些数学模型加以描述。有些模型非常精密符合，比如物理学的数学模型[2]；有些则宽松一些，比如股票模型。用准确的模型预测未来正是人类理性的体现。一个非常严格的模型也必然导致严格不会出错的结果。

CS恰好也建立了模型。CS如何建立模型？一个重要的手段就是OOP（面向对象编程）。CS将一个实体（人，银行账户，城市等等）及其属性，谓词，函数，相互之间的关系代数，等词这些，打包成一个 class (类)，一个具体的对象称为class的一个实例（instance）。注意这里class实际上是一种“元实例”；一个描述人这个实体的class，仅仅含有模型中需要的“人”的性质，而它的实例中才会有具体的内容(身高的数值等等)。类相对于实例就好像是模板对于产品一样，但是不同的是，这里的“产品”允许有各自的内容。

![IMAGE](/static/why_computer_science/AFC18DA241A220A0DA44E82A483F4447.jpg)

程序的代码本质上也是一种废话，它只会忠实地被计算机执行，没有真正意义上的“正确错误”，一切都是“对的、必然的”（如果你在这里想到了计算机程序中的异常(exception)，异常实际上也是一种错误处理的规范，最底层仅仅按照Intel芯片手册忠实执行而已）。有了OOP之后，我们可以更好的为实际问题建立正确的模型，规避逻辑上的错误）。

这时候想想，真正有意义的其实是代码的组织结构本身，这也是需要各种代码规范的重要原因。虽然数学证明得到的结论在逻辑的意义上是“废话”，但是在证明的层面上，精妙的证明依然赏心悦目；虽然工程构建得到的代码在计算机硬件的意义上是“废话”，但是在编程的层面上，精妙的代码依然赏心悦目。

不是所有语言都支持OOP，不过现代的语言几乎都有OOP的支持。C和汇编这种不支持OOP的语言更容易出现各种bug的重要原因之一[3]。

当然OOP不是万能的，过度使用OOP将形成过于复杂的模型，反而偏离的了客观事实。如何正确建立对象的模型是一个长期存在的问题。

在数据库系统设计中也用到了类似的思想来建立模型，这里的对象称为entity(实体)。

### 类型系统

我不准备详细介绍这个部分，因为它很复杂（虽然也非常精密严格），让这篇文章难以理解。
类型系统（type system）是一套严格的、保证逻辑正确的系统。在OOP的模式下它的定义和作用更为明确。
type 和 class 的关系是，（某种意义下）一个class可以对应一种类型，而程序中的实例会带有这些类型信息；这样违背类型信息的操作将会被识别出来。

## 编程语言（programming language）

很多新生学计算机最头疼的一件事情是如何学习一门编程语言。

编程语言就本质上说，是一种 formal language（规范化语言）。它和自然语言有诸多根源上的相同之处，这点在语言学(linguistics)上由Chomsky等人进行过非常深入的研究, 并产生了 [Chomsky hierarchy](https://en.wikipedia.org/wiki/Chomsky_hierarchy) 的概念[4]。

但是在实际编程中，你会发现它和自然语言非常不同：程序语言是完全逻辑的，只不过由于根源上的类似长得很像。如果你不用逻辑，而是用自然语言的方式对待编程语言，那么你很可能会陷入迷茫之中。

由于这篇文章不是为了介绍编程语言，所以这里就不细写了。我可能会考虑之后的一些简单教程。


# 结语

我写《为什么我选择计算机科学》的关于编程的这一部分，已经写了这么多了。真心感到CS的浩瀚。。。

### 附注

[1] 注意 Mathematical Model 和数学中的 [Model Theory](https://en.wikipedia.org/wiki/Model_theory) 精神相同但稍有区别，实际上后者和著名的哥德尔不完备定理有非常根本的联系。
[2] 物理学的数学模型不一定一开始就非常严格。模型也需要进行一些修补和增强。尤其越为近代的物理体系对数学模型的要求越高。经典力学中数学分析或者实分析就可以解决绝大多数问题；但量子力学用到的delta函数这些，等到泛函分析比较完善后才比较严格；而相对论显然依赖于微分几何。当代的高能物理中仍然有一些严格性问题尚待解决，我们也不能保证对应的数学模型一定能符合实验结果(如果不符合就要修正对应模型)。
[3] 不过现在一般人们不会用C或者汇编来写大项目，除了特殊需求（比如嵌入式开发，高性能计算，操作系统中的一部分等等）。另外C语言等也可以通过一些命名和组织规范来模拟OOP的效果。
[4] 在这里你将很惊奇地看到图灵机和正则表达式居然和Chomsky hierarchy密切相关，它们分别描述了不同层级的语言。