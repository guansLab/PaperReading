
### Title: Surrogate-assisted feature extraction for high-throughput phenotyping
### Publication: Journal of the American Medical Informatics Association  24(e1), 2017, e143–e149

### Author： Sheng Yu1,2, Abhishek Chakrabortty3 ,Katherine P Liao4, Tianrun Cai5 , Ashwin N Ananthakrishnan6 , Vivian S Gainer7,Susanne E Churchill8 ,Peter Szolovits9 , Shawn N Murphy7,10 ,Isaac S Kohane8 ,and Tianxi Cai 3
 1Center  for  Statistical  Science,  Tsinghua  University,  Beijing,  China,2Department  of  Industrial  Engineering,  Tsinghua  University Beijing, China,3Department of Biostatistics, Harvard T.H. Chan School of Public Health, Boston, Massachusetts, USA,4Division of Rheumatology, Brigham and Women’s Hospital, Boston, Massachusetts, USA,5Department of Radiology, Brigham and Women’s Hospital, Boston, Massachusetts, USA,6Division of Gastroenterology, Massachusetts General Hospital, Boston, Massachusetts,USA,7Research  IS  and  Computing,  Partners  HealthCare,  Charlestown,  Massachusetts,  USA,8Department  of  Biomedical  Informatics, Harvard Medical School, Boston, Massachusetts, USA,9Computer Science and Artificial Intelligence Laboratory, Massachusetts  Institute  of  Technology,  Cambridge,  Massachusetts,  USA,  and10Department  of  Neurology,  Massachusetts  General Hospital, Boston, Massachusetts, USA

  
### Paper Review
- Research Background

Phenotyping algorithms are capable of accurately identifying patients with specific phenotypes from
within electronic medical records systems. However, developing phenotyping algorithms in a scalable way remains a challenge due to the extensive human resources required. Assigning  phenotypes based on  International  Classification  of  Diseases,  Ninth Revision, Clinical  Modification  (ICD-9)  codes  often  results  in  misclassification  and  hampers  the  power  of  hypothesis  tests  in  subsequent genomic  or  biomarker  studies.


- Problem to Solve

Yet bottlenecks still exist that limit the ability to perform high-throughput phenotyping.  To  create  a  phenotyping  algorithm,  2 important and rate-limiting steps are typically involved: collecting informative features that strongly characterize the phenotype, and developing a classification algorithm based on these features with a  gold-standard  training  set.  The most commonly used features include counts of a patient’s ICD-9 billing codes, codes of diagnostic and therapeutic procedures, medication prescriptions, and lab codes/values. In addition to the codified data, features can also be derived from the patient’s clinical narrative notes via natural language processing (NLP). The other important step (and bottleneck) in developing a phenotyping algorithm is creating gold-standard labels by domain experts via chart review. Labeling is both labor-intensive and time-consuming. The training sample sizes in previous studies typically ranged from 400 to 600 and have occasionally reached several thousand. Reviewing records for 100–200 gold-standard labels would increase the feasibility of developing algorithms for multiple phenotypes over the course of a year.


- Key Design and Algorithm Proposed

The  2  bottlenecks  described  above  signify  the  need  for  auto-mated feature selection methods that can choose a small set of informative features. Ideally, selection could be done without using any gold-standard labels to reduce overfitting, and only 100–200 gold-standard labels would be needed to train a generalizable algorithm with the selected features. The objective of this study is to develop such automated feature selection methods for high-throughput phenotyping through the use of easily available but noisy surrogates.

The proposed Surrogate-Assisted Feature Extraction (SAFE) method selects candidate features from
a pool of comprehensive medical concepts found in publicly available knowledge sources. The target phenotype’s International Classification of Diseases, Ninth Revision and natural language processing counts, acting as noisy surrogates to the gold-standard labels, are used to create silver-standard labels. Candidate features highly predictive of the silver-standard labels are selected as the final features.


- Major Contribution

SAFE introduced as a high-throughput method to efficiently curate features for EMR phenotyping algorithms, leveraging publicly available knowledge sources and a large set of unlabeled data. SAFE advances current methods by expanding the knowledge sources for collection of medical concepts and employs a majority voting step to coarsely estimate the importance of a concept. The automation in feature curation eliminates the need for domain experts to manually create a list of relevant clinical terms and for NLP experts to identify optimal concept mapping. The reduction in the size of candidate features achieved by SAFE also leads to a substantial reduction in the number of gold-standard labels needed for algorithm training. Thus, employing SAFE in the training of EMR-based phenotyping algorithms can greatly improve efficiency, allowing for high-throughput phenotyping. These types of methods will play a key role in effectively leveraging big data for precision medicine studies.

- Major limitation

Although the SAFE procedure is not expected to be overly sensitive to the choice of NLP software, generalizability to other NLP software as well as to additional phenotypes and other EMR systems warrants further research.
