#  First, the principle of the algorithm 

##  1. Calculation process 

 ![avatar]( 20210307103542835.png) 

 1. According to the coordinate set of point cloud data, obtain the maximum and minimum values on the three coordinate axes. 2. Set the side length of the voxel small grid. 3. Find the side length of the minimum bounding box of the point cloud according to the maximum and minimum values on the three coordinate axes. 4. Calculate the size of the voxel grid. In the formula,  

 6. Sort the elements in order from smallest to largest, and randomly select a point in each voxel small grid to replace all the points in the small grid. 

##  2. Main functions 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574470387
  ```  
#  III. Display of results 

 ![avatar]( 7f4c93021e0c4af3bc48c66f8098b3a8.png) 

