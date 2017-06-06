## Project: Search and Sample Return

---



[//]: # (Image References)

[terrain]: ./terrain-warped-threshed-nav.png
[obstacle]: ./obstacle.png 
[obstacle1]: ./obstacle-1.png 
[obstacle2]: ./obstacle-2.png 
[rock-sample]: ./rock-sampled-threshed.png
[output-video]: ./test_mapping.mp4


---
### Writeup / README

### Notebook Analysis
#### 1. Run the functions provided in the notebook on test images (first with the test data provided, next on data you have recorded). Add/modify functions to allow for color selection of obstacles and rock samples.


Created a function to find the navigable terrain by threshing the image color channels greater than  RGB(160,160,160)
Then created functions to convert the navigable terrain pixels to Rover coordinates.

**Functions:**
  color_thresh(img, rgb_thresh=(160, 160, 160)): 
     -- This generates the navigatable binary image.
  perspect_transform(img, src, dst):
     -- 
  rover_coords(binary_img): 
     -- Finds the Rover coords, its current position
  to_polar_coords(x_pixel, y_pixel):
      -- In this function find the distance and navigable angles
  translate_pix(xpix_rot, ypix_rot, xpos, ypos, scale): 
      -- 
  pix_to_world(xpix, ypix, xpos, ypos, yaw, world_size, scale):
      -- Called the above functions ( perspect_tranform, rover_coord, translate_pix)
  

Below are the images for original, terrain , threshed 

![Navigable Terrain][terrain]




Created a function to detect the golden rocks (samples) by threshing the image within a color range using opencv library.
rock_detection(img, rgb_rock_low=(0, 0, 0),rgb_rock_hi=(0,0,0)):


Below are images for original rock image and its threshed image

![rock sample][rock-sample]



Created a function to detect the obstacle by threshing the image color channels less than RGB(160,160,160).
obstacle_detection(img, rgb_thresh=(160, 160, 160)):
Below are the different obstacles images with their threshed images

![Obstacle][obstacle]
![Obstacle1][obstacle1]
![Obstacle2][obstacle2]






#### 1. Populate the `process_image()` function with the appropriate analysis steps to map pixels identifying navigable terrain, obstacles and rock samples into a worldmap.  Run `process_image()` on your test data using the `moviepy` functions provided to create video output of your result. 

In this function, defined the source and destination which I arrived at by measuring the pixels of rover's camera view, then translated those coordinates into a top-down view of the Rover.
Then warped the rover's top down view and applied the threshold to get the navigable terrain, then converted the navigable terrain to rover coordinates, then called functions to detect the samples and obstacles.
Then added the navigable terrain, rocks, and obstacles on to the ground truth map.
Ran this method on the recorded navigation images and below is the video of the mapping of the terrain, rocks and smples on the ground truth map in moveipy functions. Below is the generated video


![Test OutPut Video][output-video]

### Autonomous Navigation and Mapping

#### 1. Fill in the `perception_step()` (at the bottom of the `perception.py` script) and `decision_step()` (in `decision.py`) functions in the autonomous mapping scripts and an explanation is provided in the writeup of how and why these functions were modified as they were.
   Defined source and destination points for perspective transform, then applied the perspective transform with perspect_transform function. Applied the color threshold to identify navigable terrain ( color_thresh) /obstacles(obstacle_detection)/rock samples (rock_detection) functions.

Updated the Rover.vision_image to display the obstacle , rock sample and navigable terrain in a threshed binary images.
Then converted the map image pixels to rover-centeric coords with rover_coords function, and then converted the rover-centri pixels to world coordinates. Then updated the rover worldmap to show the obstacle,samples and navigable terrain.
After that converted the rover-centric pixel to polar coordinates to enable the direction to streer.


For every frame from the Rover's camera is processed by the Perception and Decision, to decide what is there infront of the rover and take action accordingly.
**Perception**
  This function helps to process the frame, find the position of the rover, decide how long is the navigable terrain available, at the same time check whether there are any obstacles and samples to pickup.
**Decision **
  After every frame is processed and the respective values assigned to the Rover's State object, this function enables to take the decision by reading the values from Rover's state, whether to move forward, stop, turn , throttle, or to pick up the samples.
  At first the Rover starts to move in forward direction.
  First I check whether there is any visible terrain, that i will get from the Rover.nav_angles, if it is not null , then i will check whether my Rover is moving in the Forward or Stopped mode from Rover.mode.
  When my Rover is "Forward", I will check, whether I have enough of navigable terrain by checking the number of Rover.nav_angles greater than the Rover.stop_forward limit. If I more nav_anlges, then I will check the throttle, if it is less than the max_vel, then give an acceleration by increasing the throttle to throttle_set, else decrease the throttle.


#### 2. Launching in autonomous mode your rover can navigate and map autonomously.  Explain your results and how you might improve them in your writeup.  

Used Resolutions : 
1280 x 800

**Note: running the simulator with different choices of resolution and graphics quality may produce different results, particularly on different machines!  Make a note of your simulator settings (resolution and graphics quality set on launch) and frames per second (FPS output to terminal by `drive_rover.py`) in your writeup when you submit the project so your reviewer can reproduce your results.**


I want to improve the following
1.Some times at the dead ends, it is falling into circular rotation going into infine loop
2.Update the code to pickup all the samples
3.Some times near some big rock, it is getting stuck, want to manuever properly to get out the rocks (obstacles).





