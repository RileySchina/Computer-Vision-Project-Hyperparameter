IAT360 Computer Vision Projection

Group 7: Haoyu Zhan, Leon Su, Mackenzie Scholz, Riley Schina
Project Idea: Cyclist hand signal Identification
Signal/gesture recognition for autonomous driving
 

Explaining the idea

The main problem we are hoping to solve is poor understanding of cyclist intentions for drivers and driver assistant programs, such as autonomous driving. Accidents between cyclists and vehicles are quite common, so by creating a system to help identify cyclist intent through hand signals and help track the rough location of cyclists will help reduce those accidents. The model could be applied to or integrated into road recognition systems similar to the Tesla ADAS (Advanced Driver Assistant System).

 

What type of computer vision problem?

This problem will mostly be a binary object classification problem, using supervised learning with labelled data to determine the presence of cyclists and any hand gestures they are using to help determine their intent.




Data: Uses and Access

 

Data Source

https://universe.roboflow.com/methods-of-research-l3ap3/cycling-hand-signals-detection/dataset/3Links to an external site. 

We will be using image data from a Roboflow project containing 7000+ images, plus potentially applying transformations to the images to increase our dataset size if necessary. Additionally we will be adding roughly 30+ images each to increase our dataset. We have already downloaded an untransformed dataset, and a heavily transformed dataset from Roboflow.

 

Labels/Categories:

Cyclist, Giveway, Left Turn, Overtaking, Right Turn, Road Hazard, Slow Down, Stop

 

These labels come from the dataset, and roughly follow the hand signals used in New Zealand for cyclists on the road.




Role Distribution 

 

Week 1-2

Data collection and preprocessing: clean up data

Riley
Leon
Everyone will also contribute 30+ labeled images
Week 2-3

Fine-tuning: optimize our YOLO model

Leon (base model setup)
Everyone will also tune their own hyperparameter 
Week 3

Evaluation: evaluate model’s result

Mackenzie
Haoyu
Week 3

Report: sum up our results

Mackenzie
Riley
Week 3-4

Presentation and Final Report

Video editing: Haoyu
