# Title: An Image-based Approach to Extreme Scale In Situ Visualization and Analysis
## Link: https://datascience.dsscale.org/wp-content/uploads/2016/06/AnImage-basedApproachToExtremeScaleInSituvisualizationAndAnalysis.pdf
## Publication:  
SC '14: Proceedings of the International Conference for High Performance Computing, Networking, Storage and Analysis
## Author：
James Ahrens
Los Alamos National Laboratory
Los Alamos, NM 87545
Email: ahrens@lanl.gov  
John Patchett
Los Alamos National Laboratory
Los Alamos, NM 87545
Email: patchett@lanl.gov  
Sebastien Jourdain ´
Kitware Inc
Santa Fe, NM 87505
Email: sebastien.jourdain@kitware.com  
David H. Rogers
Los Alamos National Laboratory
Los Alamos, NM 87545
Email: dhr@lanl.gov  
Patrick O’Leary
Kitware Inc
Santa Fe, NM 87505
Email: patrick.oleary@kitware.com  
Mark Petersen
Los Alamos National Laboratory
Los Alamos, NM 87545
Email: mpetersen@lanl.gov
## paper review:
* Main picture:  
![ParaviewCatalyst](https://github.com/guansLab/PaperReading/blob/master/Zhengyong_Ren/Screenshot%20from%202019-10-24%2011-49-03.png)
* Research Background:  
Computer simulations are growing in sophistication and producing results of ever greater fidelity. This trend has been
enabled by advances in numerical methods and increasing
computing power. Yet these advances come with several
costs including massive increases in data size, difficulties examining output data, challenges in configuring simulation
runs, and difficulty debugging running codes.

* Problem to Solve:  
Interactive
visualization tools, like ParaView, have been used for postprocessing of simulation results. However, the increasing
data sizes, and limited storage and bandwidth make high
fidelity post-processing impractical.

* Key Design and Algorithm Proposed:  
Paraview Catalyst

* Major Contribution:  
ParaView Catalyst is a data
processing and visualization library that enables in situ analysis and visualization. In this paper, we presented the steps
involved in instrumenting a simulation code with Catalyst
support along with some of our successes.

* Something you don’t understand:  
I didn't really understand how VTK work in the Paraview.
* Your view on the research domain/topic/approach/data/solution (positive or negative):  
I think the Paraview Catalyst framework is a good idea to solve the limited storage and bandwidth　problems in simulate the large sizes data.
