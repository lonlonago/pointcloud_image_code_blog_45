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

