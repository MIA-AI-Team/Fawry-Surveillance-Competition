# FastReID Training Guide ⌈*[Notebook](https://colab.research.google.com/drive/1pKdfsoBmmbjCyE8hAkhxIYDPn0n9ONx7?usp=sharing)*⌉

This guide provides a step-by-step explanation for setting up the environment, preprocessing the dataset, and training a pedestrian re-identification model using FastReID.

---

## Environment Setup

To ensure compatibility, we recommend using a Conda-based environment. Below are the setup steps:

1. **Mount Drive (for Google Colab):**  
   Used to save model weights after each epoch.

2. **Clone Repository and Navigate:**

   ```shell
   !git clone https://github.com/MIA-AI-Team/Fawry-Surveillance-Competition.git
   ```

3. **Install Conda Environment and Dependencies:**
   Follow the instructions within the notebook to install the required packages. You may be prompted to restart the session before continuing.

---

## Dataset Preparation

### 1. **Download the Dataset**

Use the [Kaggle API](https://www.kaggle.com/c/surveillance-for-retail-stores) to download the competition dataset.

### 2. **Preprocessing Steps**

- The dataset is renamed to match FastReID’s required format.
- True labels containing pedestrian IDs for each frame are extracted.
- For each ID, the bounding box in every frame is cropped and saved as a separate image.
- These images are grouped and sorted by pedestrian ID per video.

#### Preprocessing Script

The following command runs the preprocessing script:

```bash
!python /content/Fawry-Surveillance-Competition/Tracking/fast_reid/datasets/generate_mot_patches.py --data_path $LOCAL_DATA_PATH --dataset "MOT20" --save_path $LOCAL_SAVE_PATH
```

---

## Model Training

### A) Start Training from Scratch

This process uses pretrained FastReID embeddings (trained on the MOT17 dataset) as a starting point.

- **Pretrained Model Weights:**  
  [`mot17_sbs_S50.pth`](https://drive.google.com/drive/folders/1cCOx_fadIOmeU4XRrHgQ_B5D7tEwJOPx)

- **Training Command:**
  ```bash
  !python3 "/content/Fawry-Surveillance-Competition/Tracking/fast_reid/tools/train_net.py" --config-file "/content/Fawry-Surveillance-Competition/Tracking/fast_reid/configs/MOT20/sbs_S50.yml" MODEL.DEVICE "cuda:0"
  ```

---

### B) Resume Training from a Checkpoint

To continue training from a previously saved checkpoint:

- Ensure that model weights and checkpoint status are saved on your drive.
- **Resume Training Command:**
  ```bash
  !python3 /content/Fawry-Surveillance-Competition/Tracking/fast_reid/tools/train_net.py --resume --config-file "/content/Fawry-Surveillance-Competition/Tracking/fast_reid/configs/MOT20/sbs_S50.yml" MODEL.DEVICE "cuda:0"
  ```

## What Next ?

The produced model weights are saved to your personal drive in the path "MIA AI/MOT20/logs".  
You are expected to follow the next steps to be able to use the fastReID model for the tracking.

- Rename the model_000n.pth file to fastReID.pth
- Upload it as a kaggle model card
- Then the card is used as input into the notebook

```
!mv /kaggle/input/fawry-models/pytorch/default/1/fastReID.pth /kaggle/working/BoostTrack/weights
```
