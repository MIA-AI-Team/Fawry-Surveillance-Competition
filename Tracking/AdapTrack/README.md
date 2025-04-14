# AdapTrack
[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/adaptrack-adaptive-thresholding-based/multi-object-tracking-on-mot17)](https://paperswithcode.com/sota/multi-object-tracking-on-mot17?p=adaptrack-adaptive-thresholding-based)<br>
[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/adaptrack-adaptive-thresholding-based/multi-object-tracking-on-mot20-1)](https://paperswithcode.com/sota/multi-object-tracking-on-mot20-1?p=adaptrack-adaptive-thresholding-based)<br>

Official code for "AdapTrack: Adaptive Thresholding-Based Matching For Multi-Object Tracking", ICIP, 2024
  - https://ieeexplore.ieee.org/document/10648139

## Environment
Developed in python3.8, pytorch 1.13


## Prepare
**1. Downlodad datasets**
  - MOT17: https://motchallenge.net/data/MOT17.zip
  - MOT20: https://motchallenge.net/data/MOT20.zip

<br />

**2. Locate codes and datasets as below**
```
- code
  - 1. YOLOX
  - 2. FastReID
  - 3. AdapTrack

- dataset
  - MOT17
  - MOT20
```

<br />

**3. Download and properly locate the GT files for the validation sets**
  - [MOT17_val_gt.zip](https://drive.google.com/file/d/1HQvUHv_ng35GhFpFgHXWz-Y4dQlI1sAa/view?usp=drive_link)
  - [MOT20_val_gt.zip](https://drive.google.com/file/d/1b84UkQPKyNG0BHWBLO4eG3QCAXirBCLQ/view?usp=drive_link)

**4. Run**
```
run 1. YOLOX
run 2. FastReID
run 3. AdapTrack
```
### Updates
- Modified `opts.py` to avoid import-time execution and support custom datasets.
- Updated `track.py` to handle cases without MOT-style detection features.
- Added flexibility for Kaggle or non-MOT environments.

### Running with Custom Datasets
To use with a custom dataset (e.g., in Kaggle):
1. Set `dataset_root`, `dataset`, `mode`, and `vid_names` in your script after importing `Opts`.
2. Pass detections directly to `Tracker` instead of relying on `det_feat.pickle`.
