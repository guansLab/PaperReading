# Title: Projecting Performance Data Over Simulation Geometry Using SOSflow and ALPINE
## Link: https://vpa17.github.io/pdfs/VPA_2017_wood.pdf
## Publication:  
ESPT 2017, ESPT 2018, VPA 2017, VPA 2018. Lecture Notes in Computer Science, vol 11027. Springer, Cham
## Author：  
Chad Wood(University of Oregon),Matthew Larsen(Lawrence Livermore National Laboratory),Alfredo Gimenez(Lawrence Livermore National Laboratory),Kevin Huck(Lawrence Livermore National Laboratory),Cyrus Harrison(Lawrence Livermore National Laboratory),Todd Gamblin(Lawrence Livermore National Laboratory),Allen Malony(University of Oregon)
## Paper Review

* Research Background:  
Projecting application and performance data onto the scientific domain allows for the behavior of a code to be perceived in terms of
the organization of the work it is doing, rather than the organizationof its source code. 

* Problem to Solve:  
The overhead of manually instrumenting large complex codes to extract meaningful geometries for use in performance analysis,combined with the limited value of offline correlation of a fixed number of metrics, naturally limited the usage of scientific domain projections for gaining HPC workflow performance insights.

* Key Design and Algorithm Proposed:  
Use SOSflow and ALPINE to overcome many prior limitations to projecting performance into the scientific domain.

* Major Contribution:  
1,Eliminate the need to manually capture geometry for performance data projections of ALPINE-enabled workflows.
2,Provide online observation of performance data projected over evolving geometries and metrics.
3,Facilitate interactive selection of one or many performance metrics and rendering parameters, adding dynamism to projections.
4,Enable simultaneous online projections from a common data source.
5,In situ performance visualization architecture supporting both current and future-scale systems

* Major limitation:  
1,Workflows that use the ALPINE framework but have complex irregular meshes, feature overlapping "halo regions".
2,Operate over non-continuous regions of space within a single process, may require additional effort to extract geometry from, depending on the organization of spatial descriptions they employ.

* Your view on the research domain/topic/approach/data/solution (positive or negative)  
It is a good choice to solve some complex problems by using the functions of existing tools. In this paper,they employs the scalable observation system SOSflow with the in-situ visualization framework ALPINE to automatically extract simulation geometry and stream aggregated performance metrics to respective locations within the geometry at runtime.
