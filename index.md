---
layout: home
title: Shark vs Dolphin Classification
nav_order: 1
---

# Shark vs Dolphin Classification from Drone Images

## Problem Overview

This project focuses on automatically classifying **overhead drone images** as either **shark** or **dolphin**. From above, sharks and dolphins can look very similar, especially in low-resolution or noisy images. Misidentifications can lead to:

- **Unnecessary beach closures**
- **Missed shark sightings**
- **Increased workload and stress** for human lifeguards and spotters

An automated computer vision system can help analyze incoming drone footage and flag potential sharks more reliably and consistently.

## Why This Matters

- **Public safety:** Accurate detection of sharks can help protect swimmers and surfers.
- **Reducing false alarms:** Dolphins are common near shore and are often mistaken for sharks.
- **Scalability:** Drones can cover large areas; a model like AlexNet can assist with real-time classification.
- **Cost-effective:** Once trained, models can run continuously without fatigue, unlike human observers.

## Dataset Description

The dataset consists of overhead drone images, organized into separate training and validation sets:

- **Training set:** 138 images  
- **Validation set:** 39 images  
- **Classes:**
  - `Dolphin`
  - `Shark`

Images vary in:

- Lighting conditions
- Water color and clarity
- Animal orientation and distance from the drone

The dataset is structured as:

```text
train/
    Dolphin/
    Shark/
valid/
    Dolphin/
    Shark/
