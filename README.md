   The content of this part is literally translated as "color mapping". The official website also describes "mapping colors to geometric shapes reconstructed from depth cameras", and this operation is called texture mapping in 3D modeling. I think it is better to call it texture mapping. The following is the text content, mapping colors to mesh geometries reconstructed from depth cameras. Since color frames and depth frames are not necessarily perfectly aligned, the result of texture mapping using color images will result in a blurry color mapping. Open3d provides based on the paper Q.-Y. Zhou, and V. Koltun, Color Map Optimization for 3D Reconstruction with Consumer Depth Cameras, SIGGRAPH, 2014. The following tutorial will provide an example of the color mapping optimization algorithm. 

#  1. Enter 

   The following code reads the color and depth image pairs and generates rgbd_image. Note that convert_rgb_to_intensity flag is set to False. This is to preserve 8-bit color channels instead of using single-channel floating-point images. It is best to visualize RGBD images before applying color mapping optimization. debug_mode choose whether to visualize RGBD images. (debug_mode visualization function written for myself, open3d-0.13.0 official website no longer has this code) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486838
  ```  
    Note: The above code is read from the local folder, which is different from the version widely circulated on the official website and the Internet. Test data free resource download link: test_data 

 The following code reads the camera track and mesh data. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486838
  ```  
 Read mesh, RGBD, and camera track data from folders 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486838
  ```  
   In order to visualize that the camera pose is not suitable for color mapping, the following code deliberately sets the number of iterations to 0, that is, does not optimize its mapping. color_map. run_rigid_optimizer use the corresponding camera pose and RGBD image to draw the mesh. If not optimized, you can see that the texture is blurry. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486838
  ```  
 ![avatar]( b220ead46f1847d8972e1572712f55a6.png) 

#  2. Rigid optimization 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486838
  ```  
    The function RigidOptimizerOption indicates using rigid optimization to optimize the six-dimensional pose of the camera. The following is the example code, maximum_iteration = 100 means setting the maximum number of iterations to 100. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486838
  ```  
 ![avatar]( ed157f1039264b41ba89d6549c456cd7.png) 

     In the content output by the console, Residual error is the residual, the residual indicates that the image intensity is inconsistent, and the lower the residual indicates that the color mapping quality is better. 

#  3. Non-rigid optimization 

   In order to have a better mapping quality, non-rigid optimization is required. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486838
  ```  
   Function NonRigidOptimizerOption uses non-rigid optimization. In addition to the six-dimensional camera pose, the non-rigid optimization even takes into account the local image deformation represented by the anchors. This method is more flexible and will have higher color mapping quality. The residuals will also be smaller than in the case of rigid optimization. Here is the example code, maximum_iteration = 100 means setting the maximum number of iterations to 100. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486838
  ```  
 ![avatar]( 0b8a172c6fa6454b8563287b99fc786d.png) 

#  4. Complete code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486838
  ```  


--------------------------------------------------------------------------------

##  First, the main function 

 1, Open3D img = o3d.io ("y7.png") to achieve image data reading, supported image formats jpg, png; 2, the size of the image can be easily obtained using print (img); 3, o3d.io write_image ("angel.jpg", img) to save the picture, the supported image format is jpg, png; 4, o3d.visualization.draw_geometries () to achieve picture display. 

##  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574496826
  ```  
##  III. Display of results 

 ![avatar]( 20210129212151835.png) 



--------------------------------------------------------------------------------

#  Traverse the octree 

##  1. Traverse the octree 

   For information on octree theory and how to build octree, please refer to: Open3D builds octree from point cloud, Open3D builds octree from voxel mesh. An octree can be traversed, which is useful for searching or dealing with sub-parts of 3D geometry. Open3D can perform additional processing each time a node (internal or leaf node) is visited by providing a traverse callback traversal method. In the example code below, only internal/leaf nodes with more than a certain number of points are processed using the early stop condition. This early stop ability can be used to efficiently process regions of space that meet specific conditions. 

##  2. Find leaf nodes that contain points 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574468155
  ```  
 locate_leaf_node function implementation returns the leaf OctreeNode and OctreeNodeInfo where the query point is located. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574468155
  ```  
#  III. Display of results 

 ![avatar]( 20210704212013457.png) 

 1. Traverse the octree 2. Octree information of points [0] 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574468155
  ```  
#  IV. Reference link 

 [1] Traversal [2] Open3d之八叉树(Octree) 



--------------------------------------------------------------------------------

#  I. Overview of algorithms 

##   1. Main function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 20240203095744775
  ```  
##   2. Source code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 20240203095744775
  ```  
#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 20240203095744775
  ```  
#  III. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 20240203095744775
  ```  
 ![avatar]( 2e091ec64d0744999a4d43ebfd258ec4.png) 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

>  [1] Point set registration - CPD (Coherent Point Drift) [2] Point set registration technology (ICP, RPM, KC, CPD) 

##  1. Main function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574499530
  ```  
##  2. References 

>  [1] Myronenko, A., and X. Song. "Point Set Registration: Coherent Point Drift. "Proceedings of IEEE Transactions on Pattern Analysis and Machine Intelligence (TPAMI). Vol 32, Number 12, December 2010, pp. 2262–2275. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574499530
  ```  
#  III. Display of results 

##  1. Initial location of point cloud 

 ![avatar]( 20210427210934679.png) 

##  2. Position after registration 

 ![avatar]( 20210427211006334.png) 

>  Registration time: 33.781 sec. 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

##  1. Algorithm overview 

   The principle of GICP algorithm is to combine ICP algorithm and Point-to-plane ICP into a probabilistic framework model, perform point cloud registration based on this framework, and play a role similar to weights through the covariance matrix to eliminate the role of some bad corresponding points in the solution process. GICP has a wider application range than standard ICP, and under certain conditions, the GICP algorithm degenerates into a standard ICP algorithm. At the same time, if there is a unique solution, the minimum point is the global optimal solution, and the GICP algorithm degenerates into a standard ICP algorithm. 

##  2. Algorithm flow 

   GICP is an extension of the "point-to-point" ICP and "point-to-plane" ICP methods. To improve the robustness of the registration, GICP uses the covariance matrix of the point cloud surface to construct the cost function of point cloud registration. Suppose we find two clusters of points in two 3D point clouds that are close neighbors to each other: = {} and = {}, where the sum matches each other. In probability theory, we assume that there are two clusters of points corresponding to each other = {} and = {}. So, it can be defined that the point cloud is generated by the following Gaussian distribution: Is the covariance matrix of each point. We define the rigid transformation matrix, and the registration error of each pair of corresponding points is as follows: because and belong to independent Gaussian distributions, then the distribution also belongs to the Gaussian distribution:  

##  3. References 

>  [1] Lin Baowei, Wang Fasheng, Sun Yi. Point cloud scale estimation and registration algorithm based on SGICP [J]. Computer Applications and Software, 2018, 35 (05): 202-207. [2] Generalized-ICP [C]//Robotics: Science and Systems V, University of Washington, Seattle, USA, June 28 - July 1, 2009. 

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574455222
  ```  
#  III. Display of results 

##  1. Primitive point cloud 

 ![avatar]( dfc21132253a48389efd3ee7d3c87701.png) 

##  2. Registration results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574455222
  ```  
 ![avatar]( 8cf8819bbc2d45d4aa8c6f39ebd54084.png) 



--------------------------------------------------------------------------------

#  First, the principle of the algorithm 

##  1. Overview 

   All data structures in Open3D are compatible with NumPy. The following tutorial uses NumPy to generate colors, assigns colors to a pcd point cloud using opend3d, and saves to a local folder. 

##  2. Main functions 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957446726
  ```  
#  Code implementation 

##  1. Generate custom colors 

 Note: The value range for colors in open3d is [0, 1], not [0, 255]. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957446726
  ```  
##  2. Results display 

 ![avatar]( 6344a25a07fb4c39a8bb59ccee0207d0.png) 

##  3. Single color (method 1) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957446726
  ```  
##  4. Display of results 

 ![avatar]( 029423ec32294098b2d0d679068f9a64.png) 

##  4. Single color (method 2) 

 This method does not require the use of numpy, but instead calls functions. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957446726
  ```  
##  4. Display of results 

 ![avatar]( 029423ec32294098b2d0d679068f9a64.png) 

#  III. Related Links 

 Open3D uses numpy (1) - save xyz coordinates 



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

#  Manual selection 

   Function pick_points (pcd) creates a VisualizerWithEditing instance to mimic draw_geometries, create a visual window, add geometric shape, visualize geometric shape and end. VisualizerWithEditing provides a new interactive function get_picked_points () that returns the index of a user-selected vertex. 

 ![avatar]( daa15427603a4bebb87228e05881cef4.jpeg) 

   Click shift + left button in the window to select a vertex. When a vertex is selected, the visual window will cover it with a sphere. For example, the following image shows the result after selecting a vertex on the source cloud.  

 It will print out: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574448538
  ```  
   Press q to close the window. Manual point selection is insufficient, and the output coordinates are incomplete. The default output of its source code is int type.  

#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574448538
  ```  
#  Automatic output of designated points 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574448538
  ```  
#  IV. Display of results 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574448538
  ```  


--------------------------------------------------------------------------------

#  First, simple visualization 

   Opene3d provides a simple visualization function draw_geometries, which is used to realize the rendering visualization of geometric objects (PointCloud, TriangleMesh or Image). In the visual interface, you can zoom, rotate and pan with the mouse, change the rendering style and screenshots, etc. The specific usage method can be viewed by pressing the h key on the window interface. In the open3d-0.13.0 version draw_geometries function has the following two calling methods: 

##  1. Main function 

 Call method one 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574478227
  ```  
 Code example 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574478227
  ```  
 Call method 2 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574478227
  ```  
##  2. Code example 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574478227
  ```  
##  3. Display of results 

 ![avatar]( 23335150c93640a8a3ba47ddfa21a2dc.png) 

#  Storage viewpoint 

 ![avatar]( 3a753dd7d6214cb7a80b11d181bf607f.png) 

   The point cloud displayed in the visual interface at the beginning is shown in the figure above. Drag the point cloud with the mouse to change a new display perspective. As shown in the figure below, after pressing ctrl + c to maintain this perspective, this perspective will become a json string saved in the paste board. At this time, rotate the view to a different perspective, like the figure below: At this time, press ctrl + v to return to the perspective saved by ctrl + c in the previous step.  

#  III. Rendering style 

 ![avatar]( 812cf4fc8adf47bc8525f27e07e0cc17.gif) 

   The Visualizer visualization function in Open3d supports a variety of rendering styles. For example, pressing L will toggle between Phong lighting and simple color rendering. Pressing 2 will reveal the color based on the x-coordinate. Color mappings can also be adjusted, such as using shift + 4 to adjust the color from an inkjet map to a heat map.  



--------------------------------------------------------------------------------

#  1. Draw the arrow 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486898
  ```  
 ![avatar]( 20210411162929424.png) 

#  2. Draw the sphere 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486898
  ```  
 ![avatar]( 20210411163358760.png) 

#  3. Draw the plane 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486898
  ```  
 ![avatar]( 9156f51875df48b59eaf1a5776c416a6.png) 

#  4. Draw the cylinder 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486898
  ```  
 ![avatar]( 20210411163628766.png) 

#  5. Draw cones 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486898
  ```  
 ![avatar]( 20210411164335677.png) 

#  6. Draw the circle 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486898
  ```  
 ![avatar]( 91290895e46748109919499c062296bd.png) 

#  7. Draw tetrahedrons 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486898
  ```  
 ![avatar]( ebf61d7a120843069953d95c4e3c718b.png) 

#  8. Draw cubes 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486898
  ```  
 ![avatar]( 20210411162623780.jpg) 

#  9. Draw the octahedron 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486898
  ```  
 ![avatar]( 983763cc85a54433800dd91d0b1086d8.png) 

#  10. Draw the icosahedron 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486898
  ```  
 ![avatar]( 304e13d89a8f4b0b87b688aa0a52b99d.png) 

#  11. Draw the Mobius Ring 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486898
  ```  
 ![avatar]( 7e423fbb88e7412ba876eb5a56b9e1af.png) 

#  12. Draw cubes with straight lines 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486898
  ```  
 ![avatar]( 20210411163818232.png) 

#  13. Draw triangles with straight lines 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574486898
  ```  
 ![avatar]( 9fd82899b55b4f299c5119a64d50eb1c.png) 



--------------------------------------------------------------------------------

#  1. Custom visualization 

   draw_geometries () and draw_geometries_with_custom_animation () functions make it easy to use Open3d's visualization functions, all of which can be done through the GUI. Press the h key in the visualization window to see the relevant help information. Imitate the draw_geometries () function through the Visualizer class 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574450529
  ```  
 ![avatar]( 20210310205100243.gif) 

 This function produces exactly the same functionality as draw_geometries (). The Visualizer class has several variables, such as ViewControl and RenderOption. The following function reads the predefined RenderOption stored in the json file. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574450529
  ```  
 ![avatar]( 20210310210018747.png) 

#   2. Change your perspective 

 To change the camera's perspective, you must first obtain an instance of the visual control. Use the change_field_of_view function to change the perspective. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574450529
  ```  
 Field of view (FoV) can be set by one degree in the range [5,90]. Note that the function change_field_of_view () adds the specified FoV to the current FoV. By default, the visualizer's field of view is 60 degrees. Call the following code: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574450529
  ```  
 ![avatar]( 20210310210856550.png) 

 This will add a 90 ° FoV to the default 60 °, and when the maximum FoV is exceeded, the FoV will be set to 90 °. The following code 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574450529
  ```  
 ![avatar]( 20210310211017852.png) 

 FoV will be set to 5 ° because 60 - 90 = -30 is lower than 5 °.  

#   3. Callback function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574450529
  ```  
 ![avatar]( 20210310211856422.gif) 

 draw_geometries_with_animation_callback register a Python callback function rotate_view as an idle function for the main loop. When the visualizer is idle, it rotates the view along the x-axis. This defines an animation behavior. Callback functions can also be registered when key events occur. This script registers four keys. For example, press k to change the background color to black. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574450529
  ```  
 ![avatar]( 20210310212542111.png) 

#   4. Capture images in custom animations 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574450529
  ```  
 ![avatar]( 20210310213616625.gif) 

 This function reads the camera track and then customizes the animation function move_forward to traverse the camera track. In this function, color images and depth images are captured using Visualizer.capture_depth_float_buffer and Visualizer.capture_screen_float_buffer, respectively, and then saved to a file. Captured Image Sequence: Captured Depth Sequence:  

#  5. Reference link 

 [1] Open3d学习计划——高级篇 10（自定义可视化） [2]【Open3d】使用open3d可视化 



--------------------------------------------------------------------------------

   It's relatively simple to go directly to the code. 

#  code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574473035
  ```  
#  result display 

 ![avatar]( 6378626a13cb4758968767c252e4ef0e.gif) 



--------------------------------------------------------------------------------

   draw_geometries () is a useful function when you need to visualize static geometry quickly. However, this function locks a process until the visualized window closes. This is not the best choice when you need to update the geometry and visualize it without closing the window. This article describes an example of a custom loop rendering. 

#  1. Review draw_geometries function 

   draw_geometries () has the following cyclic rendering: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574451757
  ```  
   Note: Binding geometry and rendering are both resource-intensive operations, so open3d operates in a lazy manner. When you need to bind and render geometry, use the update_geometry () and update_renderer () functions to set the binding and rendering functions to on, and empty these two flags after rebinding or rendering. Custom loop rendering is easy to implement, for example, the following example can customize the loop to visualize the ICP registration process. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574451757
  ```  
#  2. Visualize the ICP registration process 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574451757
  ```  
#  3. Function analysis 

   Call the registration_icp function in each iteration. Define that only one ICP registration is performed per loop by ICPConvergenceCriteria (max_iteration = 1). Each ICP registration is performed, and the source point cloud is correspondingly transformed and the geometric display of the source point cloud is updated in the visual interface. The core function of the visual registration process is done by calling update_geometry (). Finally, the visualizer renders the transformed point cloud by calling the poll_events () and update_renderer () functions. After all loops, calling destroy_window () will automatically close the display window. Adding vis.run () before the destroy_window () function will not automatically close the display window. 

#  4. Display of results 

 ![avatar]( 62e346cf067b48f2b19fc898e0cd4dd2.gif) 



--------------------------------------------------------------------------------

   This tutorial introduces the interactive function of Open3D's visual window. Test data: Open3D-ICP algorithm test data.rar 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574410660
  ```  
   This script executes two user interaction applications: demo_crop_geometry () and demo_manual_registration (). 

#  1. Cut the geometry 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574410660
  ```  
   This function simply reads a point cloud and then calls the draw_geometries_with_editing function, which provides vertex selection and clipping. 

>  Note: Open3d has a VisualizerWithEditing class that inherits the Visualizer class. It provides graphical user interaction. In the same example, VisualizerWithEditing () can explicitly replace draw_geometries_with_editing ([pcd]) in a custom visualization. 

 ![avatar]( 990d7f511ffe46c386fcc8f480640821.png) 

   After the geometry is displayed, press Y twice to align the geometry with the negative half axis of the Y axis. After adjusting the viewing angle, press K to lock the view and switch to selection mode.  

>  Tip: In the actual operation of the selected area, the orthographic projection model is generally used to align the geometry with any axis. This technique avoids the problem of occlusion due to the perspective projection strip, making the selection easier. 

 ![avatar]( 0b40d8c6a6394462addf18838ebf7695.png) 

   To select an area, you can drag with the mouse (rectangular area) or ctrl + click with the left mouse button (select polygon area). The following example shows polygon selection. The selected area is dark shaded, if you want to save the selected area and discard the rest, press C. A dialog box will pop up to select the file path to save the cropping. The result of the cropping is saved after it is displayed. Press F to end selection mode and enter free browsing mode.  

#  2. Manual registration 

##  2.1. Select the corresponding point 

   Select the corresponding point, and the following code uses a point-to-point ICP to register the two point clouds. It obtains the initial alignment through human interaction. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574410660
  ```  
 ![avatar]( 5043a6a19dc3418b92cedb2b4342780c.png) 

   This script reads two sets of point clouds and visualizes them before they are aligned. Press the q key to proceed to the next step.  

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574410660
  ```  
   Function pick_points (pcd) creates a VisualizerWithEditing instance to mimic draw_geometries, create a visual window, add geometric shape, visualize geometric shape and end. VisualizerWithEditing provides a new interactive function get_picked_points () that returns the index of a user-selected vertex. 

 ![avatar]( 73cd806fa4d24a9abc940c2e59be4b13.png) 

   Click shift + left button in the window to select a vertex. When a vertex is selected, the visual window will cover it with a sphere. For example, the following image is the result after selecting three vertices on the source cloud. It will print: 

>  After picking points, press ‘Q’ to close the window [Open3D INFO] Picked point #54681 (2.1, 1.6, 1.5) to add in queue. [Open3D INFO] Picked point #55609 (2.6, 1.6, 1.6) to add in queue. [Open3D INFO] Picked point #94992 (2.2, 2.0, 0.9) to add in queue. 

 ![avatar]( 066fe0c9090446ebb8736366a0fcc94b.png) 

   Press q to close the window, and then select the corresponding corresponding point on the target point cloud. The color of this sphere helps to identify the same corresponding point. It will print out: 

>  After picking points, press ‘Q’ to close the window [Open3D INFO] Picked point #53641 (1.6, 1.8, 1.2) to add in queue. [Open3D INFO] Picked point #54498 (2.0, 1.7, 1.4) to add in queue. [Open3D INFO] Picked point #109840 (1.9, 2.4, 0.8) to add in queue. 

   In order to get a good registration result, three corresponding points should be selected that are evenly dispersed in the scene. Selecting the vertices of the corner area helps to select high-quality corresponding points. 

##  2.2. Use the user-selected correspondence registration 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574410660
  ```  
   The follow-up part of the demo calculates the initialization transformation based on the user-supplied correspondence. This script establishes a pair correspondence by using Vector2iVector (corr). Use TransformationEstimationPointToPoint compute_transformation to calculate an initialization transformation. Then use registration_icp fine-tuning based on this. 

##  2.3. Registration results 

 ![avatar]( 756b2896d088421d82df2ae6e71b0d64.png) 



--------------------------------------------------------------------------------

#  I. Overview 

 ![avatar]( bce181c12f544d59b4a6c9faf058c223.gif) 

    Open3D integrates user interface development capabilities to create beautiful user interfaces without the use of Qt.  

##  1. Main function 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574459999
  ```  
#  Code implementation 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574459999
  ```  
#  III. Display of results 

 ![avatar]( 45a86884de794651881fe7c3b5307931.gif) 



--------------------------------------------------------------------------------

#  I. Overview 

 ![avatar]( 42d7874fcd9247d7870bf91fe6b3b35a.png) 

    Open3D also has a calling function for adding 3D text labels to the visual interface of the point cloud. Select a point evenly every 100 points, select a total of 20 points, and add a dot label to the point. The display effect is as follows:  

##  1. Main function 

 add_3d_label add the specified 3D text label at the given coordinate position. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574492654
  ```  
#  Code implementation 

##  1. Point label 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574492654
  ```  
##  2. Centroid label 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574492654
  ```  
#  III. Display of results 

 ![avatar]( 287bc4162d514e89b97fd958723883c9.png) 



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

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


--------------------------------------------------------------------------------

