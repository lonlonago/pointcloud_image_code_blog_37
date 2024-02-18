>  When doing 3D deep learning, point cloud data can be obtained by using existing CAD models 

 There are several functions in the pcl library that can read the model and generate the point cloud. There are three functions under the I/O module that can load data: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574478962
  ```  
 At the same time, the tools module contains two conversion functions obj2pcd and ply2pcd, the implementation code of obj2pcd is as follows: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574478962
  ```  
 The ply2pcd code is implemented as follows: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574478962
  ```  
 If you have a depth map, you can use the camera's internal parameters to obtain point cloud data. Here is a simple algorithm (from Dominik13993) tips dataset using the PCL library: 300 household common objects at the University of Washington, Stanford 3D scanning dataset 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574478962
  ```  
>  TODO from Sharon 

 Reference: Summary of 3D Point Cloud Datasets 

 ![avatar]( 20181031181852971.) 

  icon from easyicon 

 ref: pcl:http://pointclouds.org/documentation/ pcl.cn:http://www.pclcn.org zhihu:https://www.zhihu.com/question/37577447 

