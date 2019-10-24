# Title: Medical Image Reconstruction Based on ITK and VTK
## Link: https://ieeexplore.ieee.org/document/6835682
## Publication:2013 International Conference on Computer Sciences and Applications
## Author：
Hui Dong
Sch. of Electr. & Inf. Eng., Xihua Univ., Chengdu, China
Ling Xia
Sch. of Electr. & Inf. Eng., Xihua Univ., Chengdu, China
Jin Zhang
Sch. of Electr. & Inf. Eng., Xihua Univ., Chengdu, China
Andong Cai
Sch. of Electr. & Inf. Eng., Xihua Univ., Chengdu, China
## paper review:
* Main picture:  
![](https://github.com/guansLab/PaperReading/blob/master/Zhengyong_Ren/Screenshot%20from%202019-10-24%2013-16-19.png)
* Research Background:  
Three-dimensional reconstruction of medical images can provide the direct, real sense for doctors and play an important role in clinical medicine.
The medical images can be reconstructed by using the VTK (visualization toolkit). 
* Problem to Solve:  
With the development of medical imaging and computer technology, the clinical medicine has a great change. 
A doctor can easily obtain the two dimensional images of their patients by the technology of ultrasonic image, 
the MRI, the CT, and so on. But the two dimensional pictures can only display the certain layer information 
of the three dimension slicer and are not direct. 

* Key Design and Algorithm Proposed:  
The 3D-visualization system based on ITK Surface Extraction

* Major Contribution:  
ITK can easily perform medical image processing, for example, image enhancement, image segmentation and image registration. 
VTK can conveniently display the outcome of the reconstruction. 
The experiments proved that it is a convenient way to integrate ITK and VTK to reconstruct the medical image.

* Limitations:  
1,it's still a difficult problem how to choose the different thresholds of different format medical files and different organs. 
2,ITK only provides a way to extract the surface of the DICOM series, and the serviceability is poor. 
3,They did not add the acceleration algorithms, the reconstruction time is a little long

* Something you don’t understand:  
How to change the DICOM Files data to a VTK data.
* Your view on the research domain/topic/approach/data/solution (positive or negative):  
The experiment results demonstrate that the 3D-visualization system based on ITK Surface Extraction is efficiency and satisfy practical applications.
