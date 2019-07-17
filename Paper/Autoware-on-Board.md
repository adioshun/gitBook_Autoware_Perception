# [Autoware on Board: Enabling Autonomous Vehicles with Embedded Systems](https://dl.acm.org/citation.cfm?id=3207930)

>  S. Kato, S. Tokunaga, Y. Maruyama, S. Maeda, M. Hirabayashi, Y. Kitsukawa, A. Monrroy, T. Ando, Y. Fujii, and T. Azumi,``[Autoware on Board: Enabling Autonomous Vehicles with Embedded Systems](https://dl.acm.org/citation.cfm?id=3207930),'' In Proceedings of the 9th ACM/IEEE International Conference on Cyber-Physical Systems (ICCPS2018), pp. 287-296, 2018. Link



## 3. Autoware 


### 3.1 Sensing


### 3.2 Computing


#### 3.2.1 Perception 


##### Localization 



##### Detection 



Autonomous vehicles must detect the surrounding objects, such as other vehicles, pedestrians, and traffic signals. Having this information readily available, we can follow traffic rules and avoid accidents. Autoware supports deep learning [14], [15] and traditional machine learning approaches [16] for object detection using Caffe and OpenCV. Figure 4 (c) shows the application of the Single Shot MultiBox Detector (SSD) [14] and the You only look once (Yolo2) algorithms [15]. Both are based on fully convolutional neural networks (CNN) architectures designed to provide fast computation. As previously mentioned, Autoware also includes a pattern recognition algorithm based on the Deformable Part Models (DPM) [16], which searches and scores the histogram of oriented gradients features of target objects in 2D images [17]. Perception in Autoware is mainly performed using point cloud data obtained from LiDAR scanners. The point cloud is pre-processed and segmented using the nearest neighbors algorithm [18]. This process calculates the Euclidean distance between points according to a distance threshold in 3D space. Once the point cloud is clustered, the distance between surrounding objects and the ego-vehicle can be calculated. Moreover, using the distance of each cluster in conjunction with the classified 2D image processing algorithms, objects can be tracked on a time to improve the perception information. Assuming that localization in a 3D map is precise, Autoware implements an elegant scheme for traffic light recognition. Knowing the current position of the ego-vehicle in a map, and having an extrinsically and intrinsically calibrated camera and LiDAR scanner, the 3D map features can be projected to the image captured by the front camera of the vehicle, with the body rigid transformations across the camera, the LiDAR scanner, and the 3D map. Using this strategy, the region of interest (ROI) for traffic lights can be limited, reducing the computation time and increasing the accuracy of the traffic light state classifiers at the same time. Figures 4 (f) and (g) depict the result of this approach. In general, traffic light recognition is considered to be one of the most difficult problems associated with autonomous vehicles. Nonetheless, Autoware is able to accurately recognize traffic lights using 3D map features and a highlyreliable localization algorithm.