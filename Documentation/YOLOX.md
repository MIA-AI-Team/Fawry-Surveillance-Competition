# YOLOX Training Notebook Guide

This notebook is built for running object detection experiments using the [YOLOX](https://github.com/Megvii-BaseDetection/YOLOX) model in the context of the Fawry Surveillance Competition. It handles environment setup, data preparation, and training configuration.

---

##  Repository Setup

1. **Clone the competition repo**  
   The notebook automatically clones the competition repository:

   ```bash
   !git clone https://github.com/MIA-AI-Team/Fawry-Surveillance-Competition.git
   ```


---

##  Environment Setup

2. **Install required packages:**

   ```bash
   !pip3 install -r requirements.txt
   !python3 setup.py develop
   ```

3. **Install COCO API and other dependencies:**

   ```bash
   !pip3 install cython
   !pip3 install 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
   !pip3 install cython_bbox
   ```

---

##  Dataset Preparation

4. **Create and organize the dataset structure:**

   The notebook prepares the `datasets/MOT20` directory with subfolders for `train` and `test`. You are expected to:

   - Upload the MOT20 dataset as a Kaggle dataset
   - Copy the dataset from `/kaggle/input/...` into the working directory

---


## Running Training

5. **Training and Evaluation:**

   Modify and execute the training script (`tools/train.py`) or any other config file under `exps/`.

   Example:

   ```bash
   !python tools/train.py -f exps/example/mot/yolox_x_ablation.py -d 1 -b 1 --fp16
   ```

   - `-f`: Path to the experiment config file  
   - `-d`: Number of devices   
   - `-b`: Batch size  
   - `--fp16`: Use mixed precision

---
