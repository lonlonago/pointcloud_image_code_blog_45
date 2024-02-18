#  First, the principle of the algorithm 

##  1. Overview 

   The random sample consensus algorithm (RANSAC) is an iterative method for calculating the parameters of a mathematical model from a series of data containing divorced values. The RANSAC algorithm essentially consists of two steps, which are continuously looping: (1) randomly select the minimum number of elements that can form a mathematical model from the input data, and use these elements to calculate the parameters of the corresponding model. The selected number of these elements is the minimum number that can determine the parameters of the model. (2) Check which elements in all the data can conform to the model obtained in the first step. Elements that exceed the error threshold are considered outliers, and elements smaller than the error threshold are considered inliers. This process is repeated many times, and the model with the most points is selected to obtain the final result. 

##  2. Fitting plane 

>  RANSAC is specific to the fitting plane in the spatial point cloud: 1. Three points are randomly selected from the point cloud. 2. These three points form a plane. 3. Calculate the distance from all other points to the plane. If it is less than the threshold T, it is considered to be a point in the same plane. 3. If there are more than n points in the same plane, save the plane and mark all points on this plane as matched. 4. The condition for termination is that the plane found after N iterations is less than n points, or three unmarked points cannot be found. 

##  3. Implementation process 

   At present, the most common and simplest method to fit a plane is least squares fitting, but the accuracy of least squares fitting is easily affected by noise. The random sampling consensus algorithm (RANSAC) can eliminate the influence of noise through iterative fitting, and the fitting accuracy is greatly improved. The random sampling consensus algorithm process is shown in Figure 1:1. From the mathematical knowledge, it is known that at least three points are required to fit the plane, so three points are randomly selected first, and then the plane model parameters are calculated according to the plane equation (1). 2. Use the remaining data points to test the plane model estimated in (1), calculate the result error, and compare the error with the set error threshold. If it is less than the set threshold, determine the point as the inner point, and count the number of inner points under the parameter model and record it. 3. Continue with steps 1 and 2. If the number of inner points of the current model is greater than the maximum number of inner points that have been saved, update the model parameters. The retained model parameters are always the model parameters with the largest number of inner points. 4. Repeat steps 1 to 3 and iterate until the iteration threshold is reached. Find the model parameters with the largest number of inner points. Finally, use the inner points to estimate the model parameters again to obtain the final model parameters. 

 ![avatar]( 20210516154607138.png) 

##  4. References 

>  [1] Wang Shaochen. Research on the measurement method of workpiece curved surface profile based on point cloud reconstruction technology [D]. Shandong University, 2020. 

#  Second, the main function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574465386
  ```  
   Use segement_plane function to implement RANSAC to split the plane from the point cloud. The three parameters required by this function are as follows: 

 The function returns (a, b, c, d) as a plane with axis + by + cz + d = 0 for each point (x, y, z) on the plane. The function also returns a list of indices of interior points. 

#  III. Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574465386
  ```  
#  IV. Display of results 

 ![avatar]( 20200826105012458.png) 

 Plane equation: 0.02x + -0.01y + 1.00z + 6.41 = 0  

#  V. Related Links 

 [1] ransac提取地面（python） [2] 线性拟合笔记之：Ransac算法 [3] RANSAC算法详解(附Python拟合曲线和平面) 

