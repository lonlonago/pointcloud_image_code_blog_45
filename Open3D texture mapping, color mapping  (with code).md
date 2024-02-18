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
