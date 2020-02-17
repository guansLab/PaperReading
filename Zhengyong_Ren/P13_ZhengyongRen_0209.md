# Realtime Multi-Person 2D Pose Estimation using Part Affinity Fields ∗
## Link: https://arxiv.org/pdf/1611.08050.pdf
## Publication:  
A thesis submitted to Kent State University in partial fulfilment of the requirements for the degree of Master of Science.
## Author：
Zhe Cao, Tomas Simon, Shih-En Wei, Yaser Sheikh.
## paper review:
* Main picture:  
![](https://github.com/guansLab/PaperReading/blob/master/Zhengyong_Ren/13.png)
* Research Background:  
Human 2D pose estimation—the problem of localizing anatomical keypoints or “parts” has largely focused on
finding body parts of individuals
* Problem to Solve:  
Inferring the pose of multiple people in images, especially socially engaged individuals, presents a unique set
of challenges.
* Key Design and Algorithm Proposed:  
An approach to efficiently detect the 2D pose of multiple people in an image.
* Major Contribution:  
1,The approach uses a nonparametric representation, which we refer to as Part Affinity
Fields (PAFs), to learn to associate body parts with individuals in the image.  
2,The architecture encodes global context, allowing a greedy bottom-up parsing step that maintains high accuracy while achieving realtime performance, irrespective of the number of people in the image.   
3,The architecture is designed to jointly learn part locations and their association via two branches of the same sequential
prediction process. 
* limited  
Our photo collections just tend to capture moments of personal significance.
* Something you don’t understand:  
Part Affinity Fields for Part Association.
* Your view on the research domain/topic/approach/data/solution (positive or negative):  
This is an approach to efficiently detect the 2D pose of multiple people in an imagea, as the greedy bottom-up parsing step that maintains high accuracy while achieving realtime performance.

