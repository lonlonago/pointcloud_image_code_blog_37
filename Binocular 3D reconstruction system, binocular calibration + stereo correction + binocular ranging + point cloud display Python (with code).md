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

