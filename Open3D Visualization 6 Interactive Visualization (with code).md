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

