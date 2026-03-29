---
name: Polydact, A Flexible New Finger
tools: [Mechatronics, OnShape, Python, Rapid Prototyping, ROS 2, Sewing]
image: /assets/polydact/sprite.gif
permalink: /projects/polydact
description: Designed and built a flexible supernumerary finger and sensor glove to expand the dexterity of a human hand.
---
GitHub repo here: {% include elements/button.html link="https://github.com/tmpegues/polydact" text="GitHub" style="secondary" size="sm" %}

{% include elements/youtube.html id="WlC2JOe-_yc" %}

## Overview
I have developed a wearable robotic sixth finger that gives its user greater dexterity than they have with their natural hand. The Polydact device is controlled by a hand made glove with embedded flex sensors.

{% include elements/figure.html image="assets/polydact/blocks_simple.svg"%}

## Tentacle Design
The design of the tentacle is based on logarithmic spirals, as developed by Z. Wang (Reference 1). It was 3D printed in one piece with PLA (orange) and a TPU spine (black, not visible in video or image). 3M GM640 gripping tape (black) is added to the main inner surface both for the added grip, and also to indicate the main flexing direction.

<details>
    <summary class="text-monospace">Further design detail...</summary>
    Scaling factors a and b were set as 1.0 and 0.1 respectively, with a split angle of 30°. I wanted the tentacle to be able to coil around itself twice when fully tightened in one direction, so I required at least 24 bones and used 30. With a = 1.0 and b = 0.1, the tightest coil possible is ~2.3 cm. 2.3 cm, just over an inch, is the smallest diameter object I can pick up. I did not have a specific target for largest diameter.
    <br><br>
    See Reference 1 for spiral math derivations.
</details>

{% include elements/figure.html image="assets/polydact/tent2.jpg" caption="Tentacle and wrist mount" %}

## Control
Polydact's main control device is a glove with integrated flex sensors. The flex reading is mapped to motor velocity, which spool or unspool the three cables that travel the entire length of the tentacle and terminate in a knot at its free end. Several parts on the entire Polydact device are color coded red, green, and blue. This makes it easier for the user to know which finger controls which direction of tentacle bend.


{% include elements/figure.html image="assets/polydact/blocks_detail.svg" %}
{% include elements/figure.html image="assets/polydact/glove_circuit2.svg" caption="Glove and circuit diagram" %}

## Part Mounting
The tentacle itself is seated in a hexagonal socket (purple) and held in place with two screws. The socket has receptacles on the back to hold the tendon guide tubes in place and holes in the center of each face. These holes, in conjunction with a nut on the interior of the socket, hold the tentacle in the socket and also attach the socket to the wrist mount (pink). The angle of the socket in the plane of the hand is easily adjusted by tilting the socket before tighening the nuts on the outside of the wrist mount.

The wrist mount has slots for a strap; it is tied to the user with a band of spandex. Most other parts are also attached to the user with a band of spandex. The switch box, Raspberry Pi, Robotis U2D2, and motor strap also all have slots for straps and attach to a band tied around the user's chest. The motors are held in frames with dovetail connectors that slide into the motor strap. The battery is placed in the user's pocket.

I sewed the control glove using the same spandex as the wrist and chest bands. Flex sensors are held in 3D printed slots sewn into the back of the middle three fingers. Sensor wiring is also sewn onto the back of the glove.

The tentacle, socket, wrist mount, motor strap, motor frames, spools, and sensor slots were 3D printed. The Raspberry Pi case and U2D2 mount are made of a combination of 3D printed and laser cut parts, although they were designed to all be easily laser cut.  The switch box is intentionally a combination of 3D printed and laser cut parts. I designed all 3D printed and laser cut parts.

{% include elements/figure.html image="assets/polydact/labeled_parts.svg"%}



## ROS Nodes
Two nodes must be run to control the device: a sensor node (serial or Pi/ADC) and a motor coordinator node. The sensor node reads flex values and publishes MotorGoal messages to command motor velocity. The motor coordinator node subscribes to the MotorGoal messages and uses the DynamixelSDK to write commands to the motors.

During early development, flex values were read using a Raspberry Pi Pico 2's ADC pins and sent values over USB serial to my laptop, running both the serial sensor and motor coordinator nodes. Flex values are currently read using a MCP3008 ADC connected to a Raspberry Pi running its own sensor node. The motor coordinator can run on either the Raspberry Pi or a laptop connected to the same network.

## References
[1] Z. Wang, "SpiRobs: Logarithmic spiral-shaped robots for versatile grasping across scales," *Device*, vol. 3, April 2024, doi:10.1016/j.device.2024.100646