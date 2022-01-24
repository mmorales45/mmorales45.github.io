---
layout: post
title:  RoboKeeper
date:   2021-12-11 15:01:35 +0300 
image:  robokeeper_gif.gif
tags:   
---

The goal of this project was to create a robot that is able to act as a goal keeper and block balls from entering the goal. This would be accomplished by using a HDT Global Adroit Manipulator Arm, an Intel RealSense Camera, a paddle and red balls.

[RoboKeeper Github](https://github.com/mmorales45/final-project-robokeeper)
#### Team Members:
* Marco Morales
* Cody Nichoson
* Jonny Bosnich
* Joshua Cho
* Lio Liang

#### Skills Used:
* OpenCV
* ROS
* MoveIt!
* Python
* Manipulation

<iframe width="420" height="315"
src="https://youtube.com/embed/Q41JVfnfLcU">
</iframe>


<p align="center">
  <img src="/images/marco_robo_crop.jpg" />
</p>

### Tasks
Each team member was in charge of a compoennt of the project such as the perception, test, or manipulation of the robotic arm. I was primarily in charge of perception for the system. I created a program that is able to track a red ball when it is in the camera's frame.The ball was located by using OpenCV to locate objects that fall within a HSV range. This would provide the lcoation, and coordinates, of the ball relative to the camera and after applying transformations to these coordaintes, the ball's location can be found relative to the base of the Adroit. 

I also contributed to other parts of the system such as the manipulation component. I programmed the robot to be able to retrieve the paddle from its holster and then return to it's home position to be ready to start goal keeping. 

### Future Work
The system can be improved upon to make it more robust. For example, more high speed camera's can be added to the system as well as increasing the area for where it can goal keep. This would allow for the robot to be able to block balls for a wider area as opposed to just a goal. More high speed camera's can improve the ball detection algorithm. 