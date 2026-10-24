# IAT 360: Computer Vision Projection

**Group 7:** Haoyu Zhan, Leon Su, Mackenzie Scholz, Riley Schina

## Project Title

**Cyclist Hand Signal Identification: Signal and Gesture Recognition for Autonomous Driving**

## Target Signals

The system will identify the following cyclist hand signals:

- Right Turn
- Alternative Right Turn
- Left Turn
- Slowing Down
- Stopped

## Explain the Idea

The main idea of this project is to adapt the original YOLO real-time object detection system to focus on detecting cyclists’ hand signals for autonomous driving systems. The trained network will go beyond basic object identification and attempt to recognize cyclists’ intentions.

The goal is to support safer interactions between autonomous vehicles and cyclists, contributing to safer road conditions for both.

## What Type of Computer Vision Problem Is This?

The project may involve the following computer vision tasks:

- **Object detection and classification:** Detect cyclists and classify their hand signals.
- **Object tracking:** Track cyclists across video frames to understand continuous motion and changes in gestures.
- **Localization:** Locate cyclists in the image and estimate their positions relative to the camera.
- **Instance segmentation (optional):** Separate individual cyclists from the background and from one another, if required by the project scope.

In complicated real-world traffic scenarios, multiple cyclists may travel in different directions and may be stationary or moving. Detecting and tracking cyclists can help the system distinguish individuals and interpret their signals.

Localization can help estimate the number of cyclists and their positions. Combined with tracking and gesture recognition, this information may help the system reason about each cyclist’s direction of travel and possible intentions. Estimating distance accurately would require appropriate camera calibration or additional depth information.

This project will use **supervised learning**, with labelled training images. The proposed pipeline has two main stages:

1. Detect cyclists in images or video.
2. Recognize their turn signals or other intentions from their hand gestures.

Depending on the chosen YOLO model and dataset, cyclist detection and signal classification may be performed in one model or in separate stages.

## What Type of Data Will Be Needed, and How Will It Be Collected?

We will need images and videos of cyclists with varied appearances and riding conditions. Ideally, the data will represent different ages, genders, ethnic backgrounds, clothing, environments, and camera viewpoints, as well as different times of day, terrains, weather, and traffic conditions.

### Labels and Categories

The target signal categories are:

- Right Turn
- Alternative Right Turn
- Left Turn
- Slowing Down
- Stopped

The dataset should also support cyclist detection. If a cyclist is not displaying one of the target signals, that situation should be handled consistently—for example, with an additional `No Signal` or `Other` class if the project scope and dataset support it.

### Data Source

[Roboflow Universe: Cycling Hand Signals Detection](https://universe.roboflow.com/methods-of-research-l3ap3/cycling-hand-signals-detection/dataset/3)

The dataset source describes a collection of more than 7,000 images concerning cycling hand gestures. It also reports that transformations, such as duplication and inversion, have expanded the dataset to more than 30,000 images. The dataset is available for download through Roboflow Universe and includes a YOLO-compatible export option.

Before training, we should inspect the dataset’s labels, class distribution, licensing and usage terms, and the quality of its annotations. We should also check for duplicated or near-duplicated images across the training, validation, and test sets to avoid overly optimistic evaluation results.

## Task Distribution

The project work will be divided into the following areas:

- Data collection and dataset preparation
- Data labelling and annotation review
- Model fine-tuning and training
- Hyperparameter tuning
- Evaluation and report writing

### Individual Contribution

Each group member needs to contribute to:

- Creating or collecting additional data
- Hyperparameter tuning

### Optional Extension

- Train and evaluate a pose-estimation model.

## Challenges and Possible Future Directions

Clothing, weather, terrain, camera angles, lighting, and other environmental factors can make cyclists and their gestures difficult to recognize. Some situations may be challenging even for human observers. These conditions should be considered when preparing the dataset and evaluating model performance.

One possible approach is to divide difficult conditions into specialized recognition tasks—for example, detecting cyclists at night or from extreme camera angles—and compare specialized models with a single general-purpose model. A gating or model-selection system could route an image to an appropriate specialist. This idea would need further investigation and should be treated as an optional extension rather than a confirmed implementation plan.

Another possible direction is to detect rapid body gestures, such as extending an arm to signal a turn or stopping, convert the recognized gesture into a structured data message, and broadcast it to nearby vehicles. This could complement camera-based perception, but it would require suitable communication hardware and protocols, attention to latency and reliability, and safeguards against incorrect or spoofed messages.

The project’s primary focus remains cyclist hand-signal recognition using computer vision. The additional ideas are potential future improvements that could be explored if time and resources allow.
