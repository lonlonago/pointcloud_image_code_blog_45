#  First, the principle of the algorithm 

##  1. Algorithm overview 

 Voxel downsampling creates a uniform downsampling point cloud from the input point cloud by using a regular speed-up mesh. This is usually done in the preprocessing step of the point cloud processing task. This algorithm is divided into two steps: 

 ![avatar]( 20210620191459999.gif) 

 1. Load the point cloud into the voxel grid 2. Average the points in each occupied voxel and take an exact point.  

##  2. Calculation process 

 ![avatar]( 20210307103542835.png) 

 1. According to the coordinate set of point cloud data, obtain the maximum and minimum values on the three coordinate axes. 2. Set the side length of the voxel small grid. 3. Find the side length of the minimum bounding box of the point cloud according to the maximum and minimum values on the three coordinate axes. 4. Calculate the size of the voxel grid.  

 6. Sort the elements in order from smallest to largest, calculate the center of gravity of each voxel small grid, and replace all points in the small grid with the center of gravity. 

##  3. Main functions 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574429141
  ```  
 This function samples the input point cloud to the output point cloud with voxels. Normals and colors, if present, are averaged. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574429141
  ```  
#  III. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574429141
  ```  
 ![avatar]( bb5f83e3fbd842b4b4cb4b4e031f6135.png) 

