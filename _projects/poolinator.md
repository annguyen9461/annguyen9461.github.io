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
  url: https://github.com/ME495-EmbeddedSystems/finalproject-jrblom2

intro: |
  The Franka Emika Panda 7-DoF arm plays a game of pool by identifying balls and hitting them into pockets.

  <u>Team Members:</u> Caroline Terryn, Catherine Maglione, Joseph Blom, Logan Boswell


content_layout:
  
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
---
