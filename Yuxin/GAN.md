### Title: Generative Adversarial Networks

### Publication: NIPS

### Author: Ian Goodfellow et al.

### Paper Review
- Research Background

Although there are many generative models existing, those models cannot learn enough probabilistic distributions from data, thus they cannot produce convincing fake data. Even though there are some works using two networks to learn from data, those works don't satisfy training criterion. 

- Problem to Solve



- Key Design and Algorithm Proposed

1. Adding an adversarial network, discriminator, to estimate the data generated from the generative network. 
2. Discriminator and Generator play a minimax game to 

- Major Contribution

1. Using backprop instead of Markov chain to calculate gradients. 
2. 

- Major Limitation

There should be synchronization between Discriminator and Generator during training. 

- Something You Don't Understand



- Your view on the research domain/topic/approach/data/solution (positive or negative)


