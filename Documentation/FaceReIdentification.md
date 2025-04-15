# Face ReIdentification Pipeline Guide ⌈*[Notebook](https://www.kaggle.com/code/mohamedbassat/face-recognition-ultimate)*⌉

## Table of Contents
- [Overview](#overview)
- [Data Preparation](#data-preparation)
- [Model Setup](#model-setup)
- [Model Training](#model-training)
- [Model Inference](#model-inference)

## Overview

This guide explains how to use the accompanying Kaggle notebook for face reidentification. The solution utilizes a ResNeXt backbone, SphereFace2 loss combined with Focal Loss, MTCNN for face alignment, and a novel Fourier transform preprocessing step. It covers both training the model from scratch and running inference using a pre-trained model.

**Note:** The cells/blocks of the notebook should generally be run in order to avoid errors, especially ensuring dependencies are installed and data is prepared before training or inference.

## Data Preparation
This section preprocesses the input images by aligning faces using MTCNN.

- **Action:** *(Run the cells under the "Alligning Faces using MTCNN" markdown header).*
- **Process:**
  - The cells will load the raw face images from the specified directories.
  - MTCNN will detect facial landmarks and rotate the images to align the eyes horizontally.
  - Aligned images will be saved to a new directory structure under `/kaggle/working/clean_aligned_faces/` (e.g., `/kaggle/working/clean_aligned_faces/train/` and `/kaggle/working/clean_aligned_faces/test/`).
   
## Model Setup
This section sets up the overall model architecture and the needed components.

- **Action:** *(Run the cells until the "Training Loop" markdown header).*

## Model Training
***OPTIONAL*** if needed to train from scratch using the aligned data and the custom 4-channel (RGB + Fourier) input and not use the attached pre-trained model.

- **Action:** *(Run the cells under the "Training Loop" markdown header).*
- **Process:**
  - Loads the aligned training data using the custom `FaceIdentificationDataset` which applies data augmentation and the Fourier transform.
  - Runs the training loop for a specified number of epochs "100" in the example, optimizing the model parameters.
  - Logs training progress using Wandb (if configured).
- **Output:**
-  Trained model checkpoints saved to `/kaggle/working/checkpoints/final_4channel_model.pth`.
-  Training history plot saved as `4channel_training_history.png`.
  
## Model Inference
This section describes how to generate predictions on the test set either using a pre-trained model or the model trained in the previous step.
1. **Using your trained Model**
   - **Action:** *(Run the cell 2nd to last).*
   - **Process:**
     - Loads the checkpoint we trained in the previous step.
     - Processes each test image: applies the 4-channel transform (including Fourier if applicable during training, though the inference cell uses RGBA conversion), extracts features, calculates similarity scores against learned class weights.
     - Apply a confidence threshold (`FIXED_THRESHOLD = 0.26` in the notebook) to classify faces. Predictions below the threshold are marked as "unknown".
2. **Using Our Pre-trained Model**
    - **Action:** *(Run the last cell under the title "to infere using our trained model").*
    - **Process:**
      - Same as above but loads the pre-trained model checkpoint provided as a Kaggle model input.
---