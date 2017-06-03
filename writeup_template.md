## Project: Search and Sample Return
### Writeup Template: You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---



[//]: # (Image References)

[image1]: ./misc/rover_image.jpg
[image2]: ./calibration_images/example_grid1.jpg
[image3]: ./calibration_images/example_rock1.jpg 
[rock-sample]: ./rock-sampled-threshed.png
[output-video]: ./test_mapping.mp4

## [Rubric](https://review.udacity.com/#!/rubrics/916/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it!

### Notebook Analysis
#### 1. Run the functions provided in the notebook on test images (first with the test data provided, next on data you have recorded). Add/modify functions to allow for color selection of obstacles and rock samples.
Here is an example of how to include an image in your writeup.

Created a function to find the navigable terrain by threshing the image color channels greater than  RGB(160,160,160)
Original Image               Navigable Terrain

![Original][image1]         ![Navigable][navigable]


Created a function to detect the golden rocks (samples) by threshing the image within a color range using opencv library.
Original Image               Golden Rocks Terrain

![rock sample][rock-sample]



Created a function to detect the obstacle by threshing the image color channels less than RGB(160,160,160).
Original Image               Obstacle Terrain

![Original][image1]         ![Obstacle][obstacle]

Then created functions to convert the navigable pixels to Rover coordinates.


#### 1. Populate the `process_image()` function with the appropriate analysis steps to map pixels identifying navigable terrain, obstacles and rock samples into a worldmap.  Run `process_image()` on your test data using the `moviepy` functions provided to create video output of your result. 

In this functions, called the navigable terrain, convert to rover coordinates, detect the samples and obstacles.
Then added the navigable terrain, rocks, and obstacles on to the ground truth map.
Ran this method on the recorded navigation images and below the video of the mapping of the terrain, rocks and smples on the ground truth map in moveipy functions.


![Test OutPut Video][output-video]

### Autonomous Navigation and Mapping

#### 1. Fill in the `perception_step()` (at the bottom of the `perception.py` script) and `decision_step()` (in `decision.py`) functions in the autonomous mapping scripts and an explanation is provided in the writeup of how and why these functions were modified as they were.


#### 2. Launching in autonomous mode your rover can navigate and map autonomously.  Explain your results and how you might improve them in your writeup.  

**Note: running the simulator with different choices of resolution and graphics quality may produce different results, particularly on different machines!  Make a note of your simulator settings (resolution and graphics quality set on launch) and frames per second (FPS output to terminal by `drive_rover.py`) in your writeup when you submit the project so your reviewer can reproduce your results.**

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.  



![alt text][image3]


