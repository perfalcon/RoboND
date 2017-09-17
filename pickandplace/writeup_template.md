
## Project: Kinematics Pick & Place
------
Steps to do 
1) Take the images for Kuka Arm from the Demo ( Rzviz & Gazebo)
2) Label the Kuka Arms joints, Links,
3) Create the DH Table
4) 
--------
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

This program will try to pick and place the objects from the shelf and drop them in the bin.
This program uses the Kinematcis ( Forward and Inverse ) to calculate the positions and trajectory to drop in the bin.

[//]: # (Image References)

[image1]: ./images/Kuka-Arm1.PNG
[image2]: ./images/Kuka-Arm2.PNG
[image3]: ./images/Label-Kuka-Arm.jpg

### Kinematic Analysis
#### 1. Run the forward_kinematics demo and evaluate the kr210.urdf.xacro file to perform kinematic analysis of Kuka KR210 robot and derive its DH parameters.

Used the below two images to create the kuka-arm in 2D by labelling the joints, links in the XYZ axis.

![KukaArm-Rzviz][image1]     ![KukaArm-Rzviz][image2] 


This is the Kuka-Arm with all the labels.

![Labelled-Kuka-Arm-2D][image3] 



#### 2. Using the DH parameter table you derived earlier, create individual transformation matrices about each joint. In addition, also generate a generalized homogeneous transform between base_link and gripper_link using only end-effector(gripper) pose.

Links | alpha(i-1) | a(i-1) | d(i-1) | theta(i)
--- | --- | --- | --- | ---
0->1 | 0 | 0 | 0.75 | 
1->2 | - pi/2 | 0.35 | 0 | -pi/2 + q2
2->3 | 0 | 1.25 | 0 | 
3->4 |  -pi/2 | -0.054 | 1.50 | 
4->5 | pi/2 | 0 | 0 | 
5->6 | -pi/2 | 0 | 0 | 
6->EE | 0 | 0 | 0.303 | 0


#### 3. Decouple Inverse Kinematics problem into Inverse Position Kinematics and inverse Orientation Kinematics; doing so derive the equations to calculate all individual joint angles.

And here's where you can draw out and show your math for the derivation of your theta angles. 

![alt text][image2]

### Project Implementation

#### 1. Fill in the `IK_server.py` file with properly commented python code for calculating Inverse Kinematics based on previously performed Kinematic Analysis. Your code must guide the robot to successfully complete 8/10 pick and place cycles. Briefly discuss the code you implemented and your results. 


Here I'll talk about the code, what techniques I used, what worked and why, where the implementation might fail and how I might improve it if I were going to pursue this project further.  


And just for fun, another example image:
![alt text][image3]


