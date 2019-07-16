# AutoWare User Manual 

## 3. Operating Autoware

- The main function operations of Autoware are described in this chapter. 

- This description assumes operating by **Runtime Manager.** 

> Please refer Chapter 4 for user inter face details.



---


```
Detection

https://gitlab.com/autowarefoundation/autoware.ai/autoware/wikis/Overview

lidar_detector reads point cloud data from 3D laser scanners, and provides LiDAR-based object detection capabilities. The basic performance comes from the Euclidean Clustering algorithm, which finds clusters of the LiDAR scan (point cloud) above the ground. To classify the clusters, DNN-based algorithms are also supported, such as VoxelNet and LMNet.

vision_detector reads image data from cameras, and provides image-based object detection capabilities. The main algorithms include R-CNN, SSD, and Yolo, which are designed to perform single DNNs for real-time performance. Multiple classes of detection are supported, such as cars and passengers.

vision_tracker provides a tracking function for the results of vision_detector. The algorithm is based on Beyond Pixels. The results of tracking on an image plane are projected and combined with the result of lidar_detector in a 3D space through fusion_tools.

fusion_detector reads both point cloud data from laser scanners and image data from cameras, and achieves further accurate object detection in a 3D space. The positions of laser scanner(s) and camera(s) must be calibrated in advance. The current implementation is based on the MV3D algorithm with a minor extension of the network as compared to the original algorithm.

fusion_tools combines the results from lidar_detector and vision_tracker. The class information identified by vision_detector is added to the clusters of point cloud detected by lidar_detector.

object_tracker predicts the motion of objects detected and identified by the above packages. The result of tracking can be further used for prediction of the object behavior and estimation of the object velocity. The tracking algorithm is based on the Kalman Filters. Another variant supports the Particle Filters as well.
```