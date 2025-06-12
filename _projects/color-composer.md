---
date: 2024-09-27
published: true
title: "Color Composer"
description: "C, Embedded Systems, Microcontroller"
categories: branding, digital
technologies: C, Embedded Systems, Microcontroller
media: Book
ownership: Personal
client:
time_period: 2024
thumbnail: "/projects/color-composer/music-robot.gif"
ready: true

website:
  button_text: Github
  url: https://github.com/annguyen9461/color-composer

intro: |
  We built a differential drive robot that could be wirelessly controlled via a joystick and two Micro:Bits powered by the nRF52833 microcontrollers. As the robot drives over colors on the ground, it plays music notes that are associated with different colors.

  **Team Members:** Talia Ben-Naim, Natalie Hill
content_layout:
  - section_layout: text  
    content: |
      ## DEMO
      
      <video controls style="width: 100%; height: auto;">
      <source src="/videos/music-robot.mp4" type="video/mp4">
      Your browser does not support the video tag.
      </video>

  - section_layout: text
    content: |
      ## APPROACH

      **Inputs:**
      - Signal from the joystick
      - Color on the ground

      **Outputs:**
      - Driving direction
      - Music note

  - section_layout: 1col
    images:
      - caption: Block Diagram of the Interactions Between Subsystems
        description: 'block diagram'
        url: '/projects/color-composer/color-composer-diagram.png'
        width:
        height:

  - section_layout: text
    content: |
      **Project flow:**
      - The user controls the joystick. The x and y directions are encoded in radio packets with a password ("color composer") and sent from microbit1 (transmitter).
      - Microbit2 (receiver) decodes the packets and determines robot direction: forward, backward, forward left, forward right, backward left, or backward right.

      At the same time:
      - The color sensor reads the ground and outputs six color channels (Violet, Blue, Green, Yellow, Orange, Red).
      - These are decoded into a single color (e.g. Violet, Blue, Green, Yellow, Orange, Red, Brown, Black, White).
      - The associated frequency is played through the speaker.

  - section_layout: text
    content: |
      ## COMMUNICATION PROTOCOLS

      The joystick (microbit1) and robot (microbit2) communicate wirelessly using the 802.15.4 radio protocol. This allows real-time joystick control.

      The joystick, color sensor, and robot motors all use I2C (Inter-Integrated Circuit) for internal communication between components.

  - section_layout: text
    content: |
      ## MY TASKS

      - Process joystick input for wireless transmission
      - Implement robot control logic based on decoded joystick commands

  - section_layout: text
    content: |
      ## HANDLING JOYSTICK INPUT

      The joystick communicates with the nRF52833 microcontroller via I2C, using the nRF TWI Manager library to manage transactions. It outputs horizontal and vertical values.

      These values are encoded in radio packets as two 16-bit integers (x and y), each split into MSB and LSB. The joystick values are offset from the neutral center and placed in the payload after a password string to avoid interference from other microbits.

      **Reference:** [SparkFun Qwiic Joystick Arduino Library](https://github.com/sparkfun/SparkFun_Qwiic_Joystick_Arduino_Library)

  - section_layout: text
    content: |
      ## CONTROLLING THE MICROBIT ROBOT

      The receiving microbit decodes x and y joystick values by reconstructing the 16-bit integers from the MSB and LSB fields in the packet.

      Motor control is handled via the [SparkFun moto:bit - micro:bit Carrier Board](https://www.sparkfun.com/products/15713), which communicates via I2C. The `motor_drive` function writes speed and direction values to the controller, with helpers like `motor_forward` and `motor_reverse` simplifying motion commands.

      **Reference:** [Motobit MicroPython Library](https://github.com/hsshss/motobit-micropython/blob/master/motobit.py)

  - section_layout: text
    content: |
      ## HARDWARE COMPONENTS

      - [micro:bit V2 Board (nRF52833) (x2)](https://www.sparkfun.com/products/17287?gQT=2)
      - [SparkFun micro:bot kit for micro:bit - v2.0](https://www.sparkfun.com/products/16275)
      - [Adafruit AS7262 6-Channel Visible Light / Color Sensor Breakout](https://www.adafruit.com/product/3779)
      - [SparkFun Qwiic Joystick](https://www.sparkfun.com/products/15168)
      - [Speaker](https://www.adafruit.com/product/1313)

  - section_layout: 1col
    images:
      - caption: Hardware
        description: 'hardware'
        url: '/projects/color-composer/color-composer-components.png'
        width:
        height:

---
