---
title: "Swarm Construction"
date: 2025-10-01
draft: false
author: "An Nguyen"
tags:
  - Python
  - CAD
  - OptiTrack

image: 
description: ""
toc: true
mathjax: true
socialShare: False

---
## Overview
The goal of this project is to build a bridge autonomously using a swarm of drones.

---
## Gripper Design
Lightweight passive grippers are preferred due to the drones’ weight and control constraints. Each gripper must be capable of attaching to, carrying, and releasing the building blocks reliably.

**Previous designs**:

<div style="display: flex; justify-content: space-between;">
    <img src="/images/projects/construction/gripperv1.gif" alt="gripperv1" style="width: 48%; height: auto;"/>
    <img src="/images/projects/construction/gripperv2.gif" alt="gripperv2" style="width: 48%; height: auto;"/>
</div>
<br>

The first version requires the drone to apply a substantial amount of force to pick up the droxel. It also needs to exert the same amount of force and ascend quickly to detach from it.

The second version is too bulky, and even when operated manually, a person must be very careful when sliding in the droxel. Otherwise, it tends to rotate diagonally and get stuck in the frame, preventing the gripper from releasing it.

**Finalized design**:
<div style="display: flex; justify-content: space-between;">
    <img src="/images/projects/construction/gripperv3.gif" alt="gripperv3" style="width: 48%; height: auto;"/>
    <img src="/images/projects/construction/drox_attached.jpg" alt="a droxel attached to a drone" style="width: 48%; height: auto;"/>
</div>
<br>

The final design uses two magnets, one embedded on top of the droxel and the other placed deeper inside the gripper. A small gap between the top of the gripper and its internal magnet reduces the magnetic force, allowing the droxel to detach easily when the drone twists in the yaw direction.

---
## Next Steps
Conduct flight tests with a single drone, followed by scaling up to multiple drones for the construction task.



