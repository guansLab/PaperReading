
### Title: DECAF++: Elastic Whole-System Dynamic Taint Analysis

### Publication: 22nd International Symposium on Research in Attacks, Intrusions and Defenses ({RAID} 2019

### Author：Ali Davanian, Zhenxiao Qi, Yu Qu, and Heng Yin (University of California, Riverside)

  
### Paper Review

- Research Background

Whole-system dynamic taint analysis has many unique applications such as malware analysis and fuzz testing. Compared to process-level taint analysis, it offers a wider analysis scope, a better transparency and tamper resistance. The authors already proposed a whole-system analysis tool DECAF. 


- Problem to Solve

The main barrier of applying whole-system dynamic taint analysis in practice is the large slowdown that can be sometimes up to 30 times. Existing optimization schemes have either considerable baseline overheads (when there is no tainted data) or specific hardware dependencies. They try to reduce the overhead of DECAF

- Key Design and Algorithm Proposed

1. Aims to remove the taint propagation overhead whenever possible. 
 It is based on the intuition that taint analysis can be skipped if the taint analysis operation does not change any taint status value. Taint analysis operations can possibly result in a change only when either of the source or the destination operand of an instruction is tainted
 2. to avoid unnecessary interactions with the shadow memory. 
 In DECAF, checking happens for every memory operation. 
 They can avoid the overhead per memory address if we perform the check for a larger set of memory addresses. Thus, if the larger set doesn’t contain any tainted byte we can safely skip the check per address within that set. The natural sets within a system are physical memory pages.


- Major Contribution

Two independent optimizations to achieve the elasticity
1 elastic taint status checking: 2.6 times overhead 
2 elastic taint propagation: 1.8 times overhead.  

  
- Major limitation

The overhead is still high based on QEMU since QEMU's overhead is high.
  

- Something you don’t understand

  

- Your view on the research domain/topic/approach/data/solution  (positive or negative)

This DECAF++ is an update of DECAF, and the main Promotion from DECAF is Elasticity. Whole-system dynamic taint analysis applications like intrusion detection systems and honeypots can greatly benefit from the elastic property. It is a Good idea for other taint analysis tools too.
