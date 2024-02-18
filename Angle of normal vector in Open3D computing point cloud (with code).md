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

