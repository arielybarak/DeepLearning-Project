# Real-Time Audio-based Fall Detection (TinyML)

## Overview
We are building a **Real-Time Audio-based Fall Detection System** designed specifically for **showers and bathrooms**. 

This is a challenging task that involves distinguishing fall impacts from high-frequency water noise and echoes, currently without a dedicated dataset for this specific mission. The target platform for deployment is constrained edge hardware (ESP32-S3).

## Core Architecture & Research Plan
We will investigate variants of lightweight CNN/CRNN architectures suitable for TinyML applications on limited resources to process spectral features in real-time. Key architectures to be explored include:
- **YAMNet** (MobileNet-based)
- **PANNs** (Pre-trained Audio Neural Networks)
- **CRNN Variants**

Additionally, we plan to research a **calibration strategy** where a secondary sub-model learns room-specific masking and noise traits.

## Data Strategy
Since a dataset designed for this specific mission does not exist, we will construct one by augmenting public sources with synthetic environmental sounds.

- **Sources:** CAUCAFall, DESED, and repositories on Kaggle, Zenodo, Mendeley, and GitHub.

Our approach involves:
1. Utilizing pre-trained backbones.
2. Freezing early layers and fine-tuning the final layers for the bathroom acoustic environment.
3. Adapting these systems for deployment on constrained edge hardware (ESP32-S3).

## Resources
- **Edge Impulse:** MLOps platform for DSP and TinyML optimization.
- **Hugging Face:** Platform for accessing state-of-the-art pre-trained models.
