---
name: Bug Catcher
tools: [MoveIt 2, Onshape, OpenCV, Python, ROS 2 ]
image: https://tmpegues.github.io/assets/bug/bug1.png
description: Developed ROS 2 packages to use a FER arm to pick up and sort moving turtles
---

## Overview
This project was completed in a team of four for Northwestern's [MECH_ENG 450: ](https://www.mccormick.northwestern.edu/mechanical/academics/courses/descriptions/450-embedded-systems-in-robotics.html) Embedded Systems in Robotics.

My team chose to catch and sort HexBugs by color as the task for our Franka arm to perform. This idea was split into 3 main sub-tasks: determining the location of our camera relative to the robot, determining the positions of the points of interest (HexBugs, locations to sort to) relative to the camera, then moving the robot based on that information. My primary focus was motion.

{% include elements/figure.html image="https://tmpegues.github.io/assets/bug/bug1.png" caption="The FER arm picking up a turtle/HexBug" %}

## Position Calculations
The first step in execution of the picking and sorting is determining the locations of the camera that is suspended above the robot. The locations of the four AprilTags on the corner of the wooden arena are used for this, as their locations are known relative to the base of the FER arm. I 3D printed a locator that fits around the FER arm base to ensure that the wooden base is located properly when placed and the AprilTags are reliable. 300 frames (10 seconds) of camera data are used for this calibration, then the camera is added to the tf tree. The root of the tf tree is the robot base, which connects to the the rest of the robot, the four arena corner markers, and now the camera in six parallel branches.

After determining the location of the camera relative to the arena corner tags and robot base, the locations of the white hexagons relative to the robot base are determined. Each of these hexagons is the sort location for one color of HexBug. The mode then switches to the final state, detecting the HexBugs.

{% include elements/video.html id="https://tmpegues.github.io/assets/bug/rviz.mp4" %}

## Motion
Because the HexBug turtles move with a bit of randomness, it wouldn't have been possible to use the provided MoveIt 2 actions to send a trajectory to the arm, as these are given fixed endpoints instead of a moving target. We could have either moved the arm at relatively high speeds and sent sequential trajectories every time the previous one finished or we could have cancelled the action and sent a new trajectory as we detected new HexBug positions. Instead, we used MoveIt for trajectory calculation and then sent the trajectory directly to the *joint_trajectory_controller*, which allowed us to constantly send new trajectories and have them update immediately.

{% include elements/video.html id="https://tmpegues.github.io/assets/bug/bug_tracking.mp4" %}

In the video above, the FER arm is tracking a turtle position simulated by the ROS 2 turtlesim.

### More Info
My teammates were Rishika Bera, Nolan Knight, and Halley Zhong, all MSR '26.

Please see the GitHub repo here for more detail: [Link to be updated when available](https://github.com/tmpegues/bug_catcher)