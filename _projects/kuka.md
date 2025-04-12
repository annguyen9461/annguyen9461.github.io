---
date: 2024-12-12
published: true
title: "KUKA youBot Mobile Manipulation"
description: "Python, Trajectory Planning, Manipulation, Feedforward Control"
categories: branding, digital
technologies: Python, Trajectory Planning, Manipulation, Feedforward Control
media: Book
ownership: Personal
client:
time_period: 2024
thumbnail: "/projects/kuka/youBot.gif"
ready: true

# website:
#   button_text: Github
#   url: https://github.com/annguyen9461/youBot-pick-and-place

intro: |
   In this project, I developed a full trajectory planning and control pipeline for the youBot mobile manipulator using Modern Robotics. The robot had to autonomously pick up a block from an initial position and drop it off at a final location in CoppeliaSim, with accurate grasping and movement under a physics engine.
   
   The system plans and follows a reference trajectory for the end-effector using kinematic simulation and feedback control. The output is a CSV file containing the robot’s full configuration (chassis pose, arm joints, wheel angles, gripper state) over time, which is used to animate and test the robot in CoppeliaSim's physics-based Scene 6.

content_layout:
  - section_layout: text  
    content: |
      ## DEMO

  - section_layout: 1col
    images:
      - caption: 
        description: 'quad block diagram'
        url: '/projects/kuka/youBot.gif'
        width:
        height:

  - section_layout: text  
    content: |
        ## ALGORITHM DESCRIPTION

        The system includes three main modules:
        - `NextState`: Simulates the next robot configuration based on the current configuration and commanded speeds using Euler integration.
        - `TrajectoryGenerator`: Builds the reference trajectory for the end-effector in task space, including 8 motion segments with associated gripper states.
        - `FeedbackControl`: Computes the end-effector twist command based on the error between the current and desired configurations using a feedforward plus proportional-integral (PI) controller.

  - section_layout: text  
    content: |
        ## TRAJECTORY GENERATOR: 8 STAGES

        The `TrajectoryGenerator` creates eight concatenated trajectory segments in SE(3), each starting and ending at rest:
        1. Move to standoff above initial block.
        2. Lower to grasp pose.
        3. Close gripper.
        4. Lift to standoff.
        5. Move to standoff above goal.
        6. Lower to place pose.
        7. Open gripper.
        8. Return to standoff.

        Each segment includes both rotational and translational interpolation, with 0.01s resolution.

  - section_layout: text  
    content: |
        ## INITIAL SETUP

        The initial end-effector pose is purposely offset by:
        - **0.2 m translation** in the X-axis
        - **30° rotation** about the Z-axis

        This ensures a meaningful starting error that the feedback controller must reduce over time.

        The initial configuration vector for the robot is:
        ```
        [chassis φ, x, y, J1-J5, W1-W4, gripper state]
        ```

  - section_layout: text  
    content: |
        ## FEEDFORWARD CONTROL

        The computed twist is mapped to wheel and joint velocities using the robot Jacobian:
        - The **base Jacobian** is derived using wheel geometry and screw theory.
        - The **arm Jacobian** is computed via `JacobianBody`.

        The combined Jacobian maps the desired twist to joint and wheel speeds using the pseudo-inverse.

        Velocity saturation ensures the commanded speeds stay within physical actuator limits.

  - section_layout: text  
    content: |
        ## RESULTS
  
  - section_layout: text  
    content: |
        <u>BEST CASE</u>
        <video controls style="width: 100%; height: auto;">
            <source src="/videos/kuka/best.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>

  - section_layout: 1col
    images:
      - caption: Best Case Error Plot
        description: 'Best Case Error Plot'
        url: '/projects/kuka/best-error-plot.png'
        width:
        height:

  - section_layout: text  
    content: |
        <u>OVERSHOOT CASE</u>
        <video controls style="width: 100%; height: auto;">
            <source src="/videos/kuka/overshoot.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>

  - section_layout: 1col
    images:
      - caption: Overshoot Case Error Plot
        description: 'Overshoot Case Error Plot'
        url: '/projects/kuka/overshoot-error-plot.png'
        width:
        height:


  - section_layout: text  
    content: |
        <u>NEW TASK</u>
        <video controls style="width: 100%; height: auto;">
            <source src="/videos/kuka/newTask.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>

  - section_layout: 1col
    images:
      - caption: New Task Error Plot
        description: 'New Task Error Plot'
        url: '/projects/kuka/newTask-error-plot.png'
        width:
        height:
    
---
