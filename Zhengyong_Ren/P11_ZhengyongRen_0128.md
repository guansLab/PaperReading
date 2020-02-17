# Two-Stream Convolutional Networks for Action Recognition in Videos
## Link: https://papers.nips.cc/paper/5353-two-stream-convolutional-networks-for-action-recognition-in-videos.pdf
## Author：
Karen Simonyan Andrew Zisserman
## paper review:
* Main picture:  
![](https://github.com/guansLab/PaperReading/blob/master/Zhengyong_Ren/QQ%E5%9B%BE%E7%89%8720200217092406.png)
* Research Background:  
Recognition of human actions in videos is a challenging task which has received a significant amount
of attention in the research community. Compared to still image classification, the temporal component of videos 
provides an additional (and important) clue for recognition, as a number of actions can be reliably recognised 
based on the motion information. 
* Problem to Solve:  
Capture the complementary information on appearance from still frames and motion from vodios.
* Key Design and Algorithm Proposed:  
A two-stream ConvNet architecture which incorporates spatial and temporal networks.
* Major Contribution:  
1, Propose a two-stream ConvNet architecture which incorporates spatial and temporal networks.
2, Demonstrate that a ConvNet trained on multi-frame dense optical flow is able to achieve very good performance in spite of limited training data.
3, Show that multitask learning, applied to two different action classification datasets, can be used to
increase the amount of training data and improve the performance on both.
* limited  
A significant challenge on its own due to the gigantic amount of training data (multiple TBs)
* Something you don’t understand:  
The part of Optical flow ConvNets.
* Your view on the research domain/topic/approach/data/solution (positive or negative):  
Training a temporal ConvNet on optical flow  is significantly better than training on raw
stacked frames.
