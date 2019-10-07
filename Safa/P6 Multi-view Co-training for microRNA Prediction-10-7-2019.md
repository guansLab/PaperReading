
### Title: Multi-view Co-training for microRNA Prediction 

### Publication: bioRxiv (2019): 620740.

### Author： Mohsen Sheikh Hassani1, James R. Green1 *

1Department of Systems and Computer Engineering, Carleton University, Ottawa, Ontario, Canada

  
### Paper Review
- Research Background

Deoxyribonucleic acid (DNA) is a double helix molecule that encodes all the genetic information for a species. For this genetic information to be made usable by the cells, DNA is transcribed into Ribonucleic acid (RNA). MicroRNA (miRNA) are transcribed regions of DNA that, after some biological processes, ultimately form short non-coding RNAs typically in the range of 18 to 25 nucleotides. MicroRNA are involved in cell regulation at the post-transcriptional and translational levels through the degradation and translation inhibition of messenger RNA (mRNA). MicroRNA act on mRNA through a silencing mechanism and target a wide range of mammalian mRNA, affecting biological activities such as cell cycle control, biological development, differentiation and stress response. The majority of current de novo and NGS-based miRNA prediction techniques use supervised learning methods for the detection of novel miRNA, thereby requiring a large database of known miRNA. In addition, these methods do not always achieve high accuracy, resulting in many sequences being falsely predicted to be miRNA. These false predictions represent a substantial loss of resources, as they lead to unnecessary experimental validation costs. Previous work has demonstrated that relying on training exemplars from other species leads to reduced classification performance for the target species. 





- Problem to Solve

A significant challenge in the field of miRNA prediction is that, for many species, there is a scarcity of labelled examples of known miRNA. This makes the task of miRNA classification a very difficult matter, particularly for newly sequenced species where there are few known miRNA exemplars available. While the scarcity of labelled known miRNA data presents a challenge, the emerging abundance of unlabelled sequence and expression data represents a so far untapped opportunity for miRNA prediction. 



- Key Design and Algorithm Proposed

Multi-view co-training was proposed for miRNA prediction, which makes use of multiple views of the problem to create distinct classifiers – one for each view. Each classifier is initially trained on a small set of labelled samples and is applied to an unlabelled data set. The most confidently predicted unlabelled instances from each of these views are added to the training set without experimental validation, and this process is repeated multiple times. In multi-view co-training, they take advantage of the fact that the problem of miRNA prediction can be approached from two distinct views: sequence based de novo prediction or expression-based NGS prediction. This creates two views for classification, an expression-based view and a sequence-based view. It should be noted that both of these views have been previously applied to miRNA classification independently and as an integrated feature set; however, multi-view co training has yet to be explored in the field of miRNA prediction. By applying multi-view co-training, they leverage each view using the other to create iteratively more powerful classifiers. The significant advantage of co-training is that there is no need for collecting any new labelled data.




- Major Contribution

This work propose a new semi-supervised miRNA prediction technique that extracts maximal information from both the limited labelled miRNA data and the unlabelled data, therefore requiring very few known miRNA. They aim to not only minimize the number of labelled training exemplars required, but also to improve the performance of current prediction methods using fewer samples. In this way, they created a more efficient method for the identification of novel miRNA, particularly for species with few known miRNA, while maximizing the return on investment for costly wet-lab validation experiments. All previous methods use supervised machine learning methods, which only make use of labelled instances for classification. Semisupervised machine learning methods also make use of both labelled and unlabelled data for classification; such methods are designed to work in situations where one have a small number of known exemplars and a large body of unlabelled data. 

- Major limitation


- Your view on the research domain/topic/approach/data/solution (positive or negative)

I think the approach this paper proposed is useful and meaningful.

