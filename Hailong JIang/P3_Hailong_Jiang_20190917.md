Title: Modeling Soft-Error Propagation in Programs

Publication: DSN

Author：Guanpeng Li, Karthik Pattabiraman, Siva Kumar Sastry Hari, Michael Sullivan, Timothy Tsai
University of British Columbia, NVIDIA 

Paper Review
Research Background

Resilience Research: Find the resilient/not-resilient part of the code and Protect
Do Fault Injection (FI)  to estimate the SDC probabilities of programs. (Monte Carlo)
Thousands of FIs  too much time to be practical 
Modeling error propagation model to identify vulnerable instructions


Problem to Solve

To estimate the SDC probability of a program without fault injectioin – both in the aggregate, and on an individual instruction basis - to decide whether protection is required

Key Design and Algorithm Proposed

The key insight: error propagation in dynamic execution can be decomposed into a combination of individual modules, each of which can be abstracted into probabilistic events. 

Major Contribution

TRIDENT, predict both the overall SDC probability of a program and the SDC probability of individual instructions based on dynamic and static analysis of the program without performing FI. 
error propagation follows program data-flow at runtime
model data-flow at three levels: 
(1) Static-instruction level, corresponding to the execution of a static data-dependent instruction sequence and the transfer of results between registers. (fs)
(2) Control-flow level, when execution jumps to another program
location. (fc)
(3) Memory level, when the results need to be transferred back to memory. (fm)

Major limitation

Not really accurate in all situations

Something you don’t understand

1. Is the error propagation probability correct? 1/32 in Figure 1.
2. How did they know the branch probability of each branch? Like in Figure 3.
3. Is that computation of fc correct?



Your view on the research domain/topic/approach/data/solution (positive or negative)
