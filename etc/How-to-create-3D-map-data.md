# [How to create 3D map data?](https://gitlab.com/autowarefoundation/autoware.ai/autoware/wikis/home#how-to-create-3d-map-data)

First, you try creating small-scale 3D map data for private area testing, using the NDT mapping node provided by Autoware or using the [Autoware Tools](https://tools.tier4.jp/) (paid service). 

Once it goes well, you can contact a professional mapping company in your region to create large-scale 3D map data for public road testing. 
- Examples of the mapping companies include [Aisan Technology](http://www.aisantec.co.jp/english/) and [Mandli](https://www.mandli.com/). 

- Note that the NDT mapping node and the Autoware Tools are designed for closed environments, thus not suitable for creating large-scale 3D map data.




---

# [Autoware Tools](https://tools.tier4.jp/)

## 1. Vector Map 

Vector Map Builder is a tool that helps to create a vector map from point cloud data, which is compatible to ADAS Map. 

The vector map represents a set of features inherent to the road, such as lanes, stop lines, traffic lights, and intersections. 

These pieces of information are particularly leveraged by Autoware to enhance capabilities of path planning, object detection, traffic light recognition, and other critical tasks.







## 2. Point Cloud Map 

Point Cloud Map Builder is a tool that eases building a 3D point cloud map. Using as input a previously recorded ROSBAG file that may include range information captured by a LiDAR sensor, Point Cloud Map Builder will generate the file as output that contains a 3D point cloud map. The file formats based on PCD (Point Cloud Data), which is a standard format provided by PCL (Point Cloud Library). The generated map can be used, for instance, to localize a self-driving vehicle in the region captured.