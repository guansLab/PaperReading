
### Title: A machine-learned knowledge discovery method for associating complex phenotypes with complex genotypes. Application to pain
(Lötsch, Jörn, and Alfred Ultsch. "A machine-learned knowledge discovery method for associating complex phenotypes with complex genotypes. Application to pain." Journal of biomedical informatics 46.5 (2013): 921-928.)

### Paper Link: https://www.sciencedirect.com/science/article/pii/S1532046413001111


### Publication: Journal of biomedical informatics 46.5 (2013): 921-928

### Author： Jorn Lotsch (a,b), Alfred Ultsch (c)

a pharmazentrum frankfurt/ZAFES, Institute of Clinical Pharmacology, Johann Wolfgang Goethe University Hospital, Theodor-Stern-Kai 7, D-60590 Frankfurt am Main, Germany
b Fraunhofer Institute for Molecular Biology and Applied Ecology IME, Project Group Translational Medicine and Pharmacology TMP, Theodor-Stern-Kai 7, 60596 Frankfurt am
Main, Germany
c DataBionics Research Group, University of Marburg, Hans-Meerwein-Straße, D-35032 Marburg, Germany

  
### Paper Review
- Research Background

The association of genotyping information with common traits is not satisfactorily solved. One of the most complex traits is pain and association studies have failed so far to provide reproducible predictions of pain phenotypes from genotypes in the general population despite a well-established genetic basis of pain. This work therefore aimed at developing a method able to prospectively and highly accurately predict pain phenotype from the underlying genotype. This is caused by common genetic factors reciprocally canceling out their phenotypic consequences and usually exerting only small effects. 


- Problem to Solve

One of the most challenging traits is pain because it involves a complex pathophysiology underlying its sensory, affective, motor, vegetative and emotional components reflected in the large network of underlying molecular nociceptive pathways. Approaches applied so far have failed to provide a conclusive solution to pain genotype–phenotype association problems. This is probably due to a number of methodological shortcomings. Firstly, theoretical reasons suggest that the presently used clustering techniques should be revised in favor of those that make no prior assumptions about the cluster structure, since the patterns of pain responses across different tests provide no indication of a particular cluster form. Secondly, clustering approaches used so far have been restricted to a mere description of the pattern of pain measures among individuals, without providing analyses of clinically relevant phenotypes that could be used for predictions by genotypes. Thirdly, genotype associations were mostly made in separate tests of single markers for phenotypic effects, without regard to the complexity of the genotypes.




- Key Design and Algorithm Proposed

This study aimed at developing a methodology that provides a basis of genotypes-phenotype associations in complex traits. The used data consisted of two independent data sets obtained in two independent study cohorts. The first data set, the training data, had been previously acquired from a random sample of 125 unrelated healthy young Caucasians. At this data set, the genotype–phenotype associations were established. To test their prediction, a new data set was acquired prospectively, the test dataset, which was obtained in the same laboratory, from a random sample of 89 subjects of the same ethnicity and distribution. Analyses were done using Matlab software. Besides automated clustering of complex data, the bioinformatics toolbox also contains machine learning methods for a subsequent knowledge-generation from the clustering. Data analysis started with the identification of subjects who shared similar pain sensitivities to different stimuli (i.e., heat, cold, electrical current and blunt pressure). Subsequently, extreme pain phenotype subgroups (clusters) were analyzed for the underlying complex genetic architecture. Finally, the complex genotype was used to identify those subjects from the test data set who had belonged to a similar pain subgroup. Data was z-transformed and a combined ‘‘pain’’ variable, zTotalPain, was calculated as the sum of all rescaled pain measures to model the overall sensitivity to any type of pain stimulus. This combined data was split into three classes of pain sensitivity, i.e., ‘‘low pain’’ sensitivity, ‘‘average pain’’ and ‘‘high pain’’. 
Projection and clustering pain data. This analysis focused on identifying subjects with similar pain phenotypes. The distributions of the phenotypical pain data turned out to be rather complex. These distributions could be modeled with a mixture of three Gaussians N(mi,si),i= 1, 2, 3. The theorem of Bayes allows to calculate posterior probabilities p(i|x). For the subsequent projection and clustering as measure of ‘‘similarity’’, the Euclidian distance of the Bayes (B=p(3|x)-p(1|x)) values was used. Each person’s response to the pain stimuli (n= 4 dimensions), plus the overall sensitivity score (n= 1 dimension), was treated as a point in a five-dimensional Euclidean vector space (data space).To obtain clusters in this vector space, the data was projected on to a two-dimensional plane. This space is called a map with a geographical interpretation in mind. As classical projection algorithms, such as principal component analysis or multidimensional scaling, cannot preserve complex cluster structures, the ESOM/U-matrix method was used. ESOM clustering provides a number of advantages over alternative methods, such as K-means or Ward, the most relevant one being the lack of prior assumption about the cluster structure. The ESOM/U-matrix clustering identified the subjects who had similar pain sensitivities. However, the result was still a ‘‘blackbox’’ with respect to the pattern of particular pain thresholds shared by the cluster members. Therefore, the subsequent analysis aimed at obtaining clear descriptions, in terms of pain threshold markers, of the sensitivity patterns, thus obtaining pain phenotype groups (clusters) in the training data cohort.  The cluster structure obtained with the U-matrix was interpreted by extracting the decision rules, in terms of measured stimulus intensities at the pain thresholds, from a classification and regression tree (CART) classifier that assigned each subject of the training set to a particular pain cluster.

- Major Contribution

The methodology was developed to address several shortcomings of current approaches to genotype–phenotype associations and was presently applied to the complex trait of pain. It incorporates the complexity of both pain phenotypes and pain genotypes and is able to identify subgroups of individuals with similar pain phenotypes who share genotypic markers. They show that complex genotypes allow for correct prospective identification of up to 80% of the subjects who belong to a particular pain phenotype cluster. 


- Major limitation
In this work, they mentioned that a limited set of genotypes and phenotypes was used, the intention of this analysis rather was to pursue a clear methodological focus for the identification of complex genotypes and phenotypes and their associations than to identify new genotypes as a biological explanation of the observed pain phenotypes.


- Your view on the research domain/topic/approach/data/solution (positive or negative)

I think the approach this paper proposed is useful and meaningful.

