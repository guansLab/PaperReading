# Title: Virtual interaction and visualisation of 3D medical imaging data with VTK and Unity
## Link: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6372083/
## Publication:  
Healthc Technol Lett. 2018 Oct; 5(5): 148–153.
Published online 2018 Sep 21. doi: 10.1049/htl.2018.5064
## Author：
Gavin Wheeler,Shujie Deng,Nicolas Toussaint,Kuberan Pushparajah, Julia A. Schnabel,John M. Simpson,and Alberto Gomez
## paper review:
* Main picture:  
![](https://github.com/guansLab/PaperReading/blob/master/Zhengyong_Ren/Screenshot%20from%202019-10-28%2000-36-25.png)
* Research Background:  
Medical imaging is an invaluable tool in diagnosis and treatment planning. Volumetric images are available from different modalities.The most widespread AR and VR development environment is Unity.
* Problem to Solve:  
However, native Unity visualisation capabilities for medical images are somewhat limited to surface rendering of mesh models.

* Key Design and Algorithm Proposed:  
A method to interconnect the Visualisation Toolkit (VTK) and Unity.
* Major Contribution:  
1, Successfully integrated VTK volume rendering into Unity. 
2,Our method allows opaque surface rendered polygonal objects to be mixed with a VTK volume render. Interactive rendering rates can be achieved.
3,Our method can achieve ‘what you see in VTK is what you get in Unity’, with improvements of performance and implementation efficiency. 

* Limitations:  
1,Further improvements is needed in the performance of our software prototype. For this improvement work we will use more sophisticated tools for performance analysis.
2,Support for platforms more mobile than our existing desktop Windows/x86 implementation just an interesting possibilities.

* Something you don’t understand:  
Architecture linking Unity events to VTK functionality via the plugin.
* Your view on the research domain/topic/approach/data/solution (positive or negative):  
The render image looks good, But I think this method needs take more cost to the render quality. 
