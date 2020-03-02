# Multi-view Convolutional Neural Networks for 3D Shape Recognition
## Link: http://vis-www.cs.umass.edu/mvcnn/docs/su15mvcnn.pdf
## Publication:  
Published in: Data Mining and Knowledge Discovery,Sepember 2006,volume 13,Isssue 2,pp 119-136.
## Author：
Hang Su,Subhransu Maji,Evangelos Kalogerakis,Erik Learned-Miller
## paper review:
* Main picture:  
![](https://github.com/guansLab/PaperReading/blob/master/Zhengyong_Ren/16.png)
* Research Background:  
A longstanding question in computer vision concerns therepresentation  of  3D  shapes  for  recognition:   should  3Dshapes be represented with descriptors operating on theirnative 3D formats, such as voxel grid or polygon mesh, orcan they be effectively represented with view-based descrip-tors?  
* Problem to Solve:  
How to draw inferences about the three-dimensional (3D) world from two-dimensional (2D) images. 
* Key Design and Algorithm Proposed:  
 Learn to recognize 3D shapes from a collection of their rendered views on 2D images. 
* Major Contribution:  
1,Shape descriptors for 3D objects 
2,Image-based CNNs.
* limited  
Another obvious question is whether our view aggregat-ing techniques can be used for building compact and dis-criminative descriptors for real-world 3D objects from mul-tiple views, or automatically from video, rather than merelyfor 3D polygon mesh models. 
* Something you don’t understand:  
Low-rank  Mahalanobis  metric
* Your view on the research domain/topic/approach/data/solution (positive or negative):
I think this method doesn't just used for 3D polygon mesh models, it also can be used for building compact and dis-criminative descriptors for real-world 3D objects from mul-tiple views, or automatically from vidio.

