---
layout: project
title: Jenga Player
date: January 2022
image: /public/images/jenga1.png
---

## Overview
This robot was built for Caltech's [ME/EE/CS 134: Robotic Systems](https://www.cms.caltech.edu/academics/courses/mecsee-134). My teammates were Matthew Earney '24, Olivia Ernst '22, and Susu Le '22.

My team chose to design and build a robot capable of playing Jenga. We were provided with very ROS compatible motors, several example files (and experience from previous robotics courses), and set free to implement our idea. While we all contributed to all parts of the project, my primary focus was the vision system.

### Vision
Our robot uses a 720p webcam and OpenCV to determine the location of the 54 blocks in the Jenga tower. Each block has a 4x4 ArUco marker laser eched and painted on its end face that's used to determine its 3D pose and orientation. Each block marker was about 10 mm. In addition to the markers on every block, the Jenga tower is built on a sheet of paper with three large markers that are used as coarse stationary references. The Jenga block on the bottom right of the tower is used as a finer reference point, under the assumption that the robot or human player will never remove that block from the tower. One advantage of this approach that I didn't anticipate is that the camera can be placed anywhere, as long as the markers can be seen with enough detail. The camera can even be moved while the robot is running and it will automatically adjust all of the 3D transforms.

The primary purpose of the vision system is to deliver block coordinates to the movement system to be able to accurately remove blocks and place them on top of the tower. Our primary method of determining if a block can be removed from the tower is effort feedback from the motors: if the effort is low, the block is loose and may be removed. I added a fallback option that used the camera to determine if more than one block moves when a single block is poked.

### Link
Unfortunately, I don't have the full documentation for this project anymore, but I do have the vision code: [GitHub link](https://github.com/tmpegues/jenga_vision)