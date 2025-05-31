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
thumbnail: "/projects/hand/hand.gif"

website:
  button_text: Github
  url: https://github.com/rdlynx19/clash-of-hands
      
intro: |
  We made the Allegro Hand to play rock-paper-scissors using strategies like a decision tree classifier and a Markov model, enabling the AI to get better over time by learning from previous games.

  **Team Member:** Pushkar Dave
content_layout:

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

      **Markov Agent**
      - Tracks transition probabilities between player moves.
      - Predicts the next move based on the last move's transition matrix.

      **Decision Tree Agent**
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

      - Allegro Robotic Hand
      - CAN interface and controller
      
---
