---
date: 2024-09-28
published: true
title: "Pen Stealer"
description: "Python, OpenCV, Manipulation"
categories: branding, digital
technologies: Python, OpenCV, Manipulation
media: Book
ownership: Personal
client:
time_period: 2024
thumbnail: "/projects/pen/pen.gif"
ready: true

intro: |
  As part of the MSR Hackathon challenge, I used the Intel RealSense Camera and OpenCV techniques to detect the position of a purple pen and programmed the PincherX 100 robot to autonomously grab it.

content_layout:
  - section_layout: text
    content: |
      ## DEMO

  - section_layout: 1col
    images:
      - caption: 
        description: 'quad block diagram'
        url: '/projects/pen/pen.gif'
        width:
        height:

  - section_layout: text
    content: |
      ## COMPONENTS

      - Trossen PincherX 100
      - Intel RealSense Depth Camera D435i

  - section_layout: text
    content: |
      ## VISION PIPELINE
      - Process the RGB image to locate the pen in 2D space.
      - Use trackbars to identify the Hue, Saturation, and Value (HSV) colorspace of the color purple.
      - Generate an HSV mask and use contour detection to isolate the pen in the image.
      - If multiple contours are detected, select the one with the largest area to eliminate noise.
      - Calculate the centroid of the selected contour as the 2D location of the pen in pixels.
      - Use the camera’s intrinsic parameters to convert the 2D pixel coordinates into real-world coordinates (in meters) using the depth map.
      - Output the pen’s location relative to the camera frame.

  - section_layout: 1col
    images:
      - caption: 
        description: 'quad block diagram'
        url: '/projects/pen/pen-recognition.gif'
        width:
        height:

  - section_layout: text
    content: |
      ## CALIBRATION

      **Calculating the pen’s position in the robot’s frame:**

      - Use the `interbotix_xs_toolbox`, a Python API that integrates with ROS2, to control the robot.
      - Write different modes to control the robot’s actions:
        - Opening/closing the grippers
        - Moving forward/backward
        - Moving up/down
        - Rotating the arm about its base
      - Use these modes to evaluate the robot’s workspace limitations (e.g., singularities, joint limits, torque limits).
      - Find the transformation (translation and rotation) between the camera's coordinate frame and the robot's coordinate frame:
        - Collect data points where the end-effector is at known locations relative to both the robot base and the camera.
        - Use these data points in the camera frame and the robot frame to compute the transformation.
      - Apply the computed transformation to the pen's position (camera frame) to convert it into the robot frame for motion commands.

  - section_layout: text
    content: |
      ## ROBOT CONTROL

      - Set the robot to its ready position.
      - Open the grippers.
      - Detect the pen location using the vision pipeline.
      - Rotate the robot's waist until the end-effector is facing the pen.
      - Move forward until the pen is within the grippers’ grasp.
      - Close the grippers to grab the pen.
---
