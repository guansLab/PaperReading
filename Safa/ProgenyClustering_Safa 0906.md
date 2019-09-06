
### Title: Progeny Clustering: A Method to Identify Biological Phenotypes
### Publication:  Nature (International Journal of Science)     https://www.nature.com/nature-research/about


### Author：Chenyue W. Hu1, Steven M. Kornblau2, John H. Slater3 & Amina A. Qutub1 (1 Department of Bioengineering, Rice University. 2 Departments of Leukemia and Stem Cell Transplant, University of Texas MD Anderson Cancer Center.  3 Department of Biomedical Engineering, University of Delaware)

 
  
### Paper Review

- Research Background


Cluster analysis is one of the most useful unsupervised learning techniques in the era of big data, has been widely applied in biomedical research.  Biological datasets are often large, high-dimensional and noisy, and prior knowledge of the underlying distribution is usually lacking. Clustering in this case could provide key insights into the data by automatically organizing the data into groups of distinct patterns. Recent advances in systems biology and high-throughput technology, increased the need for cluster analysis in biomedical research. For example, the identification and categorization of cell phenotypes based on quantitative imaging metrics, is one of these emerging areas for applying cluster analysis.



- Problem to Solve


A major challenge in cluster analysis is finding the optimal number of clusters. Though some clustering methods are able to automatically determine the number of clusters (e.g. Self-Organizing Maps, Affinity Propagation). Most clustering algorithms (including the popular clustering methods k-means and hierarchical clustering) require input from users to specify the number of clusters. In k-means, the number of clusters needs to be given pre-clustering to initiate the algorithm, whereas in hierarchical clustering a cutoﬀ for the dendrogram needs to be specified post-clustering. Clustering is usually the most time consuming step in almost all classical clustering evaluation methods, the computation time of which increases with an increase in the sample size. For example, the complexity of k-means is O(tkN), and hierarchical clustering has complexity O(N^2logN) for average and complete linkage1, where k is the number of clusters, t is the number of iterations, and N is the sample size of the dataset. Most of the cluster number determination methods employ either distance-based or stability-based measures. Distance-based methods, such as Gap Statistics and Silhouette, evaluate the quality of clustering by measuring the within-cluster distance and the cross-cluster distance. The main assumption is that a good clustering should produce close proximity among observations within each cluster and sufficient separation between observations in diﬀerent clusters. Though distance-based approaches are easily implementable and computationally efficient, their model-dependent nature restricts their application to distance-based clustering only, and their dependence on absolute distance can hinder their eﬀectiveness when applied to high-dimensional data. Stability-based methods, such as Clest, Consensus Clustering and Model Explorer. The philosophy behind them resonates with the popular concept of Stability Selection. Assuming that observations are sampled from a fixed but unknown population, when samples are repetitively drawn from the same population, the clustering solution should not vary drastically. Instead of directly measuring cluster compactness and separation, stability-based methods evaluate how robust the clustering is against the randomness in sampling. Methods under this category were found to perform robust in practice, but they are slow to compute, considering the repetitive nature of the algorithm. The computation costs can dramatically escalate when we encounter big data, since the computational complexities of almost all clustering algorithms are dependent on the data size.



- Key Design and Algorithm Proposed


       Progeny Clustering, is a biologically inspired approach to estimate the ideal number of clusters. Progeny method is based on fundamental notions in stability analysis, especially on Levine and Domany’s approach. Levine and Domany’s approach, first assigns cluster membership to the full dataset and then validates clustering consistencies among resampled subsets. Their approach avoids selecting and applying classifiers, but is criticized for reusing the same samples for validation, which could lead to overestimation of cluster stability. Progeny Clustering method employs a novel sampling technique, Progeny Sampling, which constructs new samples out of existing ones by sampling feature independently. Progeny approach not only avoids reusing the same samples but also reduces data size for re-clustering.  Since feature independence is assumed in Progeny Sampling, caution should be given when applying the method to data with dependent features, and dimensional reduction techniques are recommended to first transform the data into orthogonal feature space. 



- Major Contribution


In contrast to traditional sampling methods that operate on the entire dataset for re_clustering, Progeny Clustering employs a new sampling approach to exploit the inherent heterogeneity of the population as well as to reduce the computation costs of the entire analysis. It samples values from each feature individually to construct new imaginary samples (Progenies) within each cluster.  The span and the density of each feature space are characteristic of each cluster and somewhat diﬀerent from that of other clusters, the Progeny Sampling allows us to assess the distinctness, homogeneity and compactness of each cluster without using the same samples and enables us to reduce the sample size for validation.

  
- Major limitation


       The Progeny Sampling method assumes that variation in one feature is independent from that in another, thus it decouples the relationship between features and easily exploits the fuzzy space around the progeny for cluster reconstruction. While this approach fits perfectly with centroid-based clustering algorithms (e.g., k-means), the coupling of Progeny Clustering with other clustering techniques or datasets that rely on inter-feature associations should proceed with caution. One potential solution to applying Progeny Clustering to datasets with dependent features is to first transform the raw data into reduced independent or orthogonal feature space using techniques such as PCA prior to the analysis.
       Other limitation of Progeny clustering is that the Current Progeny Clustering package is written in R (https://cran.r-project.org/web/packages/progenyClust/index.html)only!



- Something you don’t understand

The core steps in Progeny Clustering of the algorithm were not quite clear to me when I compare the steps with the provided figure that illustrate the core steps in Progeny Clustering. The core steps are as following, the used dataset consists of 20 samples (denoted as X) in a two-dimensional space (denoted as F1 and F2). The scheme displays the workﬂow of generating a stability score for clustering this dataset into two clusters. Five progenies (denoted as Y) were generated for each cluster. The co-occurrence matrix Q represents one of the clustering results of the mixed progenies, in which matrix entries are 1 if two progenies are in the same cluster and 0 otherwise. In both co-occurrence matrices Q and P, the true classification region containing progenies from the same initial cluster is colored pink and the false classification region containing progenies from diﬀerent initial clusters is colored light blue.  If the clustering quality is high, we would expect more 1s (Q) or higher probabilities (P) in the true classification region and more 0s (Q) or lower probabilities (P) in the false classification region.  



- Your view on the research domain/topic/approach/data/solution  (positive or negative)


Based on the provided results Progeny clustering method was shown successful when applied to two simulated datasets and robust with small sampling sizes and moderate level of noise. Demonstrated its application potential to biomedical research by applying it to two standard biological datasets (Iris dataset and Rat CNS dataset). Progeny clustering method is the only method that successfully identified the clinically meaningful partitions of patient groups in the AML RPPA dataset  
In particular, this method outperformed some of the most popular evaluation methods in the high-dimensional toy dataset and in the biological datasets. The algorithm was shown to perform at a completely diﬀerent and faster scale compared to other stability-based methods.




