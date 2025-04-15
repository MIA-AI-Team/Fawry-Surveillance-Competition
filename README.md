# Fawry-Surveillance-Competition

This presents the official submission of the **MIA AI 25 team** for the tasks of **Face ReIdentification** and **Pedestrian Tracking** for the Fawry competition.

## Table of Contents
- [Overview](#overview)
- [Models](#models)
- [Face ReIdentification](#face-reidentification)
- [Pedestrian Tracking](#pedestrian-tracking)
- [Submission](#submission)

## Overview

In this repository you will find the models used for the tracking task, as well as a detailed walkthrough of each step of our solution. Each section below contains links to corresponding notebooks and resources that offer an in-depth explanation of our methods and implementation details.

## Models

Access our pre-trained models' weights from the following links:

- **[Tracking <sub>Models</sub>](https://www.kaggle.com/models/youssifkhale/fawry-models/)**
- **[Face ReIdentification <sub>Model</sub>](https://www.kaggle.com/models/mohamedbassat/face-recognition-fourier-model/)**

## Face ReIdentification

Including the kaggle notebook for the face recognition task, and the cleaned data used for training the model as well as the cleaned aligned data used directly for the inference task.

- **[Face ReIdentification <sub>Notebook</sub>](https://www.kaggle.com/code/mohamedbassat/face-recognition-ultimate) ⌈*[Documentation]()*⌉**
- **[Cleaned <sub>Dataset</sub>](https://www.kaggle.com/datasets/youssifkhale/clean-faces/data)**
- **[Cleaned Aligned <sub>Dataset</sub>](https://www.kaggle.com/datasets/mohamedbassat/cleaned-aligned-faces/data)**

## Pedestrian Tracking

We divide our work on the pedestrian tracking task into two main parts: **Training** and **Inference**. The training part includes the training of the YoloX model for object detection and the FastReID model for person re-identification. The inference part includes the usage of AdapTrack and BoostTrack models.

- **Inference**
  - **[AdapTrack <sub>Kaggle</sub>](https://www.kaggle.com/code/youssifkhale/fawry-adaptrack-inference)  ⌈*[Documentation]()*⌉**
  - **[BoostTrack <sub>Kaggle</sub>](https://www.kaggle.com/code/youssifkhale/fawry-boosttrack-inference)  ⌈*[Documentation](Documentation/BoostTrack.md)*⌉**
- **Training**
  - **[YoloX <sub>Kaggle</sub>](https://www.kaggle.com/code/youssifkhale/yolox-trainer)  ⌈*[Documentation]()*⌉**
  - **[FastReID <sub>Collab</sub>](https://colab.research.google.com/drive/1pKdfsoBmmbjCyE8hAkhxIYDPn0n9ONx7?usp=sharing)  ⌈*[Documentation](Documentation/FastReID.md)*⌉**

## Submission

Finally we provide a final notebook that includes the ensembling of the trackers and the generating of the final submission file.  

- **[Submission <sub>Notebook</sub>](https://www.kaggle.com/code/mohamedbassat/ensembling-of-trackers-and-submission/notebook) ⌈*[Documentation]()*⌉**
- **[Models' Output <sub>Dataset</sub>](https://www.kaggle.com/datasets/mohamedbassat/final-submission/data)**

---
