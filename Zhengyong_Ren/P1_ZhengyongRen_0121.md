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
Data visualization plays a crucial role in identifying interesting patterns in exploratory data analysis. Its use is, however, made difficult by the large number of possible data projections showing different attribute subsets that must be evaluated by the data analyst. 

* Problem to Solve:  
Setting up optimal lighting could be a nontrivial task for average users. There were lighting design works for volume visualization but they did not consider global light transportation. 
* Key Design and Algorithm Proposed:  
  present a lighting design method for volume visualization employing global illumination.
The resulting system takes into account view and transfer-function dependent content of the volume data to automatically generate an optimized three-point lighting environment.
 
* Major Contribution:  
1, fully exploits the back light which is not used by previous volume visualization systems.   
2, Including global shadow and multiple scattering, our lighting system can effectively enhance the depth and shape
perception of volumetric features of interest.   
3, Propose an automatic tone mapping operator which recovers visual details
from overexposed areas while maintaining sufficient contrast in the dark areas. 
* limited  
1,it may not be applied to view-independent cases because the result is
optimized for the camera view.   
2,it is not applicable in cases where more than three light sources must be used.   
3,method may not give optimal results for extremely complex datasets where point light sources are needed to illuminate internal structures that directional lights cannot reach. It does not take depth information
into account.
* Something you don’t understand:  
Iε << 1 is a configurable variable in our lighting system. Note that Iε
is a data-independent value. Once set, the system can automatically
compute the appropriate back light intensity for each case. This is
much more convenient than adjusting the back light intensity manually.
* Your view on the research domain/topic/approach/data/solution (positive or negative):  
Their lighting design method for globally illuminated volume
visualization is effective for volume datasets with complex and fine
structures.
