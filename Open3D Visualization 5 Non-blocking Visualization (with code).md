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

