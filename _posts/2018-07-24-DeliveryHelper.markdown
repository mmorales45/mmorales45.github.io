---
layout: post
title:  DeliveryHelper
date:   2022-2-11 15:01:35 +0300 
image:  DeliveryHelper.gif
tags:   
---

For my Winter Project, I choose to create a robotic system that can act as a delivery assistant for delivering packages for those that need assistance or have many packages to carry at once.

[DeliveryHelper Github](https://github.com/mmorales45/deliveryhelper)

#### Skills Used:
* MediaPipe
* Robot Operating Software(ROS)
* MoveIt!
* C++
* Python
* Manipulation
* MoveBase

A clip of the Ridgeback following me when wearing an AprilTag.

<iframe width="560" height="315" src="https://www.youtube.com/embed/32niG_GuvUo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


### Systems
The project is composed of three main subsystems: manipulation, navigation, and perception. The main goal relied on these systems being able to communicate with one another and my approach for having theses systems interact with each other is through the use of topics provided by ROS. The systems can either subscribe or publish to the main topic that will take care of the interactions. 

#### Manipulation 

The Sawyer arm was controlled by using MoveIt! The arm can move through either the use of joint control or position control. Joint control was used for picking up blocks from the base of the Ridgeback whereas position control was used for picking up blocks from the little platform attached to the Ridgeback.

The video that follows presents the Sawyer arm picking up and placing a block through the use of ROS Services.

#### Navigation 

Getting the Ridgeback to follow a person was the first obstacle that needed to be overcome. My approach was to use a large AprilTag and place it on a vest that a person wears. Using AprilTag detection, the position of the tag was received and this position was used for determining where the Ridgeback move to. Using Move Base, the Ridgeback moved to a position offset from the AprilTag/Person and continuously sends out goals as long as the state is `Follow`.

#### Perception 

Initially my plan was to use AprilTags and attach them to gloves that the person would wear but being able to communicate with the system without other attachments/tools made more sense. MediaPipe was used for hand detection as well as pose detection. The more reliable option was the hand detection method since using the full body pose detection was too slow and would make the system unable to detect most gestures. 

### Integration

<p align="center">
  <img src="/images/DeliveryHelperFlowchart.png" />
</p>

Handling three systems that are independent of each other was a daunting task but as mentioned earlier, this would be solved by communicating through ROS topics. The general pipeline is that the perception detects hands/gestures and sends a message to the main topic. The Manipulation node then subscribes to this node and makes the arm perform the pick and place action. Once this action is done, it sends a message to the same topic with a message in the form of "Follow". When this message is true, the Ridgeback will follow the person but as soon as the person shows their hand again, then the Ridgeback will stop until the Manipulation node has accomplished it motion and publishes `Follow`.




<iframe width="420" height="315"
src="https://youtube.com/embed/Q41JVfnfLcU">
</iframe>

<iframe width="420" height="315"
src="https://youtube.com/embed/8SiEspXxug8">
</iframe>

<p align="center">
  <img src="/images/marco_robo_crop.jpg" />
</p>

