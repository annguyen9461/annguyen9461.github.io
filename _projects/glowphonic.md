---
date: 2024-12-11
published: true
title: "Glowphonic"
description: "C++, Max/MSP, Digital Music"
categories: branding, digital
technologies: C++, Max/MSP, Digital Music
media: Book
ownership: Personal
client:
time_period: 2025
thumbnail: "/projects/glowphonic/glow.gif"
ready: true

website:
  button_text: Github
  url: https://github.com/annguyen9461/glowphonic/
  

website:
  button_text: Github
  url: https://github.com/annguyen9461/glowphonic/
  
intro: |
  *Glowphonic* is an interactive digital musical instrument with touch-sensitive petals for playing notes and a 6-DOF IMU that modulates tremolo. It features responsive lighting that blinks to touch or audio amplitude, with sensor data sent to Max/MSP and synchronized visuals controlled by an ESP32.

content_layout:
  - section_layout: text  
    content: |
      ## DEMO

      <video controls style="width: 100%; height: auto;">
      <source src="/videos/glowphonic.mp4" type="video/mp4">
      Your browser does not support the video tag.
      </video>

  - section_layout: text
    content: |
      ## HARDWARE OVERVIEW

      Glowphonic integrates multiple sensors and microcontrollers:

      - **12-Key Capacitive Touch Sensor**: Plays notes from two keyboards via Max/MSP.
      - **6-DOF IMU**: Tilting forward (x-axis) increases the tremolo of an audio sample.
      - **Slide Potentiometer**: Controls keyboard volume.
      - **Ultrasonic Distance Sensor**: Controls sample loop speed—closer distances loop faster.

      Sensor readings are collected by an Arduino Nano and sent to Max/MSP over serial USB. Max interprets this data and sends visual triggers—such as note activations or amplitude spikes—via a second serial connection to an ESP32-S3. The ESP32-S3 controls a NeoPixel LED strip, blinking in response to these events to create synchronized light feedback.

  - section_layout: text
    content: |
      ## DESIGN

      The electronics are mounted inside a cherry blossom-style lampshade. The touch wires extend to the petals using conductive tape, turning them into large capacitive surfaces. The distance sensor is mounted at the top to remain unobstructed.

  - section_layout: 1col
    images:
      - caption: Circuit Diagram for Sensor Readings
        description: 'Sensor interface diagram'
        url: '/projects/glowphonic/music-circuit1.png'

  - section_layout: 1col
    images:
      - caption: Circuit Diagram to Blink LED Lights
        description: 'LED control circuit'
        url: '/projects/glowphonic/music-circuit2.png'

  - section_layout: 1col
    images:
      - caption: Max Code Annotations
        description: 'Max Code'
        url: '/projects/glowphonic/max-code-annotations.png'

  - section_layout: text
    content: |
      ## BUILD

  - section_layout: 2col
    images:
    - caption: Interior
      description: 'Interior'
      url: '/projects/glowphonic/glow-interior1.png'
      width:
      height:
    
    - caption: Full Build
      description: 'Full Build'
      url: '/projects/glowphonic/glow-interior2.png'
      width:
      height:

  - section_layout: 1col
    images:
    - caption: Glowing
      description: 'Interior'
      url: '/projects/glowphonic/glow-build1.png'
      width:
      height:

  - section_layout: text
    content: |
      ## INSPIRATION

      *Glowphonic* was inspired by Jonathan Sparks’ <a href="https://jonathansparks.com/nomis/" target="blank">*NOMIS*</a>, winner of the 2015 Guthman People's Choice Award, which produced melodies and layered glowing loops via gesture and light.

  - section_layout: text
    content: |
      ## REFERENCES

      - [Tremolo Effect in Max/MSP](https://music.arts.uci.edu/dobrian/maxcookbook/tremolo-effect-sound-file)
      - [NeoPixel LED Guide](https://learn.adafruit.com/adafruit-neopixel-uberguide/basic-connections)
      - [Ultrasonic Sensor Tutorial](https://www.instructables.com/Simple-Arduino-and-HC-SR04-Example/)
      - [MPR121 Capacitive Touch Sensor Guide](https://learn.adafruit.com/adafruit-mpr121-12-key-capacitive-touch-sensor-breakout-tutorial)
      - [Music Samples](https://samplefocus.com/)

  - section_layout: text
    content: |
      ## HARDWARE COMPONENTS

      - [Arduino Nano](https://store.arduino.cc/products/arduino-nano)
      - [ProS3 - ESP32-S3 Development Board](https://www.adafruit.com/product/5401)
      - [Ultrasonic Distance Sensor (x4)](https://www.adafruit.com/product/4019)
      - [Adafruit 12-Key Capacitive Touch Sensor Breakout](https://www.adafruit.com/product/1982)
      - [Adafruit ISM330DHCX 6-DOF IMU](https://www.adafruit.com/product/4502)
      - [Slide Potentiometer](https://www.adafruit.com/product/5295)
      - [Adafruit NeoPixel Digital RGB LED Strip](https://www.adafruit.com/product/1138)
      - [Cherry Blossom Lampshade](https://www.amazon.com/dp/B07MRL3FK2)

      **Other materials**:
      - USB-C to USB-C cables (x2)
      - 5V 5A AC to DC Power Supply for LEDs
      - Copper Conductive Tape
      - Jumper Wires (50cm)

---
