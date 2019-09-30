
### Title: Large-Scale Automatic Feature Selection for Biomarker Discovery in High-Dimensional OMICs Data


### Publication: Frontiers in genetics 10 (2019): 452

### Author： Mickael Leclercq1,2 *, Benjamin Vittrant 1,2, Marie Laure Martin-Magniette3,4 , Marie Pier Scott Boyer 1,2, Olivier Perin5 , Alain Bergeron1,6, Yves Fradet 1,6 and Arnaud Droit 1,2 * † 

1 Centre de Recherche du CHU de Québec–Université Laval, Québec City, QC, Canada,
2 Département de Médecine Moléculaire, Université Laval, Québec City, QC, Canada, 
3 Institute of Plant Sciences Paris Saclay IPS2, CNRS, INRA, Université Paris-Sud, Université Evry, Université Paris-Saclay, Paris Diderot, Sorbonne Paris-Cité, Orsay, France, 
4 UMR MIA-Paris, AgroParisTech, INRA, Université Paris-Saclay, Paris, France, 
5 Digital Sciences Department, L’Oréal Advanced Research, Aulnay-sous-bois, France, 
6 Département de Chirurgie, Oncology Axis, Université Laval, Québec City, QC, Canada

  
### Paper Review
- Research Background

The identification of biomarker signatures in omics molecular profiling is usually performed to predict outcomes in a precision medicine context, such as patient disease susceptibility, diagnosis, prognosis, and treatment response. Research studies involving cohorts of patients aim to discover patterns that establish risk stratification and discriminate patient states, such as diseased vs. controls, disease type, etc. These last years, clinical and biology research turned toward extensive usage of OMICs (i.e., proteomics, transcriptomics, metabolomics, genomics, etc.) technologies, which include microarrays, mass spectrometry, and whole exome/genome and RNA sequencing. Specific patterns associated with a clinical outcome of interest (e.g., disease diagnostic, prognostic), called biomarker signatures, can be derived from these high-dimensional technologies outputs (e.g., gene expression, polymorphisms).




- Problem to Solve

Biomarker signature identification from disease-derived omics datasets is a challenging task involving many pitfalls. First, the datasets are generally highly unbalanced, where the features (e.g., genes, peptides, metabolites), also called attributes or variables, largely outnumber the samples. In addition, patients are unequally distributed among measured outcomes. Second, the molecular profiles are often heterogeneous (e.g., sub phenotypes in cancer data), of diverse types (e.g., categorical, continuous), and scattered over multiple inputs. To identify sets of predictive biomarker signatures from omics data, a few non-commercial methods have been implemented in R packages. These toolkits have adopted diverse multivariate projection based methods including principal component analysis, independent component analysis, multi-group partial least squares regression, canonical correlation analysis, K-means clustering, and associated visualizations. Recently, other research teams have proposed approaches in machine learning (ML), a branch of artificial intelligence that holds a great potential for pattern recognition in complex diseases datasets. ML has already shown its ability to identify key features (markers) and modeling predictive biomarker signature in a variety of fields, including cancer research, immunology, skin diseases, etc. However, all these techniques are complex to use and are out-of-reach for non-programmers and non-ML experts. Furthermore, the software implemented specifically for omics data are still rare and are strictly limited to specific ML algorithms for feature selection (also called “attribute selection”) or classification. Hence, there is an unmet need to develop user-friendly computational approaches for using machine learning in a biomedical context that are dedicated to biologists and clinical researchers. These approaches must be able to identify complex patterns and predict outcomes in various biological or clinical fields (e.g., disease diagnosis, prognosis, therapeutics), thus helping to understand the biology behind a measured outcome


- Key Design and Algorithm Proposed

BioDiscML pipeline works as follows: It starts with the preprocessing section. After merging the input datasets when many are submitted, a first sampling step separates the data in a train and a test set (2/3 and 1/3, respectively, by default), this latter will be used after model creation to assess non-overfitting. Then, a feature ranking algorithm sorts the features based on their predictive power with respect to the class. Only the first best 1,000 s features are kept by default. Then, in the feature selection section, for each machine learning algorithm defined in BioDiscML (i.e., the classifiers), and for each optimization evaluation criterion (i.e., a chosen evaluation metric), two types of feature search selection are performed: top k features and stepwise. Top k simply select the best k elements from the ordered feature set to create a model. In the stepwise approaches, for each element in the ordered set, features are added and/or removed one by one depending on the feature search method. At each iteration, the created model is evaluated by 10-fold cross validation (10 CV) and the combination of selected features is retained if the predictive performance is improved. 

When all features are tested and the signature is identified, the model is evaluated on other cross-validation/sampling procedures. Once all classifiers are tested, they end with a set of feature optimized models with their associated performances metrics and associated features, for each model. In total, about 8,500 models for classification and about 1,800 for regression are tested, but a large part will not be computed because of non-supported data. Once all models are generated, the program executes the best model(s) selection section. The average performance among some computed metrics are used to estimate the most efficient model, and correlated features are retrieved from the original dataset and compiled in a tabular-separated text file report. Depending computing performances and dataset size, a few hours may be needed for BioDiscML pipeline to finish. Before the end of BioDiscML execution, a user can execute at any time BioDiscML from the checkpoint in parallel to perform the best model selection process, which will retrieve models from the feature optimized model list generated and updated in real-time.


- Major Contribution

Considering the complexity of the ML approach, this paper present a software called BioDiscML (Biomarker Discovery by Machine Learning), which aims to greatly facilitate the work required for biomarker signature identification from high dimensional data, such as gene expression, by automating the ML approach.

Some non-commercial automatic software already exists to facilitate the choice of learning algorithms and perform hyper-parameter optimization, such as Auto-weka, auto-Sklearn, autoML, and preconfigured pipelines in Orange canvas. But they are not explicitly designed to answer biological problems, lack of user-friendly experience for non-ML experts, some focusing only on hyperparameter optimization, and may be complex to parallelize to decrease calculation time. 

To fill the gap, providing BioDiscML the capacity to test large number of feature subsets and models in order to obtain the most performant signature to predict a measured outcome. BioDiscML uses an exhaustive search approach, which systematically enumerates a pre-defined set of possible candidates for a solution and test whether each candidate satisfies the problem statement. BioDiscML can also merge files from different sources, search for the most predictive combination of feature subsets and machine learning classifiers, train a model, evaluate predictive performances, parallelize the computation, and search for correlated features. 

- Major limitation

A reasonable number of instances (i.e. Samples) should be provided to BioDiscML. In case of very limited instances, it is expected to obtain models with low performances.
