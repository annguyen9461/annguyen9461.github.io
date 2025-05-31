---
date: 2024-12-14
published: true
title: "The Poolinator"
description: "Python, ROS2, MoveIt, OpenCV"
categories: branding, digital
technologies: Python, ROS2, MoveIt, OpenCV
media: Book
ownership: Personal
client:
time_period: 2024
thumbnail: "/projects/poolinator/pool2.gif"

website:
  button_text: Github
  url: https://github.com/annguyen9461/poolinator

intro: |
  The Franka Emika Panda 7-DoF arm plays a game of pool by identifying balls and hitting them into pockets.

  **Team Members:** Caroline Terryn, Catherine Maglione, Joseph Blom, Logan Boswell


content_layout:
  - section_layout: text  
    content: |
      ## DEMO
      
      <video controls style="width: 100%; height: auto;">
      <source src="/videos/pool-demo.mp4" type="video/mp4">
      Your browser does not support the video tag.
      </video>

  - section_layout: text
    content: |
      ## PROJECT SEQUENCE
      <ul>
        <li>The game begins with the robot arm moving to the side to avoid obscuring the table.
        </li>
        <li>The camera detects two AprilTags to determine the transformations of the table, the cue, the end-effector, and the camera, all relative to the base of the Franka.
        </li>
        <li>The locations of the cue ball (red) and other balls (blue) are updated, and these coordinates are fed into the pool algorithm.
        </li>
        <li>The robot selects a striking position that enables it to hit the cue ball and pocket another ball.
        </li>
        <li>After striking, the robot arm moves to the side again to update the new positions of the balls.
        </li>
        <li>The game continues until all the blue balls are pocketed.
        </li>
        <li>Then the robot hits the red ball into a pocket to end the game.
        </li>
      </ul>

  - section_layout: 1col
    images:
      - caption: Best Strikes
        description: 'Best Strikes'
        url: '/projects/poolinator/pool.gif'
        width:
        height:

  - section_layout: text
    content: |
      ## NODES AND PYTHON MODULES

      The project is divided into several subsystems:

      <dl>
        <dt><strong>AprilTags (Transform Node)</strong></dt>
        <dd>
          This node uses the table tag and the cue tag to establish the relationship between various coordinate frames (camera, end-effector, table, etc.) to build a TF tree.
        </dd>
        <br>

        <dt><strong>Computer Vision (Image Processing Node)</strong></dt>
        <dd>
          This node processes data from the depth camera and camera info topics to locate the cue ball (red ball) and other balls on the pool table. It integrates OpenCV and ROS2 for image processing and publishes the detected ball positions as TF frames for use in robot control and planning.
        </dd>
        <br>

        <dt><strong>Planning & Execution (Control Node)</strong></dt>
        <dd>
          This node manages the robot's movements through various states, such as striking, standby, and home positions.
        </dd>
        <br>

        <dt><strong>Pool Algorithm</strong></dt>
        <dd>
          This Python module uses ball coordinates to plan feasible striking positions for the robot.
        </dd>
        <br>

        <dt><strong>World</strong></dt>
        <dd>
          This Python module represents the environment, including the table, Franka's platform, and the ceiling-mounted camera. It ensures the robot's path planning avoids obstacles by maintaining spatial relationships and tracking key elements like table corners, pockets, and ball positions using TF transforms.
        </dd>
      </dl>
  
  - section_layout: 1col
    images:
      - caption: Block Diagram of the Interactions Between        Subsystems
        description: 'Block Diagram of the Interactions Between Subsystems'
        url: '/projects/poolinator/poolinator-diagram.png'
        width:
        height:

  - section_layout: text
    content: |
      ## CUSTOM ROS2 MOVEIT API

      Prior to this project, our team developed a custom MoveIt API to help the Franka arm plan trajectories and control its movements. Key features include:

      **Pose-based Planning**  
      Plan trajectories to reach specific end-effector poses, such as the strike position or standby position.

      **Joint State Planning**  
      Plan trajectories to move the robot to predefined joint configurations.

      **Cartesian Path Planning**  
      Plan linear motions for tasks like moving the end-effector along the x-axis during a cue strike.

      **Inverse Kinematics**  
      Convert desired end-effector poses into joint configurations for precise execution.

      **Planning Scene Setup**  
      Create a planning scene with obstacles like the table and camera to ensure collision-free paths.

  - section_layout: text
    content: |
      ## COMPUTER VISION (IMAGE PROCESSING NODE)

  - section_layout: 2col
    images:
    - caption: Red Ball Contour
      description: 'Red Ball Contour'
      url: '/projects/poolinator/red_ball_rviz_contour.gif'
      width:
      height:
    
    - caption: Real-time Image Streaming
      description: 'Real-time Image Streaming'
      url: '/projects/poolinator/red_ball_rviz_image.gif'
      width:
      height:

  - section_layout: text
    content: |
      I developed the image processing node using the Intel RealSense camera to detect the 3D positions of pool balls. These positions were used to guide the robot in planning strike trajectories.

      The image pipeline focused on detecting red (cue ball) and blue (target balls) using **HSV-based color segmentation**. I filtered contours based on size to remove noise and computed the center of mass to extract x and y positions.

      For depth (z), I used the depth stream from the RealSense camera and converted pixel coordinates into real-world metric positions using intrinsic parameters from the `camera_info` topic.

      I then broadcasted each ball’s position as a **TF frame** relative to the robot's base frame, enabling the control nodes to access their live positions.

---
