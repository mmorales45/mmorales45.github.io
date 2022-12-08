---
layout: post
title:  Isotope Retrieval Project
date:   2022-12-10 15:01:35 +0300 
image:  DeliveryHelper.gif
tags:   Simple
---

## Overview

After gaining experience in a variety of areas in robotics, I wanted to work on a project in the areas I found the most interesting. This led me to working on a project with Argonne National Laboratory under the supervision of Dr. Jerry Nolen and Dr. Park. Dr. Nolen's lab works with medical isotopes and retrieving them is a huge problem due to radiation levels and time contraints. The longer it takes for the sample to be taken, the more it deteriorates, or decays. Currently, the way the sample is retrieved is through a human going into the radioactive area, with protective gear, and do the steps required to get a hold of the isotope and take it out of the dangerous enviorment. A proposed solution is to make a robot go into the lab and get the isotope but the question was what system can help solve this problem. The system that was made was one composed of a UR16e, UR5e and a MiR 250 mobile base. 

The goal of this project is to use these three independent robots and have them work together to navigate through a radioactive enviorment, approach the isotope target, decouple it from the beam line and finally bring it back to reseachers so that they can perform experiments and reearch on it. 

To learn more about getting the system running, check out my [Github Repo!](https://github.com/mmorales45/IsotopeRetrieval)

#### Skills Used:
* Robot Operating Software(ROS)
* MoveIt!
* C++
* Python
* Manipulation
* System Integration

A clip of the Ridgeback following me when wearing an AprilTag.

<iframe width="560" height="315"
src="https://youtube.com/embed/32niG_GuvUo">
</iframe>

### Design of the System

The system was composed of two different arms due to budgest contraints. One option was to use two UR5e to make the system symmetrical and balanced but this came at the cost of the total payload the arms could carry to be 10 kg. This could limit the ability of the system to perform is faced with a heavy object. Although the system would be not symmetrical and it would require to mount the arms so that is not imbalanced, the ability to have a total payload of 21 kg would allow the system to be versatile through a variety of different objetcs. 


The initial system was composed was composed of the core robotic components but with no grippers attached and each arm was controlled by its own Raspberry PI4. The idea behind the two Raspberry PI 4s was ti reduce the amount of load each computer would have to go through and each computer would run the driver for just one arm. A main computer would be used by the researchers and the three computers would share the same ROS_MASTER_URI so that the main computer can access the nodes/drivers for each arm without being connected to it directly. Besides have no gripper, the biggest flaw in this system was power. The two robotic arms and mobile base were being powered by the battery on the MiR base and with the battery being used by three robots already, adding two more sources of power consumption was going to be a problem if the power draw is too much for the onboard battery. 


The second iteration of the system now had a gripper! However it was an old model Robotis Gripper that did not provide enough force to grip objects heavier than 3 kgs. However, it was enough for picking up light objects. In terms of the computer for the system, it was now down to just one Raspberry PI 4. This was influenced by the previously mentioned power issue but also because a MoveIt config package was made so that a single launchfile could run both robots drivers and the MoveIt launchfile can allow for both arms to move in the same ROS_MASTER. But an issue that came up was performance. Path planning was much slower when compared to just one computer per arm and this is to be expected since the computer was also running the full desktop version of Ubuntu so it had other processes occuring in the background. Increasing this performance with a single onboard computer that would not draw too much power lead to idea of using a Nvidia Jetson Nano but it still had many of the same shortcomings. 

The final iteration of the system now had Robotiq grippers for each arm. The grippers were initially controlled through low level control but eventually the ROS drivers/wrappers for the Robotiq grippers were fixed and used. As for the computer of the system, a powerful Alienware laptop was used that was running Ubuntu and running both robotic arm drivers, the camera, the the manipulation node. A laptop is a great solution. Its compact which is a huge benefit considering the amount of space on the system was limited and its powerful enough to enough everything without a concern for performance. There was a small problem in the form of power. This computer drew much more power than its Raspberry Pi 4 competitor which an average power consumption of 85 watts wereas the smaller computer only drew around 5-10 watts. The solution was to add an additional battery that could power the laptop for a full day of operation. 



