# BoostTrack++ Guide

## Installation Instructions For The Notebook

**Note:** The following installation steps must be followed in sequence due to Kaggle storage limit constraints. Additionally, the conda environment setup is incompatible with the dataset in its converted COCO format after storage.

---

**Step 1. Insert the model weights**  
Insert the weights for the detection and the tracking embeddings as a kaggle model input in any form

- Create weights directory within Fawry_Surveillance/Tracking/BoostTrack/external/weights/
- Move and rename weights:  
   a- fastReId weights --> /weights/fastReID.pth  
   b- YOLOX weights --> weights/detector.pth.tar

```shell
!cp ${YourYoloPath} /kaggle/working/Fawry_Surveillance/Tracking/BoostTrack/external/weights/detector.pth.tar

!cp ${YourEmbeddingsPath} /kaggle/working/Fawry_Surveillance/Tracking/BoostTrack/external/weights/fastReID.pth
```

**NOTE** This step is necessary only if replicating the training cycle.

---

**Step 2. Download Dataset**  
Using the MOT20 dataset from the competition, insert it as a Kaggle input, and then convert it to COCO format for YOLOX operation.

- The files are moved from `/kaggle/input` to `/Fawry_Surveillance/Tracking/BoostTrack/data` folder:

```
data
|——————MOT20
|        └——————train
|        └——————test
```

---

**Step 3. Set Up Conda Environment**  
Setting up the environment, we utilized miniconda for this step to be able to create a conda environment on kaggle

```shell
conda env create -f boost-track-env.yml
```

Note that due to a compatibility issue with NumPy versions, a modification to the mapping.py file is required. Specifically, replace the following line in onnx module on line 25:

```python
    int(TensorProto.STRING): np.dtype(object)
```

This is done using the command and it is readily performed in the notebook

```shell
!sed -i "s/np.dtype(np.object)/np.dtype(object)/g"  /kaggle/working/miniconda/envs/boostTrack/lib/python3.8/site-packages/onnx/mapping.py
```

---

**Step 4. Conovert Dataset To COCO**

- Convert to COCO format

```shell
python3 data/tools/convert_mot20_to_coco.py
```

---

**Step 5. Inference on MOT20-01**  
The default configuration uses BoostTrack++, although BoostTrack and BoostTrack+ models are also available.

To run inference, execute the following command with the specified model parameters (which can be adjusted as needed):

```shell
!python main.py --dataset mot20 --exp_name BoostTrack_FinedTunedPP --test_dataset \
        --conf {0.0} \
        --iou_thresh {0.2} \
        --min_hits {2} \
        --max_age {40} \
        --lambda_iou {0.25} \
        --lambda_mhd {0.35} \
        --min_box_area {115} \
        --lambda_shape {0.2} \
        --dlo_boost_coef {0.35} \
        --detector "yolox"
```

- These parameters were selected based on the optimal training score but can be modified for different use cases.
- The inference output is located in the following directory:
  `/Fawry_Surveillance/Tracking/BoostTrack/results/trackers/MOT20-val/BoostTrack_FinedTunedPP{|_post|_post_gbi}/data`.
- The \_post output applies linear interpolation, while the \_post_gbi output applies gradient boosting interpolation to the resulting predictions.
- The file used for submission is the one with the \_post_gbi suffix.

---

## Citations

- Vukašin Stanojević, Srđan Sladojević, Dušan Stanojević.
  BOOSTTRACK++: Using Tracklet Information to Detect More Objects in Multiple Object Tracking.
  arXiv:2408.13003 [cs.CV], 2024.  
  [Paper Link](https://arxiv.org/pdf/2408.13003)

- BoostTrack Original GitHub Repository
  [Vukasin Stanojevic's Repo](https://github.com/vukasin-stanojevic/BoostTrack)
