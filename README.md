##  3D point cloud data annotation 

 There should be a lot of students who have just started to come into contact with 3D deep learning, have been arranged to label data work, find the right way to label is a very difficult thing, bloggers in the search for marking tools, almost tried all the current marking tools, such as the current more popular PCAT_Open_Source, Semantic-Segmentation-Editor, such software is excellent but there are some drawbacks, such as complex installation steps, the use of vague, for the new entry of scientific research Xiaobai is extremely unfriendly, Lidar360 contains a rich set of point cloud data processing tools, but can not be used for point cloud accurate labeling, there are some other not very mainstream labeling tools, but also almost all in the installation can not be used for labeling state. After comparison, CloudCompare was selected as the final labeling tool. The installation method is simple, the labeling process is clear, and the visual effect after labeling is intuitive. The following is a labeling tutorial written by the blogger, which has tried to prompt all the difficulties you may encounter. Please pay attention to the details and read the entire labeling tutorial before labeling to avoid mistakes. Scientific research is a delicate job, and so is labeling! 

##  Labeling tools 

 CloudCompare2.9.0 

 Download link: https://pan.baidu.com/s/1sjnu3pHXu-3vaRaK1LC8-g 

 Tutorial: https://blog.csdn.net/datase/article/details/79797795 

##  Labels 

##  III. Labeling steps 

 ![avatar]( 20200127090841292.png) 

 ![avatar]( 20200127091326778.png) 

 Check and click Data (in blue), if you don't click, you will not be able to box: Edit- > Segment Select the local area to be marked (green box): 

 ![avatar]( 20200127091342965.png) 

  Click the Segment in button at the top right to get the labeled area: 

 ![avatar]( 20200127091402841.png) 

 Click the Confirm Segmentation button to save: 

 ![avatar]( 2020012709141951.png) 

 The directory will have one more line of data for the part just cut: 

 ![avatar]( 20200127091423314.png) 

 Cancel the check of the original data, single-select the point cloud data of the cutting part, and the interface will only display the cutting part: 

 ![avatar]( 20200127091445633.png) 

 Toolbar operation: Edit - > Scalar fields - > Add constant SF input label: 

 ![avatar]( 20200127091613997.png) 

  If the labelid of the building is 4, fill in 4: 

 ![avatar]( 20200127091626636.png) 

  Click OK, and observe that the Count value under Scalar Fields becomes 7 (Count represents the number of scalars in the data, and the initial value of this data is 6. The following examples are based on 6. The actual situation refers to its own data set, and the initial value of each data is different.), and the marked buildings become blue: 

 ![avatar]( 20200127091642989.png) 

 ![avatar]( 20200127091658375.png) 

  Check All data to observe the display effect of the marked part in all data: this time the label is over. 

 To make a second annotation, just tick the unmarked data, not the already marked data, to prevent repeated annotations. It can be observed that the marked data is not displayed. 

 ![avatar]( 20200127091741540.png) 

 The Count value under the unlabeled data Scalar Fields must be 6 (the Count value of each data is different, here 6 is used as a benchmark for the initial Count), if not 6, consider whether in the process of annotation of the framed data, the unframed data part is also checked. Solution: Select the unlabeled data, Edit - > Scalar fields - > Delete, and the Count of Scalar fields will change from 7 to the initial 6. 

 ![avatar]( 20200127091824909.png) 

  Repeat the 3.2 operation, frame the road surface, and get the following figure: 

 ![avatar]( 20200127091837111.png) 

  Repeat the 3.3 operation to mark the road surface. Note that just tick the data corresponding to the road surface and click: 

 ![avatar]( 20200127091919667.png) 

 ![avatar]( 20200127091931461.png) 

 ![avatar]( 20200127091944970.png) 

 ![avatar]( 20200127091950925.png) 

 ![avatar]( 20200127092013634.png) 

 ![avatar]( 20200127092027982.png) 

  After labeling, it is observed that: Check all the data, and you can find that the data of different labels will be displayed in different colors: Here, only the data of two labels can be combined and displayed, and 3.2 and 3.3 operations can be performed multiple times before merging: Click the Merge Multiple clouds button to merge: Get a data: Here, you can find that there is an error in the labeling of the building part. The solution refers to Part 5. It is recommended to ensure that each category of data annotation is accurate before merging different categories of data to avoid adding excess work. 

 ![avatar]( 2020012709222786.png) 

 ![avatar]( 20200127092241513.png) 

 The software may suddenly crash, so after marking for a period of time, pay attention to save, select all Ctrl keys, and click the save button. Save type ASCII: Get the above two pieces of data: 

 ![avatar]( 2020012709230774.png) 

 ![avatar]( 2020012709232087.png) 

 ![avatar]( 20200127092329952.png) 

  The last column in Notepad is labeled: Re-import these two data: Select the data that has been annotated, set Colors to Scalar field, and set Active to #7 to observe the display results of the data with different labels. 

 ![avatar]( 20200127092347115.png) 

  Repeat the above steps until all the data annotations are completed and merged into one data. 

 The data might be as shown in the image above, with Colors set to the Scalar field and Active set to #7. 

##  IV. Label the video 

 Link: https://pan.baidu.com/s/1qs9UPtXP0r7E6Z9m2F9A7g Extraction code: vygu 

##  Fives. Error resolution 

 Mark a tree, but the lawn section at the bottom of the tree is also selected. 

 ![avatar]( 20200127102602539.png) 

 ![avatar]( 20200127102608588.png) 

  Follow step 3.2 to cut out the lawn section at the bottom of the tree to obtain:  

 Delete the wrong label information in the lawn section Edit - > Scalar fields - > Delete, the Count of Scalar fields is changed from 7 to the initial 6: 

 ![avatar]( 20200127102614857.png) 

 ![avatar]( 20200127102621726.png) 

 ![avatar]( 20200127102629702.png) 

  Re-label the lawn part and repeat the labeling step 3.3: The lawn belongs to others, enter 0: It is observed that the label has been distinguished: 

 ![avatar]( 20200127102635345.png) 

##  VI. Precautions 

##  VII. Visualization 

 ![avatar]( 2020012710341533.png) 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

##  1. Overview of the principle 

   The registration accuracy of the point cloud adopts the root mean square error RMSE. The smaller the root mean square error, the higher the registration accuracy; the degree of overlap is to calculate the proportion of the nearest neighbor pairs to all points. The larger the degree of overlap, the better the registration effect. See the algorithm source code for the specific calculation process. 

##  2. Algorithm source code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574413623
  ```  
##  3. Main functions 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574413623
  ```  
 This function is used to evaluate the registration between point clouds. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574413623
  ```  
#  III. Display of results 

 ![avatar]( 7a1da8b127f349eab23b68c6bcbeda45.png) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574413623
  ```  


--------------------------------------------------------------------------------

#  Vector operation 

##   1. Vector inner product 

   For non-zero vectors, the inner product of vectors is: the inner product can describe the projection relationship between vectors. 

 main function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574468499
  ```  
 or 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574468499
  ```  
   Dot () calculates the matrix product for two-dimensional arrays, and the inner product for one-dimensional arrays. 

##   2. Vector outer product 

   For non-zero vectors, the vector outer product is: the direction of the outer product is perpendicular to the two vectors, and it is the directed area of the quadrilateral formed by the two vectors. The outer product is defined only for three-dimensional vectors. 

 main function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574468499
  ```  
   Outer () only calculates a one-dimensional array. If a multi-dimensional array is passed, the array is flattened to a one-dimensional array before calculation. It calculates the matrix product of column vectors and row vectors. 

##   3. Vector norm 

   There are several vector norms commonly used for vectors: the -norm: the largest of the absolute values of all elements in the vector, the -norm: the smallest of the absolute values of all elements in the vector, the -norm: the sum of the absolute values of the elements in the vector, the -norm (Euclidean norm): the square root of the sum of squares of each element in the vector, the -norm (Euclidean norm): the power of the sum of each element in the vector, 

 main function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574468499
  ```  
##   4. Vector angle 

 For vectors, the angle between vectors is: Note: (1) when = 1, in the same direction as; (2) when = -1, in the opposite direction; (3) when = 0,; (4) The value range of the angle between the vector and is:. 

   From the definition of vector inner product and outer product, the angle of the vector can also be calculated by the following formula: in the point cloud, the normal vector usually needs to be oriented after calculating the normal vector. When the normal vector is not oriented, the formula for calculating the angle of the normal vector is as follows: 

##   5. References 

>  WANG Fei, LIU Rufei, Ren Hongwei, Chai Yongning. Multi-phase vehicle laser point cloud registration using road target features [J]. Journal of Surveying and Mapping Science and Technology, 2020, 37 (05): 496-502. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574468499
  ```  
#  III. Related Links 

 [1] 标量、向量、矩阵、张量之间的区别和联系 [2] Open3D 计算点云法向量并显示 

#  C++ code 

 PCL Calculation of Angle of Point Cloud normal vector 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

##  1. Calculation process 

 After PCA decomposition, the ratio of the largest eigenvalue to the second minus the third eigenvalue can be regarded as the planarity of the current point cloud

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574426835
  ```  
#  III. Display of results 

 ![avatar]( 5aec416e370f41a995e3604a79313e13.png) 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

   See: Axial Angle Representation of Point Cloud Rotation and Rodriguez Formula 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574461995
  ```  
#  III. Display of results 

 ![avatar]( 98d56127d1ac47109bdfc1efb08a23ba.png) 

#  IV. Experimental data 

 Link: https://pan.baidu.com/s/1nxNQbMEdg5kiyZFt2a-Hew Extraction code: fgl8 



--------------------------------------------------------------------------------

#  First, the basic characteristics and description of point clouds 

 Calculate the eigenvalue and eigenvector of each point by radius search

   Let the feature value of the point cloud be: feature vector, then the point cloud has the following basic characteristics:    

 Linear: 

    Planarity: 

     Sphericity (divergence): 

    Total variance: 

    Anisotropy: 

    Characteristic entropy: 

    Trace: 

    Curvature change: 

  ![avatar]( dianyuntezheng.png) 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574432386
  ```  
#  III. Display of results 

 ![avatar]( 20210604201406465.png) 

#  IV. Reference link 

 [1] 三维点云处理：4作业：主成分分析+平面法向量估计 [2] 基于三维点云数据的主成分分析方法（PCA）的python实现 [3] PCA降维、法向量估计、点云体素及FPS滤波 [4] 三维点云 PCA(上) [5] 三维点云：PCA（下）open3d 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

##  1. Algorithm overview 

    Fleishman et al. proposed a grid bilateral filter. The bilateral filter was first applied to grey release images. The algorithm not only considers the distance from the point to the neighborhood point, but also uses the distance along the normal direction as the basis for judgment. In addition, the algorithm has no restrictions on the normal direction. The bilateral filter is applied to the point cloud data. For a certain point in the middle, first use the point within the neighborhood range of the point to calculate the unit normal vector of the point, and then the position of the point is updated by the equation. In the formula, it is the new point after the measurement point has been filtered bilaterally; it is the weight factor of the bilateral filter. In the formula, it is the unit normal vector of the near-neighborhood point of the measurement point; it is the Gaussian kernel function that is the standard deviation, that is, the two Gaussian weights in the point cloud bilateral filtering algorithm. Among them is the influence factor of the distance from the measurement point to its near-neighborhood point on the point, but the influence factor of the distance vector from the measurement point to its near-neighborhood point projected on the normal vector of the point on the measurement point; it is the spatial domain weight, which controls the smoothness degree; it is the feature domain weight, which can capture the change of the normal between neighborhood points, thereby controlling the feature retention degree. 

 ![avatar]( 20210613083258295.png) 

    As can be seen from Figure 1, the weight of the neighborhood point distance will be balanced by the weight of the normal direction, which is conducive to bringing the target point close to the tangent plane. The normal is obtained by computing the least squares regression plane of the neighborhood points, which is calculated from the average value of the neighborhood points and the covariance matrix.  

##  2. Calculation steps 

 Bilateral filtering calculation steps based on normal: input: a certain point, neighborhood radius, two Gaussian weights, output: denoising point 

 Therefore, the position of the point cloud after bilateral filtering based on normal will change, and the number of points will remain unchanged. 

##  3. References 

>  [1] Digne J, Franchis C D. The Bilateral Filter for Point Clouds [J]. Image Processing On Line, 2017, 7:278-287. [2] Yuan Zhicong. Research on point cloud registration method based on Harris feature [D]. Donghua University of Technology, 2019. [3] Liu Chuncheng. Column target change detection based on point cloud data [D]. Beijing University of Civil Engineering and Architecture, 2018.p43-44 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957447841
  ```  
#  III. Display of results 

     Data and parameters are from IPOL Journal · Image Processing On Line. 

##  1. Primitive point cloud 

 ![avatar]( 96c5ee93f9914a959768612a061c4335.png) 

##  2. Filtering results 

 ![avatar]( b5e49739bc154c9383d666a63c93e880.png) 

#  IV. Relevant links 

 [1] PCL 双边滤波 [2] PCL 基于强度的双边滤波 



--------------------------------------------------------------------------------

#  Binocular 3D reconstruction system (binocular calibration + stereo correction + binocular ranging + point cloud display) Python 

 1. Project structure 

 2. Environment 

 3. Binocular camera calibration and calibration 

 (0) Binocular camera 

 (1) Acquire left and right views of the calibration plate 

 (2) Monocular camera calibration and calibration (do not skip this step) 

 (3) Binocular camera calibration and calibration 

 (4) About MATLAB binocular calibration results 

 4. Parallax and depth maps 

 (1) Stereo correction 

 (2) Stereo matching and disparity map calculation 

 (3) Demo effect 

 5. Binocular ranging 

 6. Error description of binocular ranging 

 7. 3D point cloud display 

 8. Sample Code Demo 

 9. Binocular 3D reconstruction project code (Python version) 

 10. Binocular 3D reconstruction project code (C++ version) 

 11. Binocular 3D reconstruction project code (Android version) 

 This blog will implement the Python version of the binocular 3D reconstruction system, and the knowledge points included in the project code implementation. Due to space limitations, this blog will not go into too much detail about the algorithm principles, but will teach you how to build your own binocular 3D reconstruction system. The project code includes: 

 Sure, there are a lot of dual ranging codes on the Internet, but the projects are not very complete, and the recovery disparity map effect is also average, making it difficult to achieve commercial practical applications. The main reasons are as follows: 

 [Respect the original, please indicate the source when reprinting]: https://blog.csdn.net/guyuealian/article/details/121301896 

 [Binocular 3D reconstruction system (binocular calibration + stereo correction + binocular ranging + point cloud display) Python source code 

 Let's take a look at the renderings of binocular ranging (click the mouse on the image to get its depth distance): 

 ![avatar]( aa5d7c6543724d0d91f1cc7b3c2c2e6e.gif) 

  In 3D reconstruction, in addition to binocular cameras, there are also TOF and structured light 3D cameras 

>  Time of flight (TOF), on behalf of the company Microsoft Kinect2, PMD, SoftKinect, Lenovo Phab, in mobile phones generally used for 3D modeling, AR applications, AR ranging (Huawei TOF lens) binocular vision (Stereo Camera), on behalf of the company Leap Motion, ZED, DJI; structured light (Structured-light), on behalf of the company has Obi Zhongguang, Apple iPhone X (Prime Sense), Microsoft Kinect1, Intel RealSense, Mantis Vision, etc. In mobile phones (iPhone, Huawei) 3D structured light is mainly used for face unlocking, payment, beauty and other scenes. 

##  1. Project structure 

 ![avatar]( 841f1927eb494d43bc42f83387964bd2.png) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
##  2. Environment 

 Projects come with requirements.txt file, which contains the project development needs python dependency package has the corresponding version number, than the first dependency package numpy == 1.19.5, indicating that the project uses numpy library, the corresponding version is 1.19.5, you can choose to use pip to install the corresponding version: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
 Project dependency packages, please refer to requirements.txt 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
  Please refer to the project installation tutorial (beginners get started, please read the following tutorial first and configure the development environment): 

>  Project development tutorials and video tutorials for common problems and solutions: 3 How to create a pycharm environment with Anaconda Video tutorial: 4 How to use the python environment created by Anaconda in pycharm 

##  3. Binocular camera calibration and calibration 

###  (0) Binocular camera 

 The following binocular camera (RGB + RGB) was purchased at a treasure (a few hundred yuan, the link will not be sent, lest I advertise). As the binocular camera of this project, its baseline is a fixed 6cm, and it is a binocular camera with a single USB cable (the left and right cameras are spliced together in the same video), which basically meets our testing needs. Generally, the longer the baseline, the farther the measurable distance, and netizens can also buy it according to their own needs. 

 A note of caution: 

>  Binocular camera 3D reconstruction can also use RGB + IR (infrared) cameras, and even IR + IR cameras can be used. I personally test, RGB + IR cameras, the effect is also leveraged. The baseline is not recommended to be too small. As a test, the general baseline can meet the needs in 3~ 9cm. The binocular baseline of some unmanned vehicles is even more terrifying to 1~ 2 meters long. It can be seen from the principle of binocular 3D reconstruction that the imaging planes of the left and right cameras are in the same plane as possible, and the imaging plane is not in the same plane. Although it can be corrected in three dimensions, the effect is much worse. Penny, you get what you pay for. The quality of the camera directly determines your imaging effect 

 ![avatar]( 933fbf588e014e238ffbf2ec56d0b5f2.png) 

###  (1) Acquire left and right views of the calibration plate 

 Linux the end point of the system: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
 Windows system end point running (): 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
 Parameter description () 

>  The parameter width refers to the number of intersections of the black and white grid in the direction of the checkerboard width. The parameter height refers to the number of intersections of the black and white grid in the direction of the checkerboard length. The parameter left_video is the left camera ID, which is generally the camera connected to the main board. The USB interface number parameter right_video is the right camera ID, which is generally the USB interface number PS of the camera connected to the main board: If your binocular camera is a binocular camera with a single USB cable (left and right cameras are spliced together in the same video display), then set left_video = camera ID, and right_video = -1, the parameter detect is recommended to set True, which can detect the checkerboard in real time, and adjust the angle by pressing the keyboard's or c to save the left and right view pictures 

  The following is the Python code for collecting the left and right views of the binocular camera calibration board: get_stereo_images.py, in addition to OpenCV, there is no dependence, just do it. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
>  The objective of binocular calibration is to obtain the internal parameters, external parameters and distortion coefficients of the left and right cameras. The internal parameters include fx, fy, cx, cy of the left and right cameras. The external parameters include the rotation matrix and translation vector of the left camera relative to the right camera. The distortion coefficients include radial distortion coefficients (k1, k2, k3) and tangential distortion coefficients (p1, p2).

The most commonly used binocular calibration tool is the MATLAB toolbox: Stereo Camera Calibrator App. There are too many tutorials online, so I won't go into details. 

 I used the Deepin system and was too lazy to install Matlab, so I referred to various gods and implemented monocular and dual-purpose calibration procedures using OpenCV. 

###  (2) Monocular camera calibration and calibration (do not skip this step)  

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
 A note of caution:  

>  The calibration code will display the corner detection effect of the checkerboard of each image. If it is found that it cannot be detected, or the corner detection is wrong, you need to manually delete these images to avoid introducing too much error. If the error exceeds 0.1, it is recommended to readjust the camera and calibrate, otherwise the effect will be much worse 

 ![avatar]( faf200ae85ec4c6c974c1027995c30e4.png) 

  After execution, left_cam and right_cam camera parameter files will be generated in the $save_dir directory 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
>  Where K is the camera internal parameter matrix and D is the distortion coefficient matrix 

###  (3) Binocular camera calibration and calibration 

 After completing the monocular camera calibration and calibration, the next step is to perform binocular camera calibration and calibration. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
 A note of caution:   

>  If the error exceeds 0.1, it is recommended to readjust the camera and calibrate it. 

 After execution, the stereo_cam .yml camera parameter file will be generated in the $save_dir directory, which contains 

 stereo_cam.yml 

###  (4) About MATLAB binocular calibration results 

 The project source code supports monocular camera calibration and binocular camera calibration. In fact, you can calibrate without the Matlab toolbox; of course, if you have used the Matlab toolbox for binocular camera calibration, please modify the stereo_cam file according to the parameters 

>  Parameter size, corresponding to the image width and height (width, height) parameter K1, corresponding to the left-eye camera internal parameter matrix (3 × 3) parameter D1, corresponding to the left-eye camera distortion coefficient matrix (5 × 1) parameter K2, corresponding to the right-eye camera internal parameter matrix (3 × 3) parameter D2, corresponding to the right-eye camera distortion coefficient matrix (5 × 1) parameter T, corresponding to the binocular camera translation vector T (3 × 1) parameter R, corresponding to the binocular camera rotation matrix R (3 × 3), Matlab gives what appears to be the rotation vector om (1 × 3), please use cv2. Rodrigues () converts the rotation vector into a rotation matrix, referring to the following code for conversion. As for the parameters in the configuration file, such as R1, R2, P1, P2, Q, these reprojection matrices can be written down without modification. These will be recalculated at runtime. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
##  4. Parallax and depth maps 

###  (1) Stereo correction 

>  This part of the basic knowledge comes from: https://blog.csdn.net/dulingwen/article/details/100115157 

 The purpose of stereo correction is to perform mathematical projection transformation on the left and right views of the same scene, so that the two imaging planes are parallel to the baseline, and the same point is located on the same line in the left and right images, referred to as coplanar line alignment. Only after achieving coplanar line alignment can the principle of trigonometry be applied to calculate the distance. 

 ![avatar]( 20200613221307783.PNG) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
###  (2) Stereo matching and disparity map calculation 

 ![avatar]( gif.latex) 

 The purpose of stereo matching is to find the corresponding point (the same physical point in the world) in the right image for each pixel in the left image, so that the parallax can be calculated: (xi and xj respectively represent the column coordinates of the two corresponding points in the image). 

 The computational process of most stereo matching algorithms can be divided into the following stages:. Stereo matching is a difficult part of stereo vision. The main difficulties are: 

>  1. There may be duplicate and weak textures in the image, making it difficult to match these areas correctly.

2. Due to the different shooting positions of the left and right cameras, there is almost certainly an occlusion area in the image. In the occlusion area, some pixels in the left image do not have corresponding points in the right image, and vice versa.

3. The lighting conditions received by the left and right cameras are different;

4. The overexposed areas are difficult to match.

5. Inclined surfaces, curved surfaces, and non-Lambertian surfaces;

6. Higher image noise, etc. 

 The commonly used stereo matching methods can basically be divided into two categories: local methods, such as BM, SGM, ELAS, Patch Match, etc., non-local, that is, global methods, such as Dynamic Programming, Graph Cut, Belief Propagation, etc. The local method has a small amount of computation and a relatively low matching quality. The global method omits the cost aggregation and adopts the method of optimizing the energy function. The matching quality is high, but the computation amount is also relatively large. 

 At present, the methods that have been implemented in OpenCV include BM, binaryBM, SGBM, binarySGBM, BM (cuda), Bellief Propogation (cuda), and Constant Space Bellief Propogation (cuda). It is easier to use the SGBM algorithm. Its core is based on the SGM algorithm, but there are some differences with the SGM algorithm. For example, the matching cost part uses the BT cost (original image + layer diagram) instead of the HMI cost. For the principle explanation of the SGM algorithm, you can refer to another blog: "Binocular Stereo Matching Algorithm: SGM" https://blog.csdn.net/dulingwen/article/details/104142149 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
###  (3) Demo effect 

>  After the stereo matching generates the disparity map, the disparity map can also be filtered and processed, such as Guided Filter, Fast Global Smooth Filter (a fast WLS filtering method), Bilatera Filter, TDSR, RBS, etc. The disparity map filtering can transform sparse disparity into dense disparity, reduce the disparity map noise to a certain extent, and improve the visual effect of the disparity map, but it depends on the quality of the initial disparity map. 

>  It can be seen that after using WLS filtering, the overall effect of the disparity map has been significantly improved 

 ![avatar]( 53cf049177734c9d93cc087296ac8eed.gif) 

##  5. Binocular ranging 

 After obtaining the disparity map, you can calculate the pixel depth. Using the StereoRectify () function in opencv, you can obtain a disparity-to-depth mapping matrix from a 4 * 4 disparity map to a depth map. The Q matrix and cv2.reprojectImageTo3D can be used to convert the pixel coordinates into three-dimensional coordinates. The function returns a 3-channel matrix that stores X, Y, and Z coordinates respectively (under the left camera coordinate system). 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
 The calculation is as follows: 

 ![avatar]( eq) 

 ![avatar]( eq) 

 ![avatar]( 763b04f79f594fd29fdee97d73e37fe4.png) 

 ![avatar]( eq) 

 ![avatar]( eq) 

 ![avatar]( eq) 

 ![avatar]( eq) 

 And the coordinates of the main point of the left camera in the image, f is the focal length, which is the translation (negative value) between the projection centers of the two cameras, that is, the baseline, which is equivalent to the translation vector T [0], which is the coordinates of the main point of the right camera in the image. 

 Where Z is the depth distance: 

 ![avatar]( eq) 

 ![avatar]( eq) 

 ![avatar]( eq) 

 Where f is the focal length (pixel focal length), b is the baseline length, d is the parallax, and is the column coordinate of the two camera main points. 

>  Here is a place to note that if the obtained parallax image is of the CV_16S type, each pixel value of such a parallax map is represented by a 16bit, where the lower 4 bits store the fractional part of the parallax value, so the true parallax value should be Divide the value by 16. After mapping, it should be multiplied by 16 to obtain the millimeter-level true position. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
 ![avatar]( 3e96f96bdb474bea9370d894fc8cd065.png) 

##  6. Error description of binocular ranging 

  Error and accuracy of binocular ranging: 

 Accuracy Analysis of Binocular Stereo Vision System _3D Vision-CSDN Blog _ Binocular Vision Positioning Accuracy In a 3D measurement project, if a stereo vision scheme is adopted, first, the hardware scheme of stereo vision is determined according to the measurement requirements (accuracy, measurement range, speed, etc.). Thomas Luhmann in his "Close-Range Photogrammetry and 3D Imaging" (2014), gives a simplified analysis method of stereo vision system. This method assumes that the optical axes of the two cameras are parallel, the baseline is perpendicular to the optical axis, and there is no error in the baseline length b and focal length value c. The influence of image processing errors on stereo positioning is analyzed https://blog.csdn.net/xuyuhua1985/article/details/50151269 

##  7. 3D point cloud display 

 After restoring the 3D coordinates, you can use python-pcl and Open3D libraries to display point cloud images 

>  PCL Python version is difficult to install. If you can't install it, you can use Open3D to make do with it

As shown in the image below, you can use the mouse to rotate the coordinate axis and zoom in on the point cloud 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
##  8. Sample Code Demo 

 The project is equipped with the calibration parameter files of the binocular camera and the video files of the left and right cameras, which can be directly tested and used as a demo. How to use the demo: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
##  9. Binocular 3D reconstruction project code (Python version) 

  [] Binocular 3D reconstruction system (binocular calibration + stereo correction + binocular ranging + point cloud display) Python source code 

 The Python version of the project code includes: 

>  Binocular camera with dual USB cable Support binocular camera with single USB cable (left and right cameras are spliced in the same video display) Capture left and right view of calibration board: get_stereo_images.py support monocular camera calibration: mono_camera_calibration.py, no Matlab calibration Support binocular camera calibration: stereo_camera_calibration.py, no Matlab calibration Support Filtering of disparity map with WLS filter Support binocular ranging, the error is within 1cm (click the mouse to get its depth distance) Support Open3D and PCL point cloud display Source code Support Windows and Ubuntu systems 

 Project code structure:  

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957449303
  ```  
   [] Binocular 3D reconstruction system (binocular calibration + stereo correction + binocular ranging + point cloud display) Python source code 

 ![avatar]( aa5d7c6543724d0d91f1cc7b3c2c2e6e.gif) 

##  10. Binocular 3D reconstruction project code (C++ version) 

 At present, the binocular ranging of OpenCV C++ version has been realized, which is almost the same as the Python version. 

 For details, please check my other blog "OpenCV C++ binocular camera binocular ranging": https://blog.csdn.net/guyuealian/article/details/127446435 

 ![avatar]( 04b54039781b42ba905efbfba77072cb.gif) 

##  11. Binocular 3D reconstruction project code (Android version) 

 At present, the binocular ranging of the OpenCV Android version has been implemented, which is almost the same as the Python version. 

 If you need the Android version of binocular ranging, please check out my other blog "Android OpenCV for Binocular 3D Reconstruction: Binocular Camera for Binocular Ranging" 

 ![avatar]( 27381e84f63b48629f2ffb3e7d7ee15d.gif) 

 ![avatar]( a037c4083d104838a8e9d2d331a706ea.gif) 



--------------------------------------------------------------------------------

At present, the lidar of the velodyne series will already provide the value of ring. 

 The so-called value of the ring is that each point is emitted by several beams of light. 

 Refer to this picture. 

 ![avatar]( b6b89556765a4fd4b42aa84846ec33d5.png) 

 If you don't provide it, you need to calculate the value of the ring yourself. 

 Below is a reference code. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574458775
  ```  
 There are two super parameters 24.8, 2.0 represent the angle between the bottom beam of light and the horizontal line, and the angle between the top beam of light and the horizontal line, generally the bottom is large and the top is small, because the light hits the air is useless. These two parameters are in Kitti, which is why Kitti's lidar is basically too many points below. 

 The above calculation is also very easy to understand, that is, first calculate the pitch, and then look at the pitch of the entire beam of light angle ratio, note that when calculating this time, the pitch should add the upper and lower angle, it is estimated that because the bottom of the beam of light The label is 0 (for kitti.) 

 Then according to the proportion and the number of buses, it is roughly calculated which beam of light. 



--------------------------------------------------------------------------------

#  I. Overview of algorithms 

   The Chamfer Distance distance can calculate the average shortest point distance between the generated point cloud data and the labeled point cloud data. Open3D can be directly used to calculate the Chamfer Distance distance of the point cloud. For more details on the application of the Chamfer Distance in point clouds, please refer to: PCL calculation of point cloud chamfer distance (Chamfer Distance) or master's thesis: [1] Zhang Yonghan. Research on monocular vision 3D point cloud reconstruction technology based on deep learning [D]. Northeast Electric Power University, 2020. I won't go into too much detail here. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574453922
  ```  
#  III. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574453922
  ```  


--------------------------------------------------------------------------------

#  1. Conversion of radian system and angle system 

 Code implementation: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574426259
  ```  
>  Application example: Open3D curvature downsampling 

#  2. Code running time 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574426259
  ```  
#  3. Vector operations 

 ![avatar]( 8ecd13a2cce8493c827ebd638b23df1f.png) 

 Python Vector Operation Summary 

#  4. Calculate the mean, variance, and standard deviation 

 ![avatar]( e5c65a209c5d46a88088974281805fd1.PNG) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574426259
  ```  
#  5. Size and sorting 

 ![avatar]( f16746ecd43d41c9a5f3cfd4f2cfc3c9.png) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574426259
  ```  


--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

##  1. Process overview 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574433935
  ```  
#  III. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574433935
  ```  
##  1. Primitive point cloud 

 ![avatar]( df56f489d1fa4eeea70a29a7440d046f.png) 

##  2. Projection point cloud 

 ![avatar]( 72cd627813a0407ab1a7ec57d942f0f4.png) 

##  3. Concave polygon boundary 

 ![avatar]( be1d76dd6e574e4bad09b33275325cd4.png) 



--------------------------------------------------------------------------------

##  1. Install dependencies 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574463957
  ```  
##  2. Formal installation of pcl1.9.1 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574463957
  ```  


--------------------------------------------------------------------------------

c++ code for open3d and pcl data transfrom.

 ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574428571
  ```  


--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

##  1. Process overview 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574420725
  ```  
#  III. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574420725
  ```  
##  1. Primitive point cloud 

 ![avatar]( df56f489d1fa4eeea70a29a7440d046f.png) 

##  2. Projection point cloud 

 ![avatar]( 72cd627813a0407ab1a7ec57d942f0f4.png) 

##  3. Convex polygon boundary 

 ![avatar]( c620b5e9914f471c82e3395b9e810780.png) 



--------------------------------------------------------------------------------

 CPD algorithm 

#  First, the principle of the algorithm 

>  [1] Point set registration - CPD (Coherent Point Drift) [2] Point set registration technology (ICP, RPM, KC, CPD) 

##  1. Main function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957434885
  ```  
##  2. References 

>  [1] Myronenko, A., and X. Song. "Point Set Registration: Coherent Point Drift. "Proceedings of IEEE Transactions on Pattern Analysis and Machine Intelligence (TPAMI). Vol 32, Number 12, December 2010, pp. 2262–2275. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957434885
  ```  
#  III. Display of results 

##  1. Initial location of point cloud 

 ![avatar]( 20210427210934679.png) 

##  2. Position after registration 

 ![avatar]( 20210427211006334.png) 

>  Registration time: 33.781 sec. 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

   The implementation process in the code is very clear and requires no further introduction. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574437612
  ```  
#  III. Display of results 

 ![avatar]( dbb22c1a41f047a6a4bcb79b6f483a6c.png) 

#  IV. Relevant links 

 [1] Open3D KDTree的使用 



--------------------------------------------------------------------------------

#  First, the effect display 

 ![avatar]( d63fa3783b094371a8dd163a86552a28.gif) 

 ![avatar]( 41e5a665bb7f4905a1bbd7386c587d39.gif) 

#  Code 

##  2.1 Reference link: 

 ![avatar]( ab46225a44b5433eb0d617ebd518f049.png) 

 Reference paper link: Filling Holes in Meshes  

##  2.2 The complete code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574420495
  ```  
#  III. Other effects 

##  Comparison of filling effects of multiple hole point clouds 

 ![avatar]( cb4d090171844482b0b92b66687c7ff1.png) 

 ![avatar]( 1689691772fc47d39c84f80f5575761b.png) 

 ![avatar]( 8f341ff644304572b1596301ade3d1c8.png) 

 ![avatar]( bde02abb37ce4c34916f06d937393be2.png) 

#  IV. Follow-up 

 The relevant algorithms in easy3d will be integrated into the "Easy3d + QT" column in the future. 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

#  Code implementation 

##  1. Ordinary implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574429509
  ```  
##  2. Multi-threaded acceleration 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574429509
  ```  
#  III. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574429509
  ```  
 ![avatar]( 2cc41b86b6be4ee9803efb9e2d90b269.png) 



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

