---
name: Polydact, A Flexible New Finger
tools: [Mechatronics, OnShape, Python, Rapid Prototyping, ROS 2, Sewing]
image: /assets/polydact/sprite.gif
permalink: /projects/polydact
description: Designed and built a flexible supernumerary finger and sensor glove to expand the dexterity of a human hand.
---
GitHub repo here: {% include elements/button.html link="https://github.com/tmpegues/polydact" text="GitHub" style="secondary" size="sm" %}

{% include elements/video.html id="https://tmpegues.github.io/assets/polydact/sprite.mp4" %}

## Overview
I have been developed a wearable robotic sixth finger that gives its user greater dexterity than they have with their natural hand. The Polydact device is is controlled by a hand made glove with embedded flex sensors.


{% include elements/figure.html image="assets/polydact/blocks_simple.png"%}

## Tentacle Design
The design of the tentacle is based on logarithmic spirals, as developed by Z. Wang (Reference 1). It was 3D printed in one piece with PLA (orange) and a TPU spine (black, not visible in video or image). 3M GM640 gripping tape (black) is added to the inner surface both for the added grip, and also to indicate the main flexing direction.

{% include elements/figure.html image="assets/polydact/tent2.jpg" caption="Tentacle and wrist mount" %}


## Control
Polydact's main control device is a glove with integrated flex sensors. The flex reading is mapped to motor velocity, which spool or unspool the three cables that travel through the length of the tentacle.


{% include elements/figure.html image="assets/polydact/blocks_detail.png" %}
{% include elements/figure.html image="assets/polydact/glove_circuit2.svg" caption="Glove and circuit diagram" %}

## ROS Nodes
Two nodes must be run to control the device: a sensor node (serial or Pi/ADC) and a motor coordinator node. The sensor node reads flex values and publishes MotorGoal messages to command motor velocity. The motor coordinator node subscribes to the MotorGoal messages and uses the DynamixelSDK to write commands to the motors.

During early development, I read flex values using a Raspberry Pi Pico 2's ADC pins and sent values over USB serial to my laptop, running both the serial sensor and motor coordinator nodes. I currently read flex values using a MCP3008 ADC connected to a Raspberry Pi running its own sensor node. The motor coordinator can run on either the Raspberry Pi or a laptop connected to the same network.

## References
[1] Z. Wang, "SpiRobs: Logarithmic spiral-shaped robots for versatile grasping across scales," *Device*, vol. 3, April 2024, doi:10.1016/j.device.2024.100646