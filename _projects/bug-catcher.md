---
name: Bug Catcher
tools: [MoveIt 2, Onshape, OpenCV, Python, ROS 2 ]
image: https://tmpegues.github.io/assets/bug1.png
description: Developed ROS 2 packages to use a FER arm to pick up and sort moving turtles
---

## Overview
This project was completed for Northwestern's [MECH_ENG 450: Embedded Systems in Robotics](https://www.mccormick.northwestern.edu/mechanical/academics/courses/descriptions/450-embedded-systems-in-robotics.html). My teammates were Rishika Bera, Nolan Knight, and Halley Zhong, all MSR '26.

My team chose sorting HexBugs by color as the task for our Franka arm to perform. This idea was split into 3 main sub-tasks: determining the location of our camera relative to the robot, determining the positions of the points of interest (HexBugs, locations to sort to) relative to the camera, then moving the robot based on that information. My primary focus was motion, but this was a collaborative effort and I made contributions to vision and designed a part to reliably locate our wooden arena around the base of the robot.

{% include elements/figure.html image="https://tmpegues.github.io/assets/bug1.png" caption="The FER arm picking up a turtle/HexBug" %}

## Motion
Because the HexBug turtles move with a bit of randomness, it wouldn't have been possible to use the provided MoveIt 2 actions to send a trajectory to the arm, as these are given fixed endpoints instead of a moving target. We could have either moved the arm at relatively high speeds and sent sequential trajectories every time the previous one finished or we could have cancelled the action and sent a new trajectory as we detected new HexBug positions. Instead, we used MoveIt for trajectory calculation and then sent the trajectory directly to the *joint_trajectory_controller*, which allowed us to constantly send new trajectories and have them update immediately.


### Link
Please see the GitHub repo here for more detail: [Link to be updated when available]()