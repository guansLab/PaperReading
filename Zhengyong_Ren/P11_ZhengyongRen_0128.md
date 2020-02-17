# VizRank: Data Visualization Guided by Machine Learning
## Link: https://link.springer.com/article/10.1007/s10618-005-0031-5
## Publication:  
Published in: Data Mining and Knowledge Discovery,Sepember 2006,volume 13,Isssue 2,pp 119-136.
## Author：
Gregor Leban,Blaž ZupanGaj VidmarIvan Bratko.
## paper review:
* Main picture:  
![](https://github.com/guansLab/PaperReading/blob/master/Zhengyong_Ren/Screenshot%20from%202020-01-21%2009-47-33.png)
* Research Background:  
Data visualization plays a crucial role in identifying interesting patterns in exploratory data analysis. 
* Problem to Solve:  
Made difficult by the large number of possible data projections showing different attribute subsets that must be evaluated by the data analyst. 
* Key Design and Algorithm Proposed:  
    VizRank, which is applied on classified data to automatically select the most useful data projections. VizRank can be used with any visualization method that maps attribute values to points in a two-dimensional visualization space. It assesses possible data projections and ranks them by their ability to visually discriminate between classes. The quality of class separation is estimated by computing the predictive accuracy of k-nearest neighbor classifier on the data set consisting of x and y positions of the projected data points and their class information. 
 
* Major Contribution:  
1, The solution of VizRank is to apply a machine learning method to the graphically represented data
2, k-NN is a machine learning method that predicts class value for an unlabeled example by analyzing its k neighboring examples.Vizrank used the K-NN method.
3, Presents experimental results which show that VizRank's ranking of projections highly agrees with subjective rankings by data analysts. 
* limited  
In statistical terms it is highly robust since it makes no assumptions about the probability distributions either of the original data, or in the projection space.
* Something you don’t understand:  
The Brier score of the prediction in evaluating the usefulness of a projection.
* Your view on the research domain/topic/approach/data/solution (positive or negative):  
VizRank based on the k-NN classifier, lacks the statistical inference apparatus available in LDA or projection pursuit. It is also primarily aimed for original attributes.
