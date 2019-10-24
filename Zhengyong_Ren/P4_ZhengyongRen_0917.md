# Title:Extreme Scale In Situ Analysis with ParaView Catalyst
## Link: https://www.researchgate.net/publication/305347639_Extreme_Scale_In_Situ_Analysis_with_ParaView_Catalyst
## Publication:
ISC Workshop On In situ Visualization 2016At: Frankfurt
## Author：
Joachim Pouderoux   Andrew Bauer  Julien Jomier   Berk Geveci(Kitware SAS, Kitware Inc)
## Workshop review:
* Main Picture
![](https://github.com/guansLab/PaperReading/blob/master/Zhengyong_Ren/Screenshot%20from%202019-10-24%2008-44-53.png)

* Research Background:
As supercomputing moves towards exascale, scientists, engineers and medical researchers will look for efficient and cost effective ways to enable data analysis and visualization for the products of their computational efforts. The ‘exa’ metric prefix stands for quintillion, and the proposed exascale computers would approximately perform as many operations per second as 50 million laptops. 

* Problem to Solve:
Typical spatial and temporal data reduction techniques employed for post-processing will not yield desirable results where reductions of 10e3 to 10e6 may still produce petabytes to terabytes of data to transfer or store. Since transferring or storing data may no longer be viable for many simulation applications, data analysis and visualization must now be performed in situ.

* Key Design and Algorithm Proposed:
Latest Paraview Catalyst:Catalyst is a light-weight version of the ParaView server library that is designed to be directly embedded into parallel simulation codes.

* Major Contribution:
Introduce the current status of ParaView Catalyst, one of the leading production quality in situ frameworks.  It has been integrated into dozens of simulation codes and has been scaled up to 1M MPI ranks. This workshop focus on recent advancements in Catalyst.

* Limitation:
1,At scale file IO for data extracts
2,In transit workflows (Burst Buffers, ADIOS, etc) 
3,Catalyst editions with even smaller library sizes 
4,Advanced Cinema options 
4,Parallelism appropriate with simulation code’s parallelism (e.g. MPI, OpenMP, CUDA, threads, VTK-m, vtkSMPTools, etc.) 

Your view on the research domain/topic/approach/data/solution (positive or negative):
This workshop introduce the detail of Catalyst workfolw, make it easy to understand Paraview Catalyst.
