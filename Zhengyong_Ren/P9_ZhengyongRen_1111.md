# Title: Lighting Design for Globally Illuminated Volume Rendering
## Link: https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=6634193&tag=1
## Publication:  
Published in: IEEE TRANSACTIONS ON VISUALIZATION AND COMPUTER GRAPHICS, VOL. 19, NO. 12, DECEMBER 2013
## Author：
Yubo Zhang, Student Member, IEEE, and Kwan-Liu Ma, Fellow, IEEE 
## paper review:
* Main picture:  
![](https://github.com/guansLab/PaperReading/blob/master/Zhengyong_Ren/Screenshot%20from%202019-11-12%2010-17-37.png)
* Research Background:  
With the evolution of graphics hardware, high quality global illumination becomes available for real-time volume rendering.
Compared to local illumination, global illumination can produce realistic shading effects which are closer to real world scenes, and has proven useful for enhancing volume data visualization to enable better depth and shape perception. 

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
