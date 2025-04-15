# AdapTrack repository ⌈*[Notebook](https://www.kaggle.com/code/youssifkhale/fawry-adaptrack-inference)*⌉

## Installation Instructions For The Notebook

The following installation steps must be followed in sequence to replicate the same results.

---

**Step 1. Insert the model weights**  

- Move and rename weights:  
   a- fastReId weights --> /Tracking/AdapTrack/2. FastReID/weights/  
   b- keep yolox weights in kaggle input  

```shell
!cp ${YourEmbeddingsPath} "/kaggle/working/Fawry-Surveillance-Competition/Tracking/AdapTrack/2. FastReID/weights/fastReID.pth"
```

**NOTE** This step is necessary only if replicating the training cycle.

---

**Step 2. Download Dataset**  
Using the MOT20 dataset from the competition, insert it as a Kaggle input, and then convert it to COCO format for YOLOX operation.

- The files are moved from `/kaggle/input` to `/kaggle/working/datasets` folder:

```
/kaggle/working/datasets
└── MOT20
    ├── annotations
    ├── test
    │   └── MOT20-01
    └── train
        ├── MOT20-02
        ├── MOT20-03
        └── MOT20-05
```

use the following commands

``` shell
# Create the target directory
!mkdir -p /kaggle/working/datasets/MOT20/
!mkdir -p /kaggle/working/datasets/MOT20/test
!mkdir -p /kaggle/working/datasets/MOT20/train
!mkdir -p /kaggle/working/datasets/MOT20/annotations

# Copy test (MOT20-01)
!cp -r /kaggle/input/surveillance-for-retail-stores/tracking/test/01 /kaggle/working/datasets/MOT20/test/MOT20-01

# Copy train (MOT20-02, MOT20-03, MOT20-05)
!cp -r /kaggle/input/surveillance-for-retail-stores/tracking/train/02 /kaggle/working/datasets/MOT20/train/MOT20-02
!cp -r /kaggle/input/surveillance-for-retail-stores/tracking/train/03 /kaggle/working/datasets/MOT20/train/MOT20-03
!cp -r /kaggle/input/surveillance-for-retail-stores/tracking/train/05 /kaggle/working/datasets/MOT20/train/MOT20-05
```

---

**Step 3. Train the AFLink model**
```shell
!python -m AFLink.train
```

**Step 4. Conovert Dataset To COCO**

- Convert Dataset To COCO 

```shell
!python3 tools/convert_mot20_to_coco_det.py \
        --mot20_root /kaggle/working/datasets/MOT20 \
        --output_dir /kaggle/working/datasets/MOT20
```

---
** step 5. run the detection inference**
- ensure the existence of the following paths
    - ..AdapTrack/outputs/1. det
    - ..AdapTrack/outputs/2. det_feat 

- for detection of ***YOLOX*** run the following command
``` shell
!python detect.py \
        -f "exps/yolox_x_mot20_test.py" \
        -c ${YourYoloXPath}\
        -b 1 \
        -d 1 \
        -n "../outputs/1. det/MOT20_test_nms_0.8.pickle" \
        --fp16 \
        --fuse
```
- for the detection of ***fastReID*** run the followimg command
```shell
%cd "/kaggle/working/Fawry-Surveillance-Competition/Tracking/AdapTrack/2. FastReID"
!python ext_feats.py \
        --dataset "mot17" \
        --pickle_path "/kaggle/working/Fawry-Surveillance-Competition/Tracking/AdapTrack/outputs/1. det/MOT20_test_nms_0.8.pickle" \ 
        --output_path "/kaggle/working/Fawry-Surveillance-Competition/Tracking/AdapTrack/outputs/2. det_feat/MOT20_test.pickle" \ 
        --data_path "/kaggle/working/datasets/MOT20/images/val" \
        --weight_path "/kaggle/working/Fawry-Surveillance-Competition/Tracking/AdapTrack/2. FastReID/weights/fastReID.pth"
```
**Step 6. run the tracking Inference on MOT20-01** 
for the tracking inference run the following command
```shell
!python track.py \
        --dataset "MOT20" \
        --mode "test" \  
        --aflink_weight_path "./newmodel_epoch40_tmp.pth"
``` 
The inference output is located in the following directory:<br>
  `/kaggle/working/Fawry-Surveillance-Competition/Tracking/AdapTrack/3. AdapTrack/outputs/MOT20_test`

## Citations

- AdapTrack Original GitHub Repository
  [Kyujin Shim's Repo](https://github.com/kamkyu94/AdapTrack.git)