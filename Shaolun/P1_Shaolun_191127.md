Paper Reading Note
===
>Date：11/27/2019  
Author: Shaolun
***

Title: *Supporting a Visualization Application on a Self-Adapting Grid Middleware*
---
One of previous works Pro.Shen participated in.

Publication: *2008 IEEE International Symposium on Parallel and Distributed Processing*
---
Hold in Miami, FL, 2008.

Author: *Liang Chen, HanWei Shen, Gagan Agrawal*
---

  
Paper Review
---
#### Research Background
Scientific simulations and increasing numbers of high precision data collection instruments (e.g. sensors attached to satellites and medical imaging modalities) are generating data continuously, and at a high rate. In the stream model of processing, data arrives continuously and needs to be processed in real-time. **The processing rate must match the arrival rate.** As a result, often the data can be transmitted faster than it can be stored or accessed from disks within a cluster.



#### Problem to Solve
Although the speed of volume rendering has significantly increased in the past several years, the size of an average volumetric data set also continues to grow. A more challenging problem arises in the scenarios where volume data arrives in continuous streams. To observe and analyze significant features of such volume data, scientists usually need to interactively visualize them in real-time.(An example of such applications is rendering tissue volumes obtained from clinical instruments in real-time to aid a surgery.) Because visualization operations are compute-intensive, supporting real-time rendering can be very challenging. To ensure quick response while still maintain good image quality, volume rendering algorithms running in a distributed environment need to be highly adaptive.

#### Key Design and Algorithm Proposed
* **Rendering Step 1**：This rendering algorithm comprises two steps. The first step builds a hierarchical volume structure called *octree*,which is a multi-resolution representation for a volume. 

* **Rendering Step 2**: 
The second step uses octrees and volume data to render images. Traversing an octree enables a volume to be rendered in different resolutions. The higher resolution, the better image quality while the slower rendering speed.

The whole middleware is based on these two rendering steps based on a Java vitual machine, which is called *liboctree.so* and *librendering.so* respectively.

#### Major Contribution
GATES (Grid-based AdapTive Execution on Streams) is a middleware that supports the flexible and adaptive analysis of distributed data streams. This approach describes 1)how to use the **GATES**(*Grid-based AdapTive Execution on Streams*) middleware to implement a volume rendering application. 2) The algorithm of this middleware addressed the rendering where volume data arrives in continuous streams (*Because visualization operations are compute-intensive, supporting real-time rendering can be very challenging*) 3)It can enable an application to achieve the best accuracy, while maintaining the real-time constraint.

This paper addresses several challenges in developing a real-time implementation of **volume rendering** for a **distributed environment**, and show how to use **grid-based** **self-adapting** middleware, and how to expose **adaptation parameters**[^footnote].
[^footnote]: The middleware allows the application developers to expose one or more adaptation parameters. An adaptation parameter is a tunable parameter whose value can be modified to increase the processing rate, and in most cases, reduce the accuracy of the processing.

GATES middleware has three features: 1)It supports distributed processing of one or more data streams, by facilitating applications that comprise a set of stages. (For analyzing more than one data stream, at least two stages are required.) 2)It flexibly achieves the best accuracy that is possible while maintaining the real-time constraint on the analysis.3)Enable easy deployment of the application. The system is responsible for initiating the different stages of the computation at heterogeneous remote resources. The system also allows the use of existing grid infrastructure.

All in all, this kind of approach shows how they have used GATES middleware to implement a distributed and self-adapting volume rendering application. A challenge in supporting such an application on streaming data is to balance visualization quality and speed of processing. It is shown how this can be automatically done by the middleware. The group has used two different adaptation parameters, which are error-tolerance and size of the image. The experiments have shown that self-adaptation algorithm is able to converge to proper values of both the adaptation parameters, for different data stream arrival rates. At the same time, it is not sensitive to initial values of the adaptation parameters.
  
#### Major limitation
Not mentioned

  

#### Something you don’t understand
* In the Experiment 1, it is shown that a sudden drop of image size under 100 Kbps really exists at 2 rounds of the experiment. What happened in that round and what contributes to this?
* The image size of the sample they used is a little bit small(128\*128, 256\*256, 512\*512), and the reality is the image is larger than it based on big scientific data size to display the details clearly. What if the middleware algorithm handles a larger image instead of the experiment images in the study?

  

#### Your view on the research domain/topic/approach/data/solution  (positive or negative)
This rearch is such a novel tech on addressing the in-balance between visualization quality and speed of processing. It is useful for sci-vis researchers and improved a lot comparing with the previous work Pro.Shen participated in(L.Chen and G.Agrawal. Supporting self-adaptation in streaming data mining applications. In Proceedings of IEEE International Parallel & Distributed Processing Symposium(IPDPS), April 2006.) via the Grid-based approach to handle the in-balance above. The thought and expriment result is terrific. Look forward to the implement in real scientific volume rendering work. 

