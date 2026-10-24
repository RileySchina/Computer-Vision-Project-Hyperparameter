# IAT 360: Computer Vision Project Proposal

**Group 7:** Haoyu Zhan, Leon Su, Mackenzie Scholz, Riley Schina

## Project Idea

**Cyclist Hand Signal Identification: Signal and Gesture Recognition for Autonomous Driving**

## Explaining the Idea

The main problem we hope to address is that drivers and driver-assistance systems, including autonomous-driving systems, may have difficulty understanding cyclists’ intentions. Collisions between cyclists and vehicles are a road-safety concern. A system that recognizes cyclists’ hand signals and tracks their approximate locations could help vehicles anticipate cyclists’ actions and potentially reduce the risk of accidents.

The model could potentially be integrated into or used alongside road-perception systems similar in purpose to Tesla’s Advanced Driver Assistance Systems (ADAS). This project is a prototype for cyclist detection and hand-signal recognition; it would not, by itself, establish that the system is safe for real-world driving.

## What Type of Computer Vision Problem Is This?

The project primarily involves **object detection and supervised classification**. Using labelled data, the model will identify cyclists and classify the hand signals they display to help infer their likely intentions.

The work may also involve:

- **Localization:** Identifying the approximate position of each cyclist in an image.
- **Object tracking (if video is used):** Following cyclists across video frames.
- **Gesture classification:** Classifying a cyclist’s visible signal into one of the dataset’s labelled categories.

Although the original proposal describes the task as binary object classification, the listed dataset contains multiple labels. The overall task is therefore better described as object detection with multi-class classification, depending on the model configuration and annotation format.

## Data: Uses and Access

### Data Source

[Roboflow Universe: Cycling Hand Signals Detection — Dataset Version 3](https://universe.roboflow.com/methods-of-research-l3ap3/cycling-hand-signals-detection/dataset/3)

We will use image data from a Roboflow project containing more than 7,000 images. If necessary, we may apply image transformations to increase the amount and variety of training data. Each group member will also contribute approximately 30 or more labelled images.

We have already downloaded both an untransformed dataset and a heavily transformed version from Roboflow. We will review the annotations and class distribution before training. We should also avoid placing duplicated or near-duplicated images in different training, validation, and test splits, as this could make the evaluation results appear better than they are.

### Labels and Categories

The dataset uses the following labels:

- Cyclist
- Giveway
- Left Turn
- Overtaking
- Right Turn
- Road Hazard
- Slow Down
- Stop

These labels come from the dataset and roughly follow cyclist hand signals used on roads in New Zealand. We will verify the dataset’s annotation definitions and spelling before training.

## Role Distribution and Timeline

### Weeks 1–2: Data Collection and Preprocessing

- **Riley and Leon:** Coordinate data collection and preprocessing, including cleaning up the dataset.
- **All group members:** Contribute at least 30 labelled images each.

### Weeks 2–3: Fine-Tuning

- **Leon:** Set up the base YOLO model.
- **All group members:** Tune their own hyperparameters and compare results.

### Week 3: Evaluation

- **Mackenzie and Haoyu:** Evaluate the model’s results.

### Week 3: Report

- **Mackenzie and Riley:** Summarize the results and findings.

### Weeks 3–4: Presentation and Final Report

- **Haoyu:** Handle video editing.

The group will coordinate to complete the presentation and final report.
