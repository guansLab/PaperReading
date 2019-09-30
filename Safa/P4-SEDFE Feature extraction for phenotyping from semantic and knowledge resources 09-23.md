
### Title: Feature extraction for phenotyping from semantic and knowledge resources 
### Publication: Journal of biomedical informatics 91 (2019): 103122.

### Author： Wenxin Ninga , Stephanie Chanb , Andrew Beamc , Ming Yua , Alon Gevad e,f , Katherine Liaog,c , Mary Mullenh,i , Kenneth D. Mandld,c , Isaac Kohanec , Tianxi Caib,c , Sheng Yuj,a,k

a Department of Industrial Engineering, Tsinghua University, Beijing, China
b Department of Biostatistics, Harvard T.H. Chan School of Public Health, Boston, MA, USA 
c Department of Biomedical Informatics, Harvard Medical School, Boston, MA, USA 
d Computational Health Informatics Program, Boston Children’s Hospital, Boston, MA, USA 
e Department of Anesthesiology, Critical Care, and Pain Medicine, Boston Children’s Hospital, Boston, MA, USA 
f Department of Anesthesia, Harvard Medical School, Boston, MA, USA 
g Department of Medicine, Division of Rheumatology, Immunology and Allergy, Brigham and Women’s Hospital, Boston, MA, USA 
h Department of Cardiology, Boston Children’s Hospital, Boston, MA, USA
i Department of Pediatrics, Harvard Medical School, Boston, MA, USA 
j Center for Statistical Science, Tsinghua University, Beijing, China
k Institute for Data Science, Tsinghua University, Beijing, China

  
### Paper Review
- Research Background

Phenotyping algorithms can efficiently and accurately identify patients with a specific disease phenotype and construct electronic health records (EHR)-based cohorts for subsequent clinical or genomic studies. Previous studies have introduced unsupervised EHR-based feature selection methods that yielded algorithms with high accuracy. However, those selection methods still require expert intervention to tweak the parameter settings according to the EHR data distribution for each phenotype. The previous EHR-driven feature selection methods AFEP and SAFE demonstrated their effectiveness in their original papers and other independent applications. Their unsupervised nature significantly speeded up the process of developing phenotyping algorithms. However, their phenotype-dependent settings that rely on the feature distribution in the EHR, such as the thresholds for creating the silver labels and the sample size from the extremes in SAFE, still require expert intervention and make them inadequate to pair with fully automated model training algorithms such as PheNorm in large-scale phenotyping efforts.



- Problem to Solve

Although previous studies have proposed efficient feature selection methods with excellent performance, they were limited by their requirement of phenotype-specific and manually specified parameters and their reliance on a large sized EHR dataset. A lack of complete automation can influence the efficiency of these methods for large-scale phenotyping. EHR-based selection can also be biased to the dataset where the selection is done, hindering the portability of the selected features for use at different hospitals, and potentially increasing the time and effort required for phenotyping. This study addressed these two limitations and achieve fully automated and EHR-independent feature selection by using distributional semantics.



- Key Design and Algorithm Proposed

Distributional semantics models the meaning (or semantics) of a term based on the term’s co-occurrence information across a text corpus under the assumption that terms with similar or related meanings tend to appear in similar contexts . The derived semantics of a term is then encoded as a numerical vector that can be used to reveal semantic closeness between terms. 

SEmantics-Driven Feature Extraction (SEDFE) collects medical concepts from online knowledge sources as candidate features and gives them vector-form distributional semantic representations derived with neural word embedding and the Unified Medical Language System Metathesaurus. A number of features that are semantically closest and that sufficiently characterize the target phenotype are determined by a linear decomposition criterion and are selected for the final classification algorithm.


- Major Contribution

This study proposed SEDFE, a novel EHR-independent method, which leverages distributional semantic representations of UMLS concepts. SEDFE performs feature selection in a semantics-driven manner. Features that semantically best characterize the target phenotype are selected for algorithm training. The results show that SEDFE yields algorithms with comparable performance to the algorithms trained with features derived from EHR-based methods. The complete automation of feature selection eliminates the need for human intervention. Moreover, this method is robust to the input concept vectors. Therefore, SEDFE provides an effective alternative to EHR-based feature selection methods, with comparable performance, better automation, and expected acceleration in developing phenotyping algorithms. The subsequent combination of SEDFE + PheNorm can achieve high-throughput phenotyping in a fully automated and unsupervised manner.


- Major limitation

One limitation of SEDFE is that performing feature selection only based on the semantic relevance between candidate features and the target phenotype tends to yield features with less diverse semantic types. This methodology is also limited in the utilization of codified EHR data. Procedures, labs, and medications are usually stored as structured data and can be probably more informative than features obtained by NLP. Another limitation of this study is the limited phenotypes for validation, in part due to the limited availability of gold-standard labels. Creating the gold-standard labels for training and validation require tremendous time for chart review by domain experts, making annotated data a scarce resource.
