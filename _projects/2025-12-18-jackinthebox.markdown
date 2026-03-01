---
layout: post
modal-id: 2   # I don't think this is used on my theme
date: 2025-12-18    # I don't display a date on my projects, but if you change layout on line 2 to post, it will display
name: Jack-in-the-Box Physics Simulation # name is used on the index page
title: Jack-in-the-Box Physics Simulation # title is used if layout is post instead of default, not required

image: /img/portfolio/jackbox.gif    # Should be image instead of img, and you need to give a full or relative path, I'm not sure it has a default directory
alt: Jack-in-the-Box Simulation # Not sure where this is used
project-date: Dec 2025  # I don't think this is used on my theme
#client: "Physics-Based Robotics Simulation"
#category: "Dynamics • Simulation • Control"
permalink: /projects/jackinthebox   # The url defaults to the title of the .md/.markdown file, but you can set a permalink here it (since you have dates in your file names).
description: "A physics-based simulation of a jack-in-the-box that realistically models bouncing and collisions using real-world motion principles."
weight: 1 #I don't think this is used on my theme. Maybe is for posts/blog instead of projects

#tech: "Rigid body dynamics · Impact modeling · Euler–Lagrange equations · SE(3) transformations · Numerical simulation · Python"

tools: [ Euler–Lagrange,  Rigid-Body Dynamics,  Impulse Impacts,  Coordinate Frames,]  # Change from tags to tools to display on the index page

github: https://github.com/zhul49/Jack-in-the-Box # Not used on my theme, you'll have to add a button as shown below.
---

GitHub repo here: {% include elements/button.html link="https://github.com/zhul49/Jack-in-the-Box " text="GitHub" style="secondary" size="sm" %}


## Project Summary
This project simulates a jack-in-the-box mechanism to study the interaction between rigid-body motion and internal impacts. The system’s motion is computed from analytical dynamics, with collisions between the jack and the box resolved using impulse-based methods.

The result is a compact simulation that highlights the role of coordinate frames, equations of motion, and contact dynamics in mechanical behavior.

## Frames, Dynamics, and Impacts
The system is represented using multiple coordinate frames. A fixed world frame defines the inertial reference. A box frame moves and rotates with the enclosure. A jack frame rotates inside the box and defines the positions of the four tip masses. Points are mapped between frames using rigid-body transformations of the form

<p style="text-align:center;">
  p<sub>world</sub> = R · p<sub>body</sub> + t
</p>

Expressing the jack in the box frame simplifies contact detection, since the box walls are fixed in that frame.

The motion of the box and jack is derived using the Euler–Lagrange formulation,

<p style="text-align:center;">
  d/dt(∂L/∂q̇) − ∂L/∂q = Q
</p>

which governs smooth translational and rotational motion between collisions. These equations are numerically integrated forward in time.

When a jack tip contacts a wall, the collision is treated as an instantaneous event. Instead of integrating through contact, velocities are updated using an impulse-based formulation. The post-impact generalized velocities satisfy

<p style="text-align:center;">
  ∂L/∂q̇⁺ = ∂L/∂q̇⁻ + Jᵀλ
</p>

where \(J\) is the contact Jacobian and \(λ\) is the impulse magnitude. The impulse is solved by enforcing the contact constraint together with an energy consistency condition, resulting in realistic momentum transfer between the internal jack and the box. These repeated impacts produce rotation, bouncing, and jitter of the enclosure.

![Jack Frames](/img/portfolio/jackframes.png)

