---
layout: post
title:  Iso Proj
date:   2021-12-09 15:01:35 +0300 
image:  best.gif
tags:   
---
I progammed the youBot, from Kuku, in CoppeliaSim
to have it pick up a cube and move it a goal location specified by the user under various conditions.

[Capstone Github](https://github.com/mmorales45/Capstone-Project)

#### Skills Used:
* Python
* Manipulation

<p align="center">
  <img src="/images/overshoot.gif" alt="animated" />
</p> 

The final iteration of the system now had Robotiq grippers for each arm. The grippers were initially controlled through low level control but eventually the ROS drivers/wrappers for the Robotiq grippers were fixed and used. As for the computer of the system, a powerful Alienware laptop was used that was running Ubuntu and running both robotic arm drivers, the camera, the the manipulation node. A laptop is a great solution. Its compact which is a huge benefit considering the amount of space on the system was limited and its powerful enough to enough everything without a concern for performance. There was a small problem in the form of power. This computer drew much more power than its Raspberry Pi 4 competitor which an average power consumption of 85 watts wereas the smaller computer only drew around 5-10 watts. The solution was to add an additional battery that could power the laptop for a full day of operation. 
