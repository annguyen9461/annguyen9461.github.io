---
date: 2025-03-14
published: true
title: "Self-Reconfigurable Quadruped From Scratch"
description: "C++, Python, ROS2, YOLO, CAD"
categories: branding, digital
technologies: C++, Python, ROS2, YOLO, CAD
media: Book
ownership: Personal
client:
time_period: 2025
thumbnail: "/projects/quad/quad.gif"

intro: |
  **OVERVIEW**

  For my winter project, I designed and built a self-reconfigurable quadruped 
  that can switch between walking and rolling modes. 
  I also integrated ROS2 and YOLO for a computer vision task.

  **COMPONENTS**
  - Raspberry Pi 5
  - Intel RealSense Depth Camera D435i
  - DYNAMIXEL U2D2 Power Hub
  - DYNAMIXEL U2D2
  - DYNAMIXEL XC430-T240BB-T Motor (x 12)
  - Adafruit ISM330DHCX - 6 DoF IMU - Accelerometer and Gyroscope
  - 3S Lipo Battery 5200mAh 50C 11.1V RC Batteries
  

content_layout:
  - section_layout: 2col
    images:
      - caption: CAD Design
        description: 'URDF of robot'
        url: '/projects/quad/quad-urdf.gif'
        width:
        height:
      
      - caption: Top View
        description: 'Top View'
        url: '/projects/quad/quad_view.png'
        width:
        height:


  - section_layout: 2col
    images:
      - caption: Rolling Mode
        description: 'Rolling Mode'
        url: '/projects/quad/quad_rolling.png'
        width:
        height:

      - caption: Walking Mode
        description: 'Walking Mode'
        url: '/projects/quad/quad_walking.png'
        width:
        height:
  
  - section_layout: text
    content: |
      ## PROCESSING IMU DATA FOR ROLLING

      To determine when and how to propel the quadruped robot in rolling mode, we process accelerometer and gyroscope data from the ISM330DHCX sensor via I²C on a Raspberry Pi 5.

      The key goal is to compute the **tilt angle** of the robot using acceleration in the Y and Z axes:

      $$
      \theta = \arctan\left(\frac{a_y}{a_z}\right)
      $$

      where:
      - \\( a_y \\) : linear acceleration along the Y-axis  
      - \\( a_z \\) : linear acceleration along the Z-axis


      This angle is converted from radians to degrees to determine the robot’s current orientation and decide which side (blue or yellow) is on the ground:

      $$
      \theta_{\text{deg}} = \theta \cdot \left( \frac{180}{\pi} \right)
      $$

      After averaging a short window of tilt measurements, the robot checks if the orientation falls within certain thresholds:

      **Blue side under** if:

      $$
      \theta_{\text{deg}} \in [-179^\circ, -162^\circ] \cup [167^\circ, 179^\circ]
      $$

      **Yellow side under** if:

      $$
      \theta_{\text{deg}} \in [0^\circ, 15^\circ] \cup [-23^\circ, 0^\circ]
      $$


      Depending on the orientation, the system issues a movement command like `rfy` (roll forward with yellow side propulsion) or `rfb` (roll forward with blue side propulsion).

      The system runs in real time and adjusts its propulsion mode dynamically based on IMU feedback.

  - section_layout: text
    content: |
      ## NODES

      The bowling task is divided into several subsystems:

      **Control (Action Server and Client Nodes)**  
      These nodes update the robot's state (`TURNING`, `STOPPING`, `TRANSFORM TO ROLLING`, `ROLLING`, etc.) based on the number of detected bowling pins and publish the corresponding robot configuration for the Motor Control Node to set the DXL motors.

      **Computer Vision (YOLO Node)**  
      This node processes data from the camera and counts the number of bowling pins, publishing the result to a topic.

      **Dynamixel Motor Control (Quad Motor Control Node)**  
      This node controls the motors based on the robot's state and processes IMU data to determine tilt angles during ROLLING mode.

  - section_layout: 1col
    images:
      - caption:
        description: 'Newspaper magazine'
        url: '/projects/quad/quad-diagram.png'
        width:
        height:

  - section_layout: text
    content: |
      **AUTONOMOUS BOWLING SEQUENCE**

      - The robot begins turning while simultaneously scanning for bowling pins. 
      - There is a 7-second pause between turns.
      - If the robot detects at least two pins continuously for 3 seconds, it transitions to rolling mode.
      - Once in rolling mode, it reads IMU data and uses the acceleration of the Z and Y axes to determine tilt angles around the X-axis, then rolls forward.
  

  - section_layout: text
    content: |
      ## DEMO

  - section_layout: 1col
    images:
      - caption: Bowling Demo
        description: 'Newspaper magazine'
        url: '/projects/quad/quad_bowling.gif'
        width:
        height:

  
---
