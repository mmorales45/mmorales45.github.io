---
layout: post
title:  DeliveryHelper
date:   2022-3-18 15:01:35 +0300 
image:  DeliveryHelper.gif
tags:   
---

For my Winter Project, I choose to create a robotic system that can act as a delivery assistant for delivering packages for those that need assistance or have many packages to carry at once. It consists of a Ridgeback mobile base with a Sawyer arm mounted to it with a Bumblebee camera attached to the base.

For more information on the Ridgeback and Sawyer, check out the follow repositories: [Ridgeback](https://github.com/jimas95/nu_ridgeback/blob/master/nuridgeback_robot/launch/accessories.launch), and [Sawback](https://github.com/jimas95/sawback)

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

<iframe width="560" height="315"
src="https://youtube.com/embed/32niG_GuvUo">
</iframe>


### Systems
The project is composed of three main subsystems: manipulation, navigation, and perception. The main goal relied on these systems being able to communicate with one another and my approach for having theses systems interact with each other is through the use of topics provided by ROS. The systems can either subscribe or publish to the main topic that will take care of the interactions. 

A clip of the Ridgeback following me continuously. 

<iframe width="560" height="315"
src="https://www.youtube.com/embed/YpbKCqEOXKY">  
</iframe>

#### Manipulation 

The Sawyer arm was controlled by using MoveIt! The arm can move through either the use of joint control or position control. Joint control was used for picking up blocks from the base of the Ridgeback whereas position control was used for picking up blocks from the little platform attached to the Ridgeback.

The video that follows presents the Sawyer arm picking up and placing a block through the use of ROS Services as well as the view in RVIZ of the robot interacting with the block. 

<iframe width="560" height="315"
src="https://www.youtube.com/embed/SF2OrLYvXV4">  
</iframe>

<iframe width="560" height="315"
src="https://www.youtube.com/embed/SUha2dAgDAM">
</iframe>

#### Navigation 

Getting the Ridgeback to follow a person was the first obstacle that needed to be overcome. My approach was to use a large AprilTag and place it on a vest that a person wears. Using AprilTag detection, the position of the tag was received and this position was used for determining where the Ridgeback move to. Using Move Base, the Ridgeback moved to a position offset from the AprilTag/Person and continuously sends out goals as long as the state is `Follow`.

The next video shows the Ridgeback following me as I turn towards a hallway.
<iframe width="560" height="315"
src="https://www.youtube.com/embed/clr_ug3EA_I">  
</iframe>

The next two videos show the Ridgeback rotating to match the user's position. One is the the RVIZ view of the robot detecting the AprilTag and then issuing commands to rotate the robot while the other is the real world video of the Ridgeback rotating. 

<iframe width="560" height="315"
src="https://www.youtube.com/embed/RiRbWFQ4rcE">
</iframe>

<iframe width="560" height="315"
src="https://www.youtube.com/embed/bEwPnggq2Cc">
</iframe>

#### Perception 

Initially my plan was to use AprilTags and attach them to gloves that the person would wear but being able to communicate with the system without other attachments/tools made more sense. MediaPipe was used for hand detection as well as pose detection. The more reliable option was the hand detection method since using the full body pose detection was too slow and would make the system unable to detect most gestures. With more time, pose detection could have been used to issue specific gestures based on pose detection.

The next video is the camera's video using hand detecting with MediaPipe.

<iframe width="560" height="315"
src="https://www.youtube.com/embed/bXr1E_0RuOY">  
</iframe>

The next video is the camera's video using Pose detecting with MediaPipe.

<iframe width="420" height="315"
src="https://www.youtube.com/embed/op8U7gr9XKs">
</iframe>

### Integration

<p align="center">
  <img src="/images/DeliveryHelperFlowchart.png" />
</p>

Handling three systems that are independent of each other was a daunting task but as mentioned earlier, this would be solved by communicating through ROS topics. The general pipeline is that the perception detects hands/gestures and sends a message to the main topic. The Manipulation node then subscribes to this node and makes the arm perform the pick and place action. Once this action is done, it sends a message to the same topic with a message in the form of "Follow". When this message is true, the Ridgeback will follow the person but as soon as the person shows their hand again, then the Ridgeback will stop until the Manipulation node has accomplished it motion and publishes `Follow`.

When the launchfile is ran with the perception node, once perception detects a hand, it will start making the Ridgeback follow the person. Once hands are detected again, it will start the manipulation node to pick up the block on the base. The next instance will result in the Sawyer picking up the block on the attached stand.


### Future Work

There are two key ways to improve the system. First, improving the navigation of the system so it can better follow the person through hallways, around obstacles, etc. The other way is to remove the need for a large AprilTag on the person and some other form of human detection. This would help remove the need for extra components and make it more intuitive to apply in real work scenarios. 

Test