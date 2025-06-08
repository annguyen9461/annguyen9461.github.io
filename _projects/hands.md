---
date: 2024-03-14
published: true
title: "Clash of Hands"
description: "C++, Python, Computer Vision"
categories: branding, digital
technologies: C++, Python, Computer Vision
media: Book
ownership: Personal
client:
time_period: 2025
thumbnail: "/projects/hand/hands.gif"

website:
  button_text: Github
  url: https://github.com/rdlynx19/clash-of-hands
      
intro: |
  We programmed the Allegro Hand to play rock-paper-scissors using machine learning strategies that help it get smarter with every game.

  **Team Member:** Pushkar Dave
content_layout:
  - section_layout: text  
    content: |
      ## DEMO
      
      <video controls style="width: 100%; height: auto;">
      <source src="/videos/clash-of-hands.mp4" type="video/mp4">
      Your browser does not support the video tag.
      </video>

  - section_layout: text
    content: |
      ## OVERVIEW

      - **Real-time Gesture Recognition:** Uses MediaPipe to detect rock, paper, and scissors from live webcam input.
      - **AI Agents:** Markov Model, Decision Tree
      - **Robotic Hand Integration:** Controls an Allegro robotic hand via CAN bus to perform AI moves.
      - **Game History Tracking:** Logs game data for ongoing learning and behavior prediction.
  
  - section_layout: text
    content: |
      ## AI AGENTS

      **Markov Transition Matrix**
      - Tracks transition probabilities between player moves.
      - Predicts the next move based on the last move's transition matrix.

      **Decision Tree**
      - Uses features like previous move frequency and patterns.
      - Trains a decision tree to predict the player’s next move and respond optimally.

  - section_layout: text
    content: |
      ## GESTURE RECOGNITION

      The system classifies hand gestures using MediaPipe Hands:
      - **Closed Fist** → Rock
      - **Open Palm** → Paper
      - **Victory Sign** → Scissors

  - section_layout: text
    content: |
      ## HARDWARE COMPONENTS

      - Allegro Hand V4
      - CAN interface and controller

---
