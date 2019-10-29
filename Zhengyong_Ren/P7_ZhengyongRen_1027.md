# Title: An Image-based Approach to Extreme Scale In Situ Visualization and Analysis
## Link: https://datascience.dsscale.org/wp-content/uploads/2016/06/AnImage-basedApproachToExtremeScaleInSituvisualizationAndAnalysis.pdf
## Publication:  
SC '14: Proceedings of the International Conference for High Performance Computing, Networking, Storage and Analysis
## Author：
James Ahrens,
Los Alamos National Laboratory
Los Alamos, NM 87545
Email: ahrens@lanl.gov  
John Patchett,
Los Alamos National Laboratory
Los Alamos, NM 87545
Email: patchett@lanl.gov  
Sebastien Jourdain, ´
Kitware Inc
Santa Fe, NM 87505
Email: sebastien.jourdain@kitware.com  
David H. Rogers,
Los Alamos National Laboratory
Los Alamos, NM 87545
Email: dhr@lanl.gov  
Patrick O’Leary,
Kitware Inc
Santa Fe, NM 87505
Email: patrick.oleary@kitware.com  
Mark Petersen,
Los Alamos National Laboratory
Los Alamos, NM 87545
Email: mpetersen@lanl.gov
## paper review:
* Main picture:  
![](https://github.com/guansLab/PaperReading/blob/master/Zhengyong_Ren/Screenshot%20from%202019-10-29%2010-52-31.png)
* Research Background:  
Extreme scale scientific simulations are leading a charge to exascale computation, and data analytics runs the risk
of being a bottleneck to scientific discovery. Due to power and I/O constraints, we expect in situ visualization and analysis will be a critical component of these workflows.
Options for extreme scale data analysis are often presented as a stark contrast: 
write largefiles to disk for interactive, exploratory analysis, or perform in situ
analysis to save detailed data about phenomena that a scientists
knows about in advance. 

* Problem to Solve:  
The fundamental extreme scale visualization and analysis challenge is there is too much simulation data and too little transfer bandwidth. In situ techniques can analyze the data while it still resides in simulation memory.However in situ approaches either are a predefined set of analyses or, rarely, make automatic decisions about which analyses and visualizations to create.

* Key Design and Algorithm Proposed:  
 An Image-based Approach and Database

* Major Contribution:  
1,Interactive Exploration Image Database.  
2,Metadata Searching.  
3,Creation of New Visualizations and Content Querying.

* Something you don’t understand:  
The query file and histogram.
* Your view on the research domain/topic/approach/data/solution (positive or negative):  
This image-based approach is a good idea to solve Extreme Scale data by using database, based the image database we can do
interactive exploration and metadata querying.
