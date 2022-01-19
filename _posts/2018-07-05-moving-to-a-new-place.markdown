---
layout: post
title:  Moving to a new place
date:   2018-07-05 15:01:35 +0300
image:  best.gif
tags:   Home
---
# Capstone Project
[Capstone Github](https://github.com/mmorales45/Capstone-Project)

#### Skills Used:
* Python
* Manipulation

## Overview
For the Final Project, the goal was to control the Kuka youBot in CoppeliaSim
and have it pick up a cube and move it a goal location specified by the user. 

<p align="center">
  <img src="/Marco_Morales_Portfolio/public/images/overshoot.gif" alt="animated" />
</p> 

## NextState
The first Milestone's purpose is to calculate the new arm joint angles, wheel joint angles, and chassis configuration given the current conifguration. NextState also checks the velocity of the joint angles and limits them if they pass a max velocity value. The script produces a csv file of the new configurations when it is ran.

## Trajectory Generator
The goal of this Milestone, ScrewTrajectory, is to create a script that is able to calculate the trajectory of the end effector as it completes eight tasks. The tasks follow: move the end effector to a configuration above the cube's initial configuration, move the end effector to the cube configuration to grasph, close the gripper, move the end effector to a configuration above the cube's initial configuration, move the to a standoff configuration above the cube's final configuration, move the end effector to the cube's final configuration, open the gripper, and finally move to the standoff configuration above the cube's final configuration. 

After each instance of ScrewTrajectory, the values were appended to a list in the form of r11,r12,r12,etc. This was done with the function add_to_trajList that recieved a transformation matrix and indexed the important values such as the rotation and matrix values and added the gripper state to a list composed of these 13 values. This was done eight times to correspond to the number of steps the end effector completes. TrajectoryGenerator returns this list of 13 values. It was then converted to a .csv file called Trajetory.csv.

## FeedbackControl
Milestone 3 calculates the controls based on the proportional and integral gains. An important note is that the twist error was calculated and graphed so show if, at all, the error converges to zero and is able to complete all eight tasks mentioned in Trajectory Generator.