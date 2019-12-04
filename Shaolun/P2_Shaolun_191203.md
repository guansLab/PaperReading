Reading Note(2)
===
Anatomy of "La VALSE: Scalable Log Visualization for Fault Characterization in Supercomputers"
---
>Date： 
Author: Shaolun
***

Publication: *Eurographics Symposium on Parallel Graphics and Visualization (2018)*
---

Author: *Hanqi Guo, Sheng Di, Rinku Gupta, Tom Peterka, and Franck Cappello*
---

- ![#f03c15](https://placehold.it/15/f03c15/000000?text=+) `#f03c15`
- ![#c5f015](https://placehold.it/15/c5f015/000000?text=+) `#c5f015`
- ![#1589F0](https://placehold.it/15/1589F0/000000?text=+) `#1589F0`
  *色块在文中都是成对出现的，可以视为带有颜色的括号*
***

### Abstract
![#f03c15](https://placehold.it/15/0044FF/000000?text=+)We design and implement La VALSE—a scalable visualization tool to explore tens of millions of records of reliability, availability, and serviceability (RAS) logs—for IBM Blue Gene/Q systems. Our tool is designed to meet various analysis requirement,including tracing causes offailure events and investigating correlations from the redundant and noisy RAS messages.![#f03c15](https://placehold.it/15/0044FF/000000?text=+) ![#f03c15](https://placehold.it/15/33A400/000000?text=+)La VALSE consists of multiple linked views to visualize RAS logs; each log message has a time stamp, physical location, network address, and multiple categorical dimensions such as severity and category. The timeline view features the scalable ThemeRiver and arc diagrams that enables interactive exploration of tens of millions of log messages. The spatial view visualizes the occurrences of RAS messages on hundreds of thousands of elements of Mira—compute cards, node boards, midplanes, and racks—with viewdependent level-of-detail rendering. The multidimensional view enables interactive filtering of different categorical dimensions of RAS messages.![#f03c15](https://placehold.it/15/33A400/000000?text=+) ![#f03c15](https://placehold.it/15/F07A2B/000000?text=+)To achieve interactivity, we develop an efficient and scalable online data cube engine that can query 55 million RAS logs in less than one second.![#f03c15](https://placehold.it/15/F07A2B/000000?text=+) ![#f03c15](https://placehold.it/15/030061/000000?text=+)We present several case studies on Mira, a top supercomputer at Argonne National Laboratory. The case studies demonstrate that La VALSE can help users quickly identify the sources of failure events and analyze spatiotemporal correlations of RAS messages in different scales.![#f03c15](https://placehold.it/15/030061/000000?text=+)


摘要原文如上。
本文的摘要分为了四部分。
![#f03c15](https://placehold.it/15/0044FF/000000?text=+)蓝色是开篇第一句，说明了研究设计和实现的系统的名称，解释了LA VALSE大致功能，说明了实验对象的类别 IBM geneQ system。下一句更加具体的说明了系统的功能 tracing causes offailure events and investigating correlations from the redundant and noisy RAS messages。
![#f03c15](https://placehold.it/15/33A400/000000?text=+)绿色部分详细的 按照view的划分 来逐一解释系统的功能。其中还引出了实验对象Mira。
![#f03c15](https://placehold.it/15/F07A2B/000000?text=+)橙色部分 解释为了实现交互性 抛出了他们的服务器架构： scalable online data cube engine 
最后蓝色部分是对contribution的概括。
***

### 我的Abstract
This paper presents an integrated visualization system JobPlot that employs a two-staged streaming visualization for addressing user-specific behaviors that may cause the issues through analyzing andvisualize system job scheduling data and system usage data. Throughthe tool, administration team can be guided to understand the stateof system. Prior to rendering into visual interface, the data generatedfrom the platform are pre-processed, modeled before delivered to thefront-end visualization interface. The visualization system illustratesa novel technique to visually identify the user’s abnormal operationinstead of reading through the raw data collected from the cloudinfrastructure. We demonstrate the effectiveness and accuracy of theproposed system framework on a real cloud system data trace

自己的摘要如上。前两句还make sense 到第三句Prior to rendering into visual interface, the data generatedfrom the platform are pre-processed, modeled before delivered to thefront-end visualization interface首先不明所以，因为这句话的重要程度放在摘要就很奇怪，而且没有什么内容分和特殊点。
剩下的还算读的通，但是感觉有些幼稚。没有什么闪光点 不像上面paper中那么宏大的感觉，这个技能可能要读很多的paper然后慢慢积累吧
读完Abstract 因为没有啥重大失误但也给人的印象不深，所以估计就是个3/5分的摘要吧
***

### Inctruction
![#f03c15](https://placehold.it/15/0044FF/000000?text=+)Resilience—the most difficult and underaddressed problem in today’s high performance computing—becomes a significant issue as the systems approach exascale.![#f03c15](https://placehold.it/15/0044FF/000000?text=+)**引出resilience** ![#f03c15](https://placehold.it/15/33A400/000000?text=+)For example, in a typical petascale supercomputer, a failure event that causes job termination could happen every several days. Such failures arise from hardware, sys- software, file systems, power, and even the cooling system. Large-scale scientific simulations and data analysis jobs are vulnerable to the errors, because fatal system errors may lead to the unexpected termination and job failures during execution. To this end, researchers have been investigating systems and software that are resilient to failures.![#f03c15](https://placehold.it/15/33A400/000000?text=+)**举例解释Resilience** ![#f03c15](https://placehold.it/15/F07A2B/000000?text=+)Exploring the properties and correlations of the failure events is nontrivial; however, because of the largescale, complicated system architecture that involves hundreds of thousands of various types of modules and components, such as processors, memory units, network modules, and power supplies. ![#f03c15](https://placehold.it/15/F07A2B/000000?text=+)**阐述现在研究背景的困难和不好解决的问题，以及研究受到掣肘的因素**

![#f03c15](https://placehold.it/15/FF2A00/000000?text=+)One of the most important ways to study resilience is to perform posthoc analysis of the logs that record the error, warning, nd informational messages generated by different components in supercomputers. These logs provide the key information that can be used to understand the features of failure events and eventually help resilience researchers improve checkpoint/restart mechanisms and system software designs.![#f03c15](https://placehold.it/15/FF2A00/000000?text=+)**这一段主要解释了现在研究Resilience的主要方法：posthoc analysis of the logs，可能也在解释为什么没有一个实时分析系统而是用post data分析来解释的**

![#f03c15](https://placehold.it/15/030061/000000?text=+)In this paper, we present a scalable visualization framework— La VALSE—to help users explore and understand log data of supercomputers.![#f03c15](https://placehold.it/15/030061/000000?text=+)**承接上面的现有研究方法之后，作者提出了自己的研究方法，但是并没有 直接说LA VALSE相比较其他方法的优势（在下文中提到）** ![#f03c15](https://placehold.it/15/04756F/000000?text=+)We specifically study Mira, which is a 10-petaflops IBMBlue Gene/Q supercomputer at Argonne National Laboratory. The system consists of 786,432 processors, 768 TB of memory, and 24 PB of parallel file system. The interconnection of Mira is a 5D torus network. In our visualizations, we mainly incorporate the reliability, availability, and serviceability (RAS) logs. The RAS logs accumulated over five years have 55 million entries.![#f03c15](https://placehold.it/15/04756F/000000?text=+)**介绍了一下研究对象Mira的基本情况吗，可能是作者的研究资源比较的突出，所以花了些篇幅来介绍这个一般人不太了解的supercomputer的运行情况**

![#f03c15](https://placehold.it/15/2E0927/000000?text=+)The objectives of La VALSE are derived from the needs of two target user groups, resilience researchers and system administrators: (1) interactively exploring tens of millions of logs and (2) correlating errors that occur in different categories, locations, and times. ![#f03c15](https://placehold.it/15/2E0927/000000?text=+)**介绍系统的用户类型，突出系统具有实用性和可用性** First, users need to trace the causes of failures and understand error propagation through interactive exploration. With La VALSE’s scalable visualizations, users can explore the causes of failures with their domain knowledge.**通过例子，将本次研究自然地放进normal的fault event排查任务中** For example, an unexpected memory error could lead to a bit flipping in the code segment of a user application. The bit flipping may cause an instruction error, resulting in failures in functions, threads, processes, and jobs. Second, it is important to correlate different types of errors in order to understand failures. In addition to the obvious correlations uch as memory error and instruction error in the previous example, we must be able to comprehensively identify all correlations of different types of errors that happen in different spatiotemporal locations. **以上的First and Second，很有技巧性的，既阐述了正常failure排查和分析的过程，又侧面的说明了本系统也具有这样的特性，可以帮助分析人员按照原来的流程分析并且简化该流程**

![#f03c15](https://placehold.it/15/33A400/000000?text=+)Major challenges in designing La VALSE include (1) visual representation of noisy and heterogeneous logs and (2) scalability of handling tens of millions of log records for interactive visualization and analysis.![#f03c15](https://placehold.it/15/33A400/000000?text=+)**阐述系统设计的难点和关键问题**

![#f03c15](https://placehold.it/15/9C9B46/000000?text=+)We must design new visual representations for logs that are noisy, heterogeneous, and with hierarchical and high-dimensional network topologies.In general, most of the RAS records are warnings and informational messages, **。。。** In Blue Gene/Q systems, for example, compute nodes are installed on node boards, which are located in different midplanes and racks; compute nodes are also connected in a 5D torus network.

We must also visualize and handle log data with scalability. Mira, which consists of 100K components, has generated 55 million RASmessages in the past five years. **。。。** Instead, we need to redesign scalable OLAP query engines to handle RAS log data.![#f03c15](https://placehold.it/15/9C9B46/000000?text=+)**主要阐述了深红色段落的两个问题，在实现系统方面需要克服的困难和关键问题**

*经过查询，大致明白了文中提到的compute cards， node board， midplane， rack之间的关系，基本上就是后一个上可以承载若干前一个元件的物理关系*

*我比较关注的架构方面的问题，在第二段中也有说明，我大概的凝练一下：这次实验的log data是55,000,000数量级的数据，作者想用themeRiver和arc diagram的方法来实现，但是海量数据导致这两种方法不能很流畅的渲染视图，并且达不到实时交互查询的要求，解决办法：La VALSE通过随着时间对消息进行分档来缩放交互式弧图渲染，并避免使用细节级别渲染过度绘制机器组件。（说实话没看太懂。。看后文有没有比较全面的解释）。交互式查询的本可以用Nanocubes或者imMens来实现，但是这两种tools都比较偏向于地理空间多维度的交互，对处理RAS数据并不是很擅长，所以作者打算重新设计线上分析&处理工具来handle RAS data*

La VALSE features several novel designs in both visualization representation and data handling. We propose scalable ThemeRiver, scalable arc diagrams, and a scalable physical view to enable interactive exploration of tens of millions of log records through web browsers. ![#f03c15](https://placehold.it/15/33A400/000000?text=+)The scalable ThemeRiver magnifies and highlights a small volume of important log messages; the scalable arc diagrams reduce geometry primitives by binning logs for fast and scalable rendering; and the scalable physical view uses semantic zooming and level-of-detail rendering to visualize hundreds of thousands of components on Mira, such as compute cards, link chips, optical modules, and power modules. The implementation of the web-based user interface is based on d3.js, SVG, and HTML5 Canvas. ![#f03c15](https://placehold.it/15/33A400/000000?text=+)More details on the scalable visualization designs are in Section 5.**绿色部分表示了该系统的架构，基于web，还有三个关键view的设计理念**

![#f03c15](https://placehold.it/15/FF2A00/000000?text=+)La VALSE also features scalable querying designs. We developed a customized in-memory database to enable execution of data cube queries for RAS logs with high dimensionality, large volume, and complex physical and topological locations. Not only can the query engine can run in a single machine, but it also is scalable to distributed and parallel environments. We also use a sparse data structure to reduce interprocess communication for scalable querying.![#f03c15](https://placehold.it/15/FF2A00/000000?text=+) More details on scalable querying are in Section 6.
**这一段是对交互式通信的实现的解释，作者运用了in-memory的方式，来对多维度数据实现查询**

**下面的一端是intro的最后一段，主要是对该系统的模型进行了重新的解释，并且列出了所有的contribution，看起来条例非常清晰。**
To the best of our knowledge, La VALSE is the first visualization
framework that addresses the challenge of analyzing RAS logs.
Overall, the contributions of this paper are threefold:
• A scalable log visualization framework for fault characterization
in supercomputers ![#f03c15](https://placehold.it/15/2E0927/000000?text=+)fault characterization![#f03c15](https://placehold.it/15/2E0927/000000?text=+)
• A redesign of scalable ThemeRiver and scalable arc diagrams
for visualizing tens of millions of log records![#f03c15](https://placehold.it/15/2E0927/000000?text=+)重构两种可视化手段ThemeRiver & arc diagrams![#f03c15](https://placehold.it/15/2E0927/000000?text=+)
• A scalable data cube query engine for interactive queries of tens
of millions of log records![#f03c15](https://placehold.it/15/2E0927/000000?text=+)interactive queries![#f03c15](https://placehold.it/15/2E0927/000000?text=+)

![#f03c15](https://placehold.it/15/030061/000000?text=+)The remainder of this paper is organized as follows. Section 2
summarizes the related work. Section 3 gives an overview of the
system, followed by the description of the data. We then introduce
our scalable visualization and querying techniques in Section 5 and
Section 6, respectively. Cases studies and discussions are in Section
7 and Section 8, respectively, followed by the conclusions in
Section 9.![#f03c15](https://placehold.it/15/030061/000000?text=+)**文章结构综述**

***
### Related Work

![#f03c15](https://placehold.it/15/F07A2B/000000?text=+)Our study is related to but different fromperformance visualization, which aims to help high performance computing (HPC) developers profile their software. A comprehensive review of performance visualization can be found in [IGJ14].![#f03c15](https://placehold.it/15/F07A2B/000000?text=+)作者的写作风格就是在相关工作的每一小节刚开始先阐述自己的工作内容，然后再在后文中进行分析。可以借鉴**

The performance visualization community has developed methods to visualize communication traffic in different network topologies, which is critical for HPC developers and administrators for studying communication patterns [IBJ14,WZYK14], investigating network latencies [IGB16], and scaling parallel applications. For example, Isaacs et al. developed Boxfish [ILG12],which can visualize the performance data in 2D and 3D torus networks. Mc- Carthy et al. [MIB14] further generalized Boxfish to 5D torus networks. Ring layout [BGI12] provides another way to project high dimensional networks, and Cheng et al. [CDJM14] further combine parallel coordinates and ring layout for performance visualization. In our study, we also use parallel coordinates to help users filter compute nodes in torus networks, as explained in the following sections.
*** 
### System Overview

![#f03c15](https://placehold.it/15/0044FF/000000?text=+)The main user interface and the system design of La VALSE are illustrated in Figure 1 and Figure 2, respectively. The main user interface of La VALSE comprises multiple linked views including the
timeline view, physical view, multidimensional view, and correlation view. Through the user interface, users can investigate the  data from different perspectives, different spatiotemporal regions, and different query criteria.![#f03c15](https://placehold.it/15/0044FF/000000?text=+)**对用户界面的概括性论述，以及通过界面用户可以达到的功能（包括的视图也提了一下）**

![#f03c15](https://placehold.it/15/33A400/000000?text=+)The timeline view, which features the scalable ThemeRiver and arc diagram designs, visualizes the distributions of RAS logs and job logs over time. All the subviews align with the time axis in the horizontal direction. The job visualization on the top of the timeline has two layers, and each layer aligns with the y-axis that encodes the midplanes (from R00-M0 to R2F-M1). The bottom layer is a heatmap that shows the distributions of RAS messages over different midplanes; the top layer visualizes machine allocations of jobs as semitransparent rectangles. The middle of the timeline view is the scalable ThemeRiver with sampled messages embedded in the rivers. The bottom of the timeline view is the scalable arc diagram that helps users understand time correlations of different RAS messages. Users can browse any time period by zooming
in and brushing. More details on the scalable ThemeRiver and arc diagram designs are in Sections 5.2 and 5.1, respectively. 

The physical view visualizes the spatial distribution of RAS messages in the time period of interest. The physical view provides a scalable level-of-detail rendering and semantic zooming mechanism to enable interactive exploration of RAS messages on more than 100K components in Mira. The physical view also allows users to quickly explore the interconnections between compute nodes. More details on the physical view are in Section 5.3.

 The multidimensional views visualize the statistics of RAS messages with bar charts. Bar charts show how many RAS messages exist for each value in the current data cube query. For example, we show the number of INFO, WARN, and FATAL messages in the severity bar chart, while we simultaneously show the number of messages under different RAS log categories.![#f03c15](https://placehold.it/15/33A400/000000?text=+)**以上三段均是对系统界面的分模块解释。解释的非常清楚。（每个维度是干嘛的，颜色代表什么含义等等。我自己的系统介绍用了很大的篇幅但是 感觉还没作者说的清楚）**

 *Firure 2的示意图是系统架构的示意图，这种表示方法不错，可以运用到自己以后的论文中，非常的清晰简约和明确。*
***

 ### Data Description and Preprocessing
 作者在这一章节进行了对本次研究的系统背景和研究对象和机器进行了一个基本的介绍。分成了两个部分：Mira的架构和研究的RAS数据集。还用了一张表来清楚地向读者展示了数据模型的构成，还伴有Example，学习。这一章节基本上就是科普性的文字，介绍硬件信息和一些变量的名称、含义和简称，介绍的比较的清楚。Figure 3的示意图从系统设计的角度来做解释，让人系统中的view有了一个直观的理解。学习。
***

### Scalable RAS Log Visualization
由于从这里开始文章的内容开始系统的科普LA Valse的设计和功能，不再是像Introduction一样的每一句都有套路的写作，所以不再每一句话都着重分析。

根据系统的三大组件：Scalable ThemeRiver， Scalable Arc Diagram， Scalable Physical View，来进行逐一介绍。每一个组建的介绍被分成了一个独立的subsection。每一个subsection大致有三个段落。第一段介绍view的基本信息和含义，接下来的两端的则是把重点放在了如何把组件scalable。（读完Introduction原本以为scale海量数据的关键点是如何介绍后台Scalable Standalone Query Engine，没想到作者说的scale只是把视图按照比例尺进行缩放。）scalable也是这篇文章的介绍重点，所以作者花了一定的篇幅来讲scalable。

读到这里有一点感想，记录一下：就是说，一个优秀的可视化系统，不一定就包含很多的可视化图表类型。像本文的系统LA Valse，只有三个主要的组件，其中一个还是最基本的bar chart，（另外两个是ThemeRiver和arc diagram），就只有这三个组件构成，但是还有实现了很强大的功能。想想自己之前的一片chinaVis一篇PacificVis，我的思路就是一味地堆砌可视化图形，觉得只要画面够awesome够好看，就可以让reviewer觉得牛逼。。实际上并不是这样，这种想法太年轻了。

***
###Example 
这一章没有subsection，而是分成了五个小的部分，用来解释La Valse的具体使用流程。但是，读完整个章节，我发现作者对系统的使用证明过程不是很有说服力。。也可能是我太菜了get不到。
* 首先作者用了五个方面来解释系统的使用的可用性和有效性，但是让人感觉这五个部分可以分为1+1+1+2，意思是前三个部分是脱离于一个正常的error分析流程的，最后两个部分才正式开始介绍系统在分析burst of network eror时是如何实用的。
* 第一部分不知道什么时候来了一个新的overview of the daily message，在前面没有提及这一个类似于统计的模块。
* 作者就用很少的篇幅，不到1/4页的空间的一个demo，来证明系统的可用性和有效性未免有点缺少说服力。这一个case可能是最突出的、异常的但是最适合作为例子的例子。而且就这一个由于voltage error而导致的error证实可以被La Valse分析出来，那么至于其他原因导致的呢？能不能也可以像这样被推理出来呢？作者似乎也没有明确提到。 

但是除了上面说的这几个方面，其他的点还是值得我学习的。所以这篇文章差不多也要接近尾声了，给我的最大的感想就是，只要自己确实花了功夫，花了时间，做了测试，做了取舍。。等等effort在这项工作中，文章自然内容就可以很多，不愁没得写，给人一种水到渠成的感觉。

架构方面，作者的团队在处理层面用了一个offline data convertion，将tens of million的数据进行16bit处理最终得到460MB的数据，这个方法值得我去学习。另一个处理模块是online in-memory query engine。至于怎么实现的这俩模块，作者并没有明确交代。已向作者发送邮件，正在等待回复。

That's all。以后还是要重视读文献的环节，很受益匪浅。一心埋头码代码是没有出路的。
