#  First, the principle of the algorithm 

##  1, normal vector estimation 

   Based on the local surface fitting method for normal vector estimation: when the sampling surface of the point cloud is smooth everywhere, the local neighborhood of any point can be well fitted by the plane;

##  2, normal vector orientation 

   The normal vector calculated earlier is ambiguous, that is, only the line where the normal vector is located is obtained, but the direction of the line is not determined as the final direction of the normal vector. The normal vector is redirected by the following method: Assuming that the point cloud is dense enough and the sampling plane is smooth everywhere, then the normal vector of two adjacent points will be close to parallel.

##  3. Surface curvature 

     The greater the delta, the greater the fluctuation of the neighborhood. 

##  4. References 

>  [1] Wang Fei, Liu Rufei, Ren Hongwei, Chai Yongning. Multi-phase vehicle laser point cloud registration using road target features [J]. Journal of Surveying and Mapping Science and Technology, 2020, 37 (05): 496-502. [2] Xing Zhengquan, Deng Kazhong, Xue Jiqun. Initial registration of point clouds based on K-nearest neighbor search [J]. Surveying and Mapping Science, 2013, 38 (02): 93-95. [3] Li Xinchun, Yan Zhenyu, Lin Sen, Jia Di. Point cloud registration based on neighborhood feature point extraction and matching [J]. Journal of Photonics, 2020, 49 (04): 255-265. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574450402
  ```  
