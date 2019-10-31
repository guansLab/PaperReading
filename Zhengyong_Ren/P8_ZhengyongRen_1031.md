# Title: Real Time Visualization of Monitoring Data for Large Scale HPC Systems
## Link: https://ieeexplore.ieee.org/document/7307671
## Publication:  
Published in: 2015 IEEE International Conference on Cluster Computing
## Author：
Michael Showeman
National Center for Supercomputing Applications
Univ. of Illinois
Urbana, IL.
mshow@ncsa.illinois.edu 
## paper review:
* Main picture:  
![](https://github.com/guansLab/PaperReading/blob/master/Zhengyong_Ren/Screenshot%20from%202019-10-31%2010-56-29.png)
* Research Background:  
High Performance Computing (HPC)
system users and administrators are often hampered in
their ability understand application performance and
system behavior due to a lack of sufficient information
about how resources, such as memory, CPU, networks
and filesystems are being used.

* Problem to Solve:  
While obtaining the
related data is a necessary step, it is insufficient without
tools that can turn the data into actionable information.
Required capabilities of such tools are the ability to
efficiently handle vast amounts of data in a timely
fashion, the presentation of effective and
understandable information representations for large
node counts, and the correlation of that data with job
and system events.

* Key Design and Algorithm Proposed:  
  visualization approaches and tools that combined with the use of freely available web interfaces for both system
administrators and users. 
 Insights from the visualizations both at the system and the job levels 
* Major Contribution:  
1, parallel
database models with the goal of using Blue Waters'
Lustre filestem to store the information
2,A group of service nodes on the system to scale up the processing and memory utilized in the process. 
* limited
File based data processors such as ODP yield reasonable performance, but lack convenience and flexibility
* Something you don’t understand:  
Figure 1 shows an example of a day's worth of data for free node memory. what is free node memory?
* Your view on the research domain/topic/approach/data/solution (positive or negative):  
I think the　types of visualization is too single,and the effect of the visualization is not so good.
