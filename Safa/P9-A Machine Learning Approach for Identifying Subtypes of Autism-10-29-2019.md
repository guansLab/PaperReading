
### Title: A Machine Learning Approach for Identifying Subtypes of Autism
Guillén, Rocio, Curtis Jensen, and Stephen Edelson. "A machine learning approach for identifying subtypes of autism." Proceedings of the 1st ACM International Health Informatics Symposium. ACM, 2010.

### Publication: Proceedings of the 1st ACM International Health Informatics Symposium. ACM, 2010.


### Author： Rocio Guillén1, Curtis Jensen1, Stephen Edelson2
1 California State University San Marcos
2 Autism Research Institute
  
### Paper Review
- Research Background

Recently, the National Institute of Health (NIH) relied on a machine learning program in an attempt to categorize ASD. The researchers used the Autism Diagnostic Interview Revised (ADI-R), and their goal was to correlate genetic markers with specific subgroups. 



- Problem to Solve

They address the problem of mining the data collected by the Autism Research Institute (ARI). Using the mined data from ARI, they were able to classify subtypes of ASD.

- Key Design and Algorithm Proposed

The data mining for the ARI survey is done by applying two clustering algorithms to the ARI survey data. The first clustering algorithm is the well-known Expectation Maximization (EM) algorithm. The second is a clustering algorithm developed by them from Minimum Message Length (MML) principals applied to clustering.  The clusters produced from these two algorithms are then processed by the JRip classification algorithm. This is for the dual purpose of creating human understandable rules behind the clusters and to also create a form of validation for the discovered clusters. The EM algorithm has not been modified from its basic process as implemented in the Weka data mining tool. The MML clustering algorithm has been developed by us for Weka and for the attributes found in the ARI survey. MML can be applied in fields other than machine learning. It was originally developed as a communication model. Also, in this work there are two measures to evaluate clustering results. The first measure is simple execution time. The second measure is how accurate the algorithm is at identifying groupings in the data.


- Major Contribution

In this work they define an extensible four step approach for applying data mining and machine learning techniques to epidemiological studies. Second, they also developed an adaptation of the Minimum Message Length (MML) information theory machine learning algorithm for the Weka data mining software suite. Third, epidemiological data mining approach was used to apply their Minimum Message Length algorithm, the Expectation
Minimization algorithm, and the JRip algorithm to identify subtypes of Autism in a very large database that has been created by the Autism Research Institute. Fourth, analyzed the results of their experiments and discovered nine subtypes of Autism.

- Major limitation


- Your view on the research domain/topic/approach/data/solution (positive or negative)

I think the approach this paper proposed is useful and meaningful.

