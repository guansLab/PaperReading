Paper Reading Note
===
>Date： 2019年12月16日16:00:32
Author: Shaolun
***

Title: *MetricsVis: A Visual Analytics System for Evaluating Employee Performance in Public Safety Agencies*
---
![Screenshot](https://raw.githubusercontent.com/shaolun-Ryan/Coding-Workstation/master/static/%E6%90%9C%E7%8B%97%E6%88%AA%E5%9B%BE20191216210611.png)

Publication: *IEEE VIS 2019(VAST)*
---

Author: *Jieqiong Zhao, David S. Ebert*
---

  
Paper Review
---
#### Research Background
Organizational performance evaluation can be useful for strategic planning, staff management, and operational development. An effective performance evaluation system with clearly defined goals and prompt feedback is essential for organizations to improve their productivity, especially with limited resources and personnel. Oftentimes, employee, unit, and organizational performance characterization requires considering multiple facets such as economic return, social impact, sustainability, and team and individual productivity. 
#### Problem to Solve
Developing an appropriate method to integrate multiple aspects, including qualitative, quantitative, and subjective data into an accurate representation of an organization’s performance is challenging. The task is further complicated when different employee teams have different workloads based on shifts and locations, as is common in public safety organizations. As a result, the study of this paper proposed a visual analystic tool MetricsVis to evaluate the performance of individual, group and oranization quantitatively and qualitatively.


#### Key Design and Algorithm Proposed
Zhao et al. present MetricsVis, a visual analytics system for evaluating the performance of individual employees, teams, and the entire organization in public safety agencies. Zhao et al. designed the system iteratively with users from two medium-sized law enforcement agencies (representing similar-sized organizations in our study). Zhao et al. rooted our metrics in the existing organizational performance literature and adaptively tailored MetricsVis to meet the requirements of public safety organizations with groups of employees performing similar jobs but at different locations and times, resulting in different workloads that impact their contribution to organizational goals. Additionally, Zhao et al. formalized the analytical tasks, goals, and metrics; derived metrics; and surveyed organizational personnel and the public to decide on priorities of evaluation. Zhao et al. implemented multiple coordinated views in MetricsVis to support efficient, effective, and dynamic performance evaluation for multiple levels of an organization. The MetricsVis system enables a holistic evaluation of organizational priorities versus actual achievements, and helps identify opportunities for improvement. Additionally, it facilitates evaluation of strategic goals, expedites resource allocation (e.g. understanding which employees may need additional training or would be good trainers), and improves workload balance and individual employee performance.

#### Major Contribution
* The mapping of the analysis of public-safety organizational performance evaluation into four visual analytical task categories.
* A novel system supporting interactive visual organizational performance analysis in public safety agencies based on hybrid evaluation metrics that integrate quantitative employee data and qualitative subjective feedback, and appropriate visual representations to support the four aforementioned visual task categories.
* A system evaluation with domain experts from two medium-sized law enforcement agencies to validate system usability.
#### Major limitation
For visualization design, Zhao et al. deduced that a tabular visualization summarizing all employees provided better utility than graphs of individual statistics. Besides the individual performance, Zhao et al. noticed the importance of providing overview on the aggregated group results. After examination of different designs in small multiple settings, they adopted a dandelion glyph, which is a variation of star coordinates. they added the stacked radar chart to bridge the gap betZhao et al.en dandelion glyph (group) and performance matrix (individual). The radial layout can show only a limited number of visually differentiable categories; hoZhao et al.ver, the number of common job types across different teams is limited, and filtering interactions and selection by keyboard can improve the usability.

#### Your view on the research domain/topic/approach/data/solution  

这项工作common的不太常见，在我的印象中vis的工作似乎都是非常的high的，不是in situ，就是new approach，而这项工作，就是用post data设计了一套系统，然后用故事 的形式写成了这项paper。这好像和我之前认识的VAST的风格有点相似，这说明我们不管用什么套路，只要system本身是非常make sense的，那么顶会都不是问题。
本工作用一组public safety agency的data，将agency内部的个人、团体和组织的workload都用多种view刻画了出来，而且之间可以用交互，最关键的是，他们工作的可视化设计并不是多么的创新，而是每一种view每一个维度的设计都是恰到好处，这样设计出来的系统兼具美观和实用。我大概总结了一下他们工作能上IEEE vis的几点理由：
* paper第一页的视图很美观
* 有domain experts的评估
* user interface和视频做的很make sense
* 文章写作的结构和措辞都非常ok，写作技巧也非常的好
* 故事脉络讲得很清楚
* 设计做的很到位，每一个元素都运用的恰到好处
* 这是一篇可以以后拿来经常借鉴的paper。学习他的写作技巧

*The link of this article is [here](https://github.com/guansLab/PaperReading/blob/master/Shaolun/P5_Shaolun_191216.md)*
