# Hybrid Bandwidth Prediction for RTC Systems

 Code for paper titled: "__BoB: Bandwidth Prediction for Real-Time Communications Using Heuristic and Reinforcement Learning__", IEEE TMM.

This document provides instructions for reproducing the Bandwidth prediction in peer to peer connection (serverless) using AplhaRTC environment.

## Table of Contents
1. [Context](#context)
    <!-- - [Problem Statement](#problem-statement)
    - [Traditional Approches](#traditional-approaches)
    - [The BoB Model](#the-bob-model)
    - [Key Features](#key-features)
    - [Benefits](#benefits)
    - [Applications](#applications)
    - [Conclusion](#conclusion) -->
2. [Suitable Operating Systems](#suitable-operating-systems)
3. [System Requirements](#system-requirements)
4. [Prerequisites](#prerequisites)
5. [Getting Started](#getting-started)
   <!-- - [Clone the BoB repository](#clone-the-bob-repository)
   - [Pull the Docker image of the challenge environment](#pull-the-docker-image-of-the-challenge-environment)
   - [Download the configuration and test media](#download-the-configuration-and-test-media) -->
6. [Running BoB model](#running-bob-model)
7. [Traffic Profiles in BoB Model Experiment](#traffic-profiles-in-bob-model-experiment)
7. [Results](#results)
8. [Notes](#notes)
   <!-- - [script (run_with_tc.sh)](#script-run_with_tcsh)
   - [Issues](#issues) -->

## Context

### Problem Statement
In real-time communication (RTC) systems, fluctuating bandwidth can lead to poor user experience. Predicting bandwidth accurately can help ensure smooth communication and optimize resource allocation.

### Traditional Approaches
Existing methods for bandwidth prediction often rely on statistical models or machine learning algorithms. However, these methods may not be able to capture the dynamic nature of network traffic and user behavior effectively.

### The BoB Model
The BoB model (Bandwidth Prediction for Real-Time Communications using Heuristic and Reinforcement Learning) proposes a hybrid approach that combines heuristic methods with reinforcement learning to achieve accurate and dynamic bandwidth prediction.

### Key Features
- **Heuristic Methods:** Leverage domain knowledge to extract features from network traffic and user behavior for short-term bandwidth prediction.
- **Reinforcement Learning:** Utilizes an agent that interacts with the network environment, learning to predict bandwidth based on received rewards. This enables adaptation to changing network conditions and user behavior.

### Benefits
- **Improved Accuracy:** By merging heuristic methods and reinforcement learning, the BoB model achieves superior bandwidth prediction compared to traditional approaches.
- **Dynamic Adaptation:** Adapts to changes in network conditions and user behavior, enhancing prediction accuracy over time.
- **Resource Management:** Enables efficient resource allocation in RTC systems, improving overall performance.

### Applications
- **Video Conferencing:** Maintains video quality and avoids disruptions during conferences by predicting bandwidth fluctuations.
- **Online Gaming:** Ensures smooth gameplay and minimizes delays and lag through accurate bandwidth prediction.
- **Streaming Services:** Optimizes content delivery and prevents buffering by forecasting bandwidth demand.

### Conclusion
The BoB model offers a promising approach for accurate and dynamic bandwidth prediction in RTC systems. It contributes to improved user experience and efficient resource management, benefiting various applications such as video conferencing, online gaming, and streaming services.



## Suitable Operating systems
- MacOs with intel chip 
- Linux
#### One of these operating system is mandatory to setup environment

## System Requireents
- 8 GB RAM
- 256 GB ROM


## Prerequisites
- Docker installed and running on your system.
- Git installed and configured.
- Basic understanding of Dockerfile and bash scripting.
- Python installed and running on your system.



## Getting Started
### Clone the BoB repository:
```bash
git clone https://github.com/NUStreaming/BoB
```

### Pull the docker image of challenge environment
```bash
docker pull opennetlab.azurecr.io/challenge-env
```

### Download the configuration and test media
```bash
wget https://raw.githubusercontent.com/OpenNetLab/AlphaRTC/main/examples/peerconnection/serverless/corpus/receiver_pyinfer.json -O receiver_pyinfer.json
wget https://raw.githubusercontent.com/OpenNetLab/AlphaRTC/main/examples/peerconnection/serverless/corpus/sender_pyinfer.json -O sender_pyinfer.json
mkdir testmedia
wget https://github.com/OpenNetLab/AlphaRTC/raw/main/examples/peerconnection/serverless/corpus/testmedia/test.wav -O testmedia/test.wav
wget https://raw.githubusercontent.com/OpenNetLab/AlphaRTC/main/examples/peerconnection/serverless/corpus/testmedia/test.yuv -O testmedia/test.yuv
```
#### We can see files in the BoB folder

# Running BoB model
- First build the environment in environment folder by `make all`
- run ./run_with_tc in the parent folder.
- This will create results folders with audio files, graphs and log files.

# Traffic Profiles in BoB Model Experiment

In the BoB model experiment, various traffic profiles are used to evaluate the model's performance under different network conditions. Here's a brief explanation of each profile:

1. **lte_profile_x0.25:** Simulates a mobile network with a 25% bandwidth reduction to represent typical LTE network conditions.
2. **cascade_profile_x0.25:** Simulates a network with cascading congestion, where congestion occurs at multiple points in the network path, leading to unpredictable bandwidth fluctuations.
3. **twitch_profile_x0.25:** Emulates the traffic patterns of Twitch streaming, characterized by high bandwidth demands and frequent bursts of data.
4. **FCCamazone_x0.25:** Replicates the network conditions experienced during the FCC Amazon data transfer experiment, representing a real-world scenario with complex traffic patterns.
5. **Synthtic_x0.25:** A synthetically generated traffic profile used to stress test the model and assess its performance under extreme conditions.

These profiles represent different network scenarios commonly encountered in real-world RTC applications. By testing the BoB model on these profiles, researchers can evaluate its ability to adapt to diverse network conditions and ensure accurate bandwidth prediction for various applications.

# Results
- We get 4 results folders one for each model and each folder contain audio.wav,audio.json, bandwidth_estimator.log and graph files.
- Log file will have the content of actual bandwidth and estimated bandwidth along with weather the heauristic model is used or not.

# Notes
## script (run_with_tc.sh)
- run_with_tc.sh is a shell script which handles whole execution of project.
- Traffic profiles of lte_profile_x0.25 cascade_profile_x0.25 twitch_profile_x0.25 FCCamazone_x0.25 Synthtic_x0.25 are used for execution.
- The script runs for bob, gemini, heuristic and hrcc models.

## Issues
- Phantom container blocking to create new container then use rm command to remove the container which it gives in terminal
```bash
docker rm <container_name_or_id>
```
- Sometimes we get receiver_pyinfer.json is not in path then we can change the path of it from cmdinfer file in docker container.