---
layout: post
title:  计算思维译文（带原文对照）
comments: true
excerpt: "入门－真实的 Computer Science & Technology"
date:   2016-09-16 +2327
categories: lecture
---

*by Jeannette M. Wing*

> It represents a universally applicable attitude and skill set everyone, not just computer scientists, would be eager to learn and use.

> 计算思维展现了一种普适的观点和技能，不仅适合计算机学家，也适合所有人学习和使用

Computational thinking builds on the power and limits of computing processes, whether they are executed by a human or by a machine. 

计算思维建立在对计算这个过程本身的能力和限制的（理解）之上，（这种计算能力）不分人还是机器。

Computational methods and models give us the courage to solve problems and design systems that no one of us would be capable of tackling alone. 

计算方法和计算模型给予我们解决问题和设计系统的底气－－这些东西凭一个人本身的能力是很难应付的。

Computational thinking confronts the riddle of machine intelligence: What can humans do better than computers? and What can computers do better than humans?

计算思维直面这样的谜团：人类究竟在何处比机器优越，机器又能在哪些地方战胜人类？

Most fundamentally it addresses the question: What is computable? Today, we know only parts of the answers to such questions.

它（还试图）回答这样的问题：什么东西是可计算的？直至今日我们对此所知也只是冰山一角。

>

Computational thinking is a fundamental skill for everyone, not just for computer scientists. To reading, writing, and arithmetic, we should add computational thinking to every child’s analytical ability. 

计算思维不仅是计算机学家，也是每个人的基本技能。为了阅读、写作、算术我们需要将将计算思维作为孩子分析能力的一部分。

Just as the printing press facilitated the spread of the three Rs, what is appropriately incestuous about this vision is that computing and computers facilitate the spread of computational thinking.

恰如出版社促进了3R（一说阅读、写作、算术这种教育体系）的传播，计算和计算机加速了计算思维的传播。

>

Computational thinking involves solving problems, designing systems, and understanding human behavior, by drawing on the concepts fundamental to computer science.Computational thinking includes a range of mental tools that reflect the breadth of the field of computer science.

计算思维透过计算机科学的基本观念解决问题，设计系统，理解人类行为。它包含一些理念上的能够折射出计算机科学纵深的工具。

>

Having to solve a particular problem, we might ask: How difficult is it to solve? and What’s the best way to solve it? Computer science rests on solid theoretical underpinnings to answer such questions precisely. 

（如果）需要解决一个特定问题，我们或许会问：它难度有多大？解决它的最好办法是什么？计算机科学基于坚实的理论基础来精确回答这些问题。

Stating the difficulty of a problem accounts for the underlying power of the machine — the computing device that will run the solution. We must consider the machine’s instruction set, its resource constraints, and its operating environment.

执行解决方案的机器本身的能力决定了解决问题的难易程度。我们必须考虑机器的指令集，资源限制和操作环境。

>

In solving a problem efficiently, we might further ask whether an approximate solution is good enough, whether we can use randomization to our advantage, and whether false positives or false negatives are allowed. 

即使我们能够有效地解决问题，我们也会进一步探讨一个近似解是否足够好，是否可以利用随机的方法来得到某些优势，并且还关系到假阳性（遗漏了正确解）或者假阴性（多出了错误解）是否被允许。

Computational thinking is reformulating a seemingly difficult problem into one we know how to solve, perhaps by reduction, embedding, transformation, or simulation.

计算思维通过规约，嵌入，变换或者模拟的方法，可以将一个难题转变为我们知道如何解决的问题。

>

Computational thinking is thinking recursively. It is parallel processing. It is interpreting code as data and data as code. It is interpreting code as data and data as code. It is type checking as the generalization of dimensional analysis. It is recognizing both the virtues and the dangers of aliasing, or giving someone or something more than one name. It is recognizing both the cost and power of indirect addressing and procedure call. It is judging a program not just for correctness and efficiency but for aesthetics, and a system’s design for simplicity and elegance.

计算思维递归地思考问题，并行的处理事务，它对数据和代码一视同仁（从而我们可以反射和元编程），它将维数分析一般化为类型检查（用类型封装复杂结构，从而降低了使用的复杂度。类似于将高维度空间紧致到0维，然后使用空间的代称），它展现了同一命名或者给予东西不止一个名字的两面性。它展现了间接寻址和过程调用的得失（原则上大多数间接寻址和过程调用都没有必要或者被其他方法代替，但是这会给人带来严重的逻辑负担）。它不止用正确性和效率衡量程序的优良，也包括（内在逻辑的）美观性，以及系统设计的简约高雅。

>

Computational thinking is using abstraction and decomposition when attacking a large complex task or designing a large complex system. It is separation of concerns. It is choosing an appropriate representation for a problem or modeling the relevant aspects of a problem to make it tractable. 

计算思维使用抽象和分解来对付一个大的复杂的任务或者设计一个复杂系统。这是一种对事务的分离。计算思维为问题选择合适的表述形式或者为问题各方面的关联建模来使得它易于处理。

It is using invariants to describe a system’s behavior succinctly and declaratively. It is having the confidence we can safely use, modify, and influence a large complex system without understanding its every detail. It is modularizing something in anticipation of multiple users or prefetching and caching in anticipation of future use.

计算思维简要和声明式地（用“做什么”来解决问题，并且等价于“怎么做”。这样可以减少很多副作用）使用不变量来描述系统的行为（循环不变量等等，这些保证了算法的正确性）。它给予我们安全使用，修改，影响一个大的复杂系统而不必理解它的细节的信心。它为将来预期的多用户使用，预取，缓存使用了模块化的方法。

>

Computational thinking is thinking in terms of prevention, protection, and recovery from worst-case scenarios through redundancy, damage containment, and error correction. It is calling gridlock deadlock and contracts interfaces. It is learning to avoid race conditions when synchronizing meetings with one another.

计算思维考虑到预防，保护，通过冗余、错误限制、错误纠正这些方法从最坏的情况恢复。考虑到拥塞（例如A和B通信，由于B处理太慢导致没有及时回复A，A由于收不到成功回复认为B没有收到于是试图向B发送更多消息，最终导致B的彻底崩溃）、死锁（A等待B，B等待C，C等待D，D等待A和C，最终这样会一直等待下去）、和接口合同（不一致的接口会导致无法协同工作）。它学习如何在互相同步时避开竞争条件（竞争条件会导致不可预期的结果）。

>

Computational thinking is using heuristic reasoning to discover a solution. It is planning, learning, and scheduling in the presence of uncertainty. It is search, search, and more search, resulting in a list of Web pages, a strategy for winning a game, or a counterexample. 

计算思维使用启发式方法来寻求问题的解。它在不确定的环境下规划、学习、调度。它通过一次次的搜索来得到网页列表，赢得游戏的策略，或者一个反例。

Computational thinking is using massive amounts of data to speed up computation. It is making trade-offs between time and space and between processing power and storage capacity.

计算思维使用大量数据加速计算。它试图在时间和空间，计算能力和存储能力间取得平衡。

> Thinking like a computer scientist means more than being able to program a computer. It requires thinking at multiple levels of abstraction.

> 像计算机学家一样思考远远不止写程序。它要求在多个层次的抽象上思考。

Consider these everyday examples: When your daughter goes to school in the morning, she puts in her backpack the things she needs for the day; that’s prefetching and caching. 

考虑这样的每日的例子：当早晨你女儿去学校的时候，她将一天所需放在背包里；这是预取和缓存。

When your son loses his mittens, you suggest he retrace his steps; that’s back-tracking. 

当你的儿子丢了连指手套，你建议他沿着原来的路找一遍；这是回溯。

At what point do you stop renting skis and buy yourself a pair?; that’s online algorithms. 

什么时候你停止租用滑雪板转而自己买一个？这是在线算法。

Which line do you stand in at the supermarket?; that’s performance modeling for multi-server systems. 

你站在超市的哪个结账队列？这是多服务系统的性能模型。

Why does your telephone still work during a power outage?; that’s independence of failure and redundancy in design. 

为什么停电时你还可以用电话？这是设计时的错误独立性和冗余。

How do Completely Automated Public Turing Test(s) to Tell Computers and Humans Apart, or CAPTCHAs, authenticate humans?; that’s exploiting the difficulty of solving hard AI problems to foil computing agents.

如何使用完全自动化的公开图灵测试来区别人和机器，或者为什么使用验证码验证人类？这是利用困难的人工智能问题来糊弄计算机程序。

>

Computational thinking will have become ingrained in everyone’s lives when words like algorithm and precondition are part of everyone’s vocabulary; when nondeterminism and garbage collection take on the meanings used by computer scientists; and when trees are drawn upside down.

当像“算法”和“先决条件”这样的词汇在每个人的字典中，当“不确定性”和“垃圾回收”带有计算机学家所使用的意思，当“树”被倒过来画（自上而下），计算思维就早已经是每个人心中根深蒂固的东西了。

>

We have witnessed the influence of computational thinking on other disciplines.

我们会见证计算思维对其他学科的影响。

For example, machine learning has transformed statistics. Statistical learning is being used for problems on a scale, in terms of both data size and dimension, unimaginable only a few years ago. Statistics departments in all kinds of organizations are hiring computer scientists. Schools of computer science are embracing existing or starting up new statistics departments.

例如，机器学习造成了统计学的改革。统计学习被用来解决一定规模的问题，无论怎样的数据规模和维度，这在早些年前还是不可想象的。各个统计相关的机构都在招募计算机学家。而计算机学院也在拓展已有的或者新建立统计部门（不过正如我们所见某些学校不会的）。

>

Computer scientists’ recent interest in biology is driven by their belief that biologists can benefit from computational thinking. Computer science’s contribution to biology goes beyond the ability to search through vast amounts of sequence data looking for patterns. The hope is that data structures and algorithms—our computational abstractions and methods—can represent the structure of proteins in ways that elucidate their function. 

相信计算思维能够给生物学家带来好处造成了计算机学家近年来对生物的兴趣。计算机科学对生物学的贡献超出了从大段序列中发现模式。我们希望数据结构和算法－－这是我们计算上的抽象和方法－－能够表达蛋白质的结构特性并阐明其功能。

Computational biology is changing the way biologists think. Similarly, computational game theory is changing the way economists think; nanocomputing, the way chemists think; and quantum computing, the way physicists think.

计算生物学正在改变生物学家思考的方式。类似地，计算博弈论在改变经济学家思考的方式；纳米计算在改变化学家思考的方式；量子计算在改变物理学家思考的方式。

>

This kind of thinking will be part of the skill set of not only other scientists but of everyone else. Ubiquitous computing is to today as computational thinking is to tomorrow. Ubiquitous computing was yesterday’s dream that became today’s reality; computational thinking is tomorrow’s reality.

这种思维会成为不止计算机学家，而且是每个人的能力。普适计算（泛在的计算，比如你的手机，街头的监控，传感器，射频卡，车牌识别，等等等等）对于如今正如计算思维对于未来。普适计算是昨日的梦俨然变成今天的事实，（而我们可以断言）计算思维会是将来的事实。

---

### WHAT IT IS, AND ISN’T

### 计算思维是什么，不是什么

Computer science is the study of computation — what can be computed and how to compute it. Computational thinking thus has the following characteristics:

计算机科学研究计算本身 — 什么可以计算并且怎样计算. 计算思维因此有以下特性:

*Conceptualizing, not programming*. Computer science is not computer programming. Thinking like a computer scientist means more than being able to program a computer. It requires thinking at multiple levels of abstraction;

*计算思维是概念化的，而不是编程这种东西*。计算机科学不是计算机编程。像计算机学家一样思考意味着比编程更多的东西。它需要在多种抽象层次上思考；

*Fundamental, not rote skill*. A fundamental skill is something every human being must know to function in modern society. Rote means a mechanical routine. Ironically, not until computer science solves the AI Grand Challenge of making computers think like humans will thinking be rote;

*计算思维是基础和根本的，而不是可以死记硬背的技巧*。基本技能是每个人在现代社会都必须知道如何使用的东西。而死记硬背（按部就班）是一种机械的途径。讽刺的是，如果计算机科学解决了强AI这个巨大的挑战，（那么就有证据说明）人类的思考（可能也是）一种机械的操作;

*A way that humans, not computers, think*. Computational thinking is a way humans solve problems; it is not trying to get humans to think like computers. Computers are dull and boring; humans are clever and imaginative. We humans make computers exciting. Equipped with computing devices, we use our cleverness to tackle problems we would not dare take on before the age of computing and build systems with functionality limited only by our imaginations;

*计算思维是人类而不是计算机思考的方式*. 计算思维是人类解决问题的方式；它并不是试图使人像计算机一样思考。计算机迟钝而无聊；人类聪明并且富有想象。正是我们使得计算机激动人心。有了计算设备的助攻，我们使用我们的聪明才智来解决那些计算时代之前无法克服的问题，建立复杂的系统，限制我们的仅仅是我们的想象；

*Complements and combines mathematical and engineering thinking*. Computer science inherently draws on mathematical thinking, given that, like all sciences, its formal foundations rest on mathematics. Computer science inherently draws on engineering thinking, given that we build systems that interact with the real world. The constraints of the underlying computing device force computer scientists to think computationally, not just mathematically. Being free to build virtual worlds enables us to engineer systems beyond the physical world;

*互补和合并数学思维和工程思维*。数学思维内禀于计算思维，（计算机科学）正如所有的科学一样，它的基础基于严格的数学，建造与现实世界交互的系统。我们所依赖的底层计算设备的限制驱使计算机学家按照计算的方式去思考，而不只是数学的方式；而可以建造虚拟世界的能力允许我们造出超越物理世界的系统。 

*Ideas, not artifacts*. It’s not just the software and hardware artifacts we produce that will be physically present everywhere and touch our lives all the time, it will be the computational concepts we use to approach and solve problems, manage our daily lives, and communicate and interact with other people; and

*计算思维重在想法，而不是成品*. 它不会仅仅是那些现实中随处可见的软件硬件成品, 它会是一种我们用来解决问题，管理日常生活，和别人沟通交互的计算的观念；并且

For everyone, everywhere. Computational thinking will be a reality when it is so integral to human endeavors it disappears as an explicit philosophy.

（接上文）它适合于每个人，每一处。它真实地融合在人类事业中，却又隐藏在明确的理念中。

>


Many people equate computer science with computer programming. Some parents see only a narrow range of job opportunities for their children who major in computer science. Many people think the fundamental research in computer science is done and that only the engineering remains. 

许多人将计算思维和计算机编程混为一谈。一些家长仅仅预见到了计算机专业的孩子很狭隘的一部分工作机遇。很多人认为计算机科学的基础研究部分已经完成并且只剩工程的部分。

Computational thinking is a grand vision to guide computer science educators, researchers, and practitioners as we act to change society’s image of the field. 

计算思维为计算机教育者，研究者，参与者提供了广阔的视野的同时也改变了社会对于这个专业的印象。

We especially need to reach the pre-college audience, including teachers, parents, and students, sending them two main messages:

我们亟需向即将融入大学教育的受众，包括老师，家长和学生，传递这样两条主要信息：

*Intellectually challenging and engaging scientific problems remain to be understood and solved*. The problem domain and solution domain are limited only by our own curiosity and creativity; and

*（仍然有）智力挑战和吸引人注意的科学问题等待我们理解和解决*。限制问题和解决方法的领域的只是我们的好奇心和创造力；并且

*One can major in computer science and do anything*. One can major in English or mathematics and go on to a multitude of different careers. Ditto computer science. One can major in computer science and go on to a career in medicine, law, business, politics, any type of science or engineering, and even the arts.

*一个人可以从事计算机科学并且从事任何事情*。一个人可以从事英语或者数学然后走向各种各样的职业生涯。计算机科学也一样。一个人可以主修计算机然后从事医药，法律，商业，政治，或者任何其他类型的科学和工程，甚至于艺术。

>

Professors of computer science should teach a course called “Ways to Think Like a Computer Scientist” to college freshmen, making it available to non-majors, not just to computer science majors. We should expose pre-college students to computational methods and models. Rather than bemoan the decline of interest in computer science or the decline in funding for research in computer science, we should look to inspire the public’s interest in the intellectual adventure of the field. We’ll thus spread the joy, awe, and power of computer science, aiming to make computational thinking commonplace.

计算机科学的教授应该向新人，而且不仅仅是本专业学生教授一门叫“像计算机学家一样思考”的课程。我们应该将计算方法和模型在大学前就暴露给学生。我们应该寻求激发大众对这个领域思维冒险的兴趣，而不是哀叹（人们）对计算机科学兴趣的减弱或者科研资金的减少。我们会因此传播计算机科学的乐趣，敬畏，力量，从而让计算思维无处不在。

---

*Jeannette M. Wing (wing@cs.cmu.edu) is the President’s Professor of Computer Science in and head of the Computer Science Department at Carnegie Mellon University, Pittsburgh, PA.*

*Jeannette M. Wing (wing@cs.cmu.edu) 是卡内基梅隆大学（宾夕法尼亚州匹兹堡）计算机学院的首席教授和学院负责人*
