Paper Reading Note
===
>Date: 2019年12月23日 21点05分
Author: Shaolun
***

Title: *TitLearning Vis Tools: Teaching Data Visualization Tutorialsle*
---
![Screenshot](https://github.com/shaolun-Ryan/Coding-Workstation/blob/master/static/1223.PNG?raw=true)

Publication: *IEEE VIS 2019（short paper）*
---

Author: *Leo Yu-Ho Lo, Yao Ming, and Huamin Qu*
---

  
Paper Review
---
#### ![#f03c15](https://placehold.it/15/e4a0e7/000000?text=+) Your view about the research
这篇文章是第一篇short paper，算上最后的reference一共五页，章节是这样划分的 introducction，related work， challenge and reuirement, tutorial design, student feedback. 这个工作是屈华民老师的一个教学报告，介绍了一门他和他的团队教授的课程数据可视化的情况。选择这一篇工作阅读的理由是：本文介绍了如今最流行最主流的可视化工具和框架，可以拓展自己的学科视野，但是读完整篇文章发现，似乎只有VAST方面的visualization tools，SciViS涉及的很少。接下来我将大概总结一下这篇工作所阐述的工作，供大家参考和学习。
#### ![#f03c15](https://placehold.it/15/f03c15/000000?text=+) Research Background

教学数据可视化是可视化领域中最重要的活动之一。 随着商业和科学专业人士对数据分析的兴趣日益浓厚，数据可视化课程吸引了不同学科的学生。 但是，全面的可视化培训要求学生在编程方面具有一定水平的熟练程度，这对老师和学生都构成了挑战。 随着可视化工具的最新发展，我们设法通过教授各种可视化和支持工具来克服这些障碍。本篇文章就是简述屈华民老师是如何在他的可视化课程教授学生可视化概念和编程技术，还伴随着一些可视化工具的简述以及者之间的比较。以下，我将提炼的知识性内容做一个总结：

#### ![#c5f015](https://placehold.it/15/c5f015/000000?text=+) No Programming Tools
* MicroSoft Excel
* Tableau
* GIS
以上的三种工具都是基于existing data or datatset，不需要任何的编程基础就可以完成书数据展示的目的。但是正因为如此，图表的扩展性和灵活性受到了很大的制约，which means，作者只能利用既有的可视化模型或者框架，不能根据自己的idea组合或者生成新的图表。而且，图表的样式还是比较单一，多是刻画统计量或者地理位置的可视化模型，如同表示关系、颜色映射、三维几何模型等图形时显得扩展性不是很强。

#### ![#1589F0](https://placehold.it/15/1589F0/000000?text=+) Vis Tools Needing a Certain Capability of Programming
* D3
* Vega-Lite
* HighChart & Echarts
除去python的可视化库(下文会单独说明), 最有代表性的可视分析研究人员所用的工具就是以上几种，或许还有其他的框架，但都是大同小异，不在赘述了。相比于第一种对编程零基础的库来说，这一种代码需要coder具有更强的代码能力，但是所获得的成果则是更多，因为我们可以走出局限，去设计和实现我们想要的各种图形。此类型的库有着几处共同的特点，首先都具有格式化数据格式的能力，将raw data重新组织（或者重构）成可以解析的结构，其次，再将重构完成的数据交给生成器（enter()过程）。在整个过程中，我们可以在程序合理的情况下，去异构图形结构，甚至可以将多种结构结合在一起。What a play!

#### ![#f03c15](https://placehold.it/15/FF2A00/000000?text=+) Platforms With Server On It
本文介绍了两种线上的编译平台：Google Colab和Observable, 这两种工具的出现，是解决了在可视化的过程中需要重新架构server来响应font-end的需求。Observable是一个线上的JS noteBook，可以让coder在线编写js程序，并且可以实时注册DOM元素和运算的web工具。Google Colab则更偏向于python的运行，是编写python可视化的很好的平台。这两项服务使整体学习体验非常流畅，并鼓励非CSE学生将可视化融入课程结束后的工作场所。
#### ![#f03c15](https://placehold.it/15/9C9B46/000000?text=+) Python Vis Tools
* matplotlib
* ggplot
* ggplot2
基于python的数据可视化库。特点如下：
* 可以及时的让coder看到具象 的 数据的可视化，效率高
* 容量大 运算速度快，不依赖其他外部环境
* 缺点是不够灵活的实现需求 需要定制框架
* 适合做实时观测数据 或者精确的统计数据（比如散点图或则柱形图）
* 和user application不容易兼容，合适做论文的插图或者作报告

Thanks for reading！

*Note：昨天在洗澡的时候，突然想到了可视化的一个很有趣的idea。我们习惯于在可视化的过程中运用单个的可视化图形，非常忌讳或者在避免图形之间的融合或者覆盖，因为这样会掩盖图标想表达的真正含义。但是，如果偏偏要用融合的效果来展示我们想表达的东西呢，线条？不合适。图形？也不合适。颜色？yeah，颜色不怕叠加，甚至偶然的叠加会产生意想不到的效果。所以说，用颜色的重叠后的效果来表示我们想观察的融合后的效果（比如化学反应，枪支和瞄准镜之间的组合效果），是对融合后抽象的结果的一种具象化。举个例子，玩过cf的人知道，如果我们自己组装一个武器，有三种组合的选项（枪的型号、瞄准镜的种类和支架的型号），比方说枪有x种，瞄准镜有y种，支架有z种，那么最终的组合结果会有`x*y*z`中配对结果，玩家为了配出最好的枪，用这么多的基础元素一个一个的配对，对比每一种的结果参数（精度、威力、后坐力），每一个配对的结果必然都是不同的，所以导致玩家甚至拿出了小本本，写下了每一种结果的三种参数的值。有没有一种更好的对比方式让玩家可以更有效率的选择出最佳的配对方案呢？类似的有雷达图，每一个维度代表一个参数（精度、威力、后坐力），但是`x*y*z`个雷达图，排列出来就是一个有难度的事情，user去捕捉特点则更加的困难。那么用颜色呢？`x*y*z`个色块？似乎不是已经那么庞杂和冗余了。我们可以用亮度代表射击精度，饱和度代表子弹威力，从蓝到红表示后坐力越来越大。如此一来，玩家prefer哪一个参数，岂不是一目了然？这其中参杂了由参数到RGB值运算的算法，以及对颜色的定义和设计。难点是颜色的各项指标的浮动对影响到其他参数的观察，所以这只是一个idea，具体实现的话，需要更合理的设计思路*

*The link of this article is [here](https://github.com/guansLab/PaperReading/new/master/Shaolun)*
