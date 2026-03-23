---
name: Polydact, A Flexible New Finger
tools: [OnShape, Python, ROS 2, Sewing]
image: /assets/polydact/sprite.gif
permalink: /projects/polydact
description: Designed and built a wearable sensor-integrated glove and flexible supernumerary finger to expand the dexterity of a human hand.
---
GitHub repo here: {% include elements/button.html link="https://github.com/tmpegues/polydact" text="GitHub" style="secondary" size="sm" %}

## Overview
I have been developing a wearable robotic sixth finger that will give the user greater dexterity than they have with their natural hand. The Polydact device is is controlled by a hand made glove with embedded flex sensors.

{% include elements/video.html id="https://tmpegues.github.io/assets/polydact/sprite.mp4" %}

## Tentacle Design
The design of the tentacle is based on logarithmic spirals, as developed by Z. Wang (Reference 1). It was 3D printed in one piece with PLA (orange) and a TPU spine (black, not visible in video). 3M GM640 gripping tape is added to the inner surface both for the added grip, but also to indicate the main flexing direction.


## Control
Polydact's main control device is a glove with integrated flex sensors. The flex reading is mapped to motor velocity, which spool or unspool the three cables that travel through the length of the tentacle.


## References
[1] Z. Wang, "SpiRobs: Logarithmic spiral-shaped robots for versatile grasping across scales," *Device*, vol. 3, April 2024, doi:10.1016/j.device.2024.100646