# AutoWare User Manual 

## 3. Operating Autoware

- The main function operations of Autoware are described in this chapter. 

- This description assumes operating by **Runtime Manager.** 

> Please refer Chapter 4 for user inter face details.



---

![](https://gitlab.com/autowarefoundation/autoware.ai/autoware/raw/master/docs/images/autoware_overview.png)


## [Developers Guide- Overview - Detection](https://gitlab.com/autowarefoundation/autoware.ai/autoware/wikis/Overview)


- lidar_detector : 라이다에서 포인트 클라우드 데이터 입력으로 받음.  군집화(Euclidean) - 분류(DNN:VoxelNet, LMNet) 수행 `reads point cloud data from 3D laser scanners, and provides LiDAR-based object detection capabilities. The basic performance comes from the Euclidean Clustering algorithm, which finds clusters of the LiDAR scan (point cloud) above the ground. To classify the clusters, DNN-based algorithms are also supported, such as VoxelNet and LMNet.`
 - [lidar_euclidean_cluster_detect](https://gitlab.com/autowarefoundation/autoware.ai/core_perception/tree/master/lidar_euclidean_cluster_detect)
 - [CNN LiDAR Baidu Object Segmenter](https://gitlab.com/autowarefoundation/autoware.ai/core_perception/tree/master/lidar_apollo_cnn_seg_detect)
 - [Naive-L-Shape fitting](https://gitlab.com/autowarefoundation/autoware.ai/core_perception/tree/master/lidar_naive_l_shape_detect)
 - [Point Pillars for 3D Object Detection: ver. 1.0](https://gitlab.com/autowarefoundation/autoware.ai/core_perception/tree/master/lidar_point_pillars) [[논문]](Fast Encoders for Object Detection from Point Clouds)
 - [Shape Estimation](https://gitlab.com/autowarefoundation/autoware.ai/core_perception/tree/master/lidar_shape_estimation)
 


- vision_detector: 카메라에서 이미지 데이터 입력으로 받음. 분류(DNN:R-CNN, SSD, and Yolo) 수행 ` reads image data from cameras, and provides image-based object detection capabilities. The main algorithms include R-CNN, SSD, and Yolo, which are designed to perform single DNNs for real-time performance. Multiple classes of detection are supported, such as cars and passengers.`

- vision tracker : 비젼 디텍터의 결과물을 이용하여 추적 수행. 2D 이미지 평면상 수행된 추적 결과는 fusion_tool을 이용하여 3D 라이다 디텍터 결과물과 합쳐짐 `provides a tracking function for the results of vision_detector. The algorithm is based on Beyond Pixels. The results of tracking on an image plane are projected and combined with the result of lidar_detector in a 3D space through fusion_tools.`


- fusion_detector : 라이다와 카메라에서 포인트 클라우드와 이미지를 동시에 입력으로 받음. 3D 공간상 탐지 정확도를 향상 시키는데 사용됨. `reads both point cloud data from laser scanners and image data from cameras, and achieves further accurate object detection in a 3D space. The positions of laser scanner(s) and camera(s) must be calibrated in advance.`
 - The current implementation is based on the MV3D algorithm with a minor extension of the network as compared to the original algorithm.


- fusion_tools : **lidar_detector**와 **vision_tracker**의 결과를 합치는데 사용됨. **vision_detector**의 분류 결과를 **lidar_detector**의 포인트 클라우드 클러스터에 추가 시킴 `combines the results from lidar_detector and vision_tracker. The class information identified by vision_detector is added to the clusters of point cloud detected by lidar_detector.`

- object_tracker : 위 패키지의 결과물의 모션을 예측. 칼만필터와 파티클 필터 사용 `predicts the motion of objects detected and identified by the above packages. The result of tracking can be further used for prediction of the object behavior and estimation of the object velocity. The tracking algorithm is based on the Kalman Filters. Another variant supports the Particle Filters as well.`

![](https://user-images.githubusercontent.com/38030772/46925660-0393e380-d068-11e8-8b75-2f0586f20a17.png)