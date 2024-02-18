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

