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

