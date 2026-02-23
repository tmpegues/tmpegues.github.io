---
name: Polydact, A Flexible New Finger
tools: [Python, ROS 2, OnShape, ]
image: http://localhost:4000/assets/polydact/placeholder.png
description: Designed and built a wearable sensor-integrated glove and flexible supernumerary finger to expand the dexterity of a human hand.
---

## Overview
Over the Winter 2026 quarter, I have been developing a wearable robotic sixth finger that will allow the user greater dexterity than they have with their natural hand.This project is a work in progress. The description here is up to date as of 22 February 2026.

## Tentacle Design
The design of the tentacle is based on a set of nested logarithmic spirals, as developed by Z. Wang (Reference 1). Polydact uses a 30 bone long tentacle, with the spiral discretized into 30 degree increments, which allows the tentacle to wrap 2.5 times around itself when fully curled. The black tentacle shown in images and videos was 3D printed in one piece on a PrusaXL with black PLA bones and a red central TPU spine. The spine is 15% of the width of each bone, tapering along its length.

## Actuation
The tentacle is actuated by three cables (30 lb fishing line) strung through itself and tied through a bead at the small end. The other end of the cables pass through the hand-bracket and travel through plastic tubing and end tied to spools mounted on three motor shafts. The motors used here are Dynamixel XW540-T140s, which are 185 g (~.4 lb each). Due to the combined weight of three motors, they are mounted on the user's shoulder. Each motor is held in a frame with a dovetail connector that slides into the shoulder strap.

## Control

{% include elements/video.html id="https://tmpegues.github.io/assets/polydacy/glove_video1.mp4" %}

Polydact's main control device is a glove with integrated flex sensors and contact pads. The bends measured by flex sensors along the ring, middle, and index fingers are remapped to [-1, 1], then multiplied by the desired motor speed limit. Each finger directly controls the speed of one motor. Position and effort limits are imposed; the encoder readings of each motor are recorded during calibration, then the motors are not allowed to wind or unwind outside the range of spiral lengths determined during tentacle design. The main effort limit prevents over-curling of the tentacle, protecting the motors from overload. The secondary effort limits requires that the motors always maintain tension in the cables. This prevents loose cable from tangling around the motor shaft and keeps the tentacle reaction speed as high as possible.

## References
[1] Z. Wang, "SpiRobs: Logarithmic spiral-shaped robots for versatile grasping across scales," *Device*, vol. 3, April 2024, doi:10.1016/j.device.2024.100646