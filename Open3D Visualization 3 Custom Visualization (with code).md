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

