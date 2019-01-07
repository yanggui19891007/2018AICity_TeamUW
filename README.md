# Single-camera and Inter-camera Vehicle Tracking and 3D Speed Estimation Based on Fusion of Visual and Semantic Features for the NVIDIA AI City Challenge Workshop at CVPR 2018

This repository contains our source code of Track 1 and Track 3 at the [NVIDIA AI City Challenge](https://www.aicitychallenge.org) Workshop in [CVPR 2018](http://cvpr2018.thecvf.com/program/workshops).

The source code of Track 1 is built in MATLAB and C++, with our trained YOLOv2 model provided. 

The source code of Track 3 is developed in Python and C++. 

Both Track 1 and Track 3 have been tested on Linux and Windows. Dependencies include CUDA, cuDNN and OpenCV.

Our UW team members include [Zheng(Thomas) Tang](https://github.com/zhengthomastang), [Gaoang Wang](https://github.com/GaoangW), [Hao(Alex) Xiao](https://github.com/AlexXiao95), Aotian Zheng.

[[Paper]](http://openaccess.thecvf.com/content_cvpr_2018_workshops/papers/w3/Tang_Single-Camera_and_Inter-Camera_CVPR_2018_paper.pdf), 
[[Slides]](https://alexxiao95.github.io/publications/cvprw/cvpr_slides.pdf),
[[Poster]](https://alexxiao95.github.io/publications/cvprw/cvpr_poster.pdf), 
[[Project Page]](http://allison.ee.washington.edu/thomas/aicity18/), 
[[2018 NVIDIA AI City Challenge]](http://openaccess.thecvf.com/content_cvpr_2018_workshops/papers/w3/Naphade_The_2018_NVIDIA_CVPR_2018_paper.pdf)

## Announcement

Sorry about the inconvenience, but the datasets for the I City Challenge Workshop at CVPR 2018 is no longer available to the public. Instead, the 2019 CVPR AI City Challenge Workshop has just been launched. This year they have a unique city-scale dataset for multi-camera vehicle tracking as well as image-based re-identification. They also have a new dataset for traffic anomaly detection. The scale of the dataset and the number of vehicles that are being used for evaluation are both unprecedented. 

To access the new datasets, each participant will need to download a data release form at the [AI City Challenge website](https://www.aicitychallenge.org/) and participate in the challenge. Please forward your inquiry to aicitychallenge2019@gmail.com for questions and comments.

## Introduction

### NVIDIA AI City Challenge Workshop at CVPR 2018

The NVIDIA AI City Challenge Workshop at CVPR 2018 will specifically focus on ITS problems such as

1. Estimating traffic flow characteristics, such as speed
2. Leveraging unsupervised approaches to detect anomalies caused by crashes, stalled vehicles, etc. This is the only way to get the humans in the loop pay attention to meaningful visual information
3. Multi-camera tracking, and object re-identification in urban environments

Our team participated in 2 out of 3 tracks: 

1. Track 1 - Traffic Flow Analysis - Participating teams submit results for individual vehicle speed for a test set containing 27 1-minute videos. Performance is evaluated based on ground truth generated by a fleet of control vehicles that were driven during the recording. Evaluation for Challenge Track 1 is based on detection rate of the control vehicles and the root mean square error of the predicted control vehicle speeds.
2. Track 3 - Multi-camera Vehicle Detection and Reidentification - Participating teams identify all vehicles that are seen passing at least once at all of 4 different locations in a set of 15 videos. Evaluation for Challenge Track 3 is based on detection accuracy and localization sensitivity for a set of ground-truth vehicles that were driven through all camera locations at least once.

Detailed information of this challenge can be found [here](https://www.aicitychallenge.org/).

Our team achieves rank #1 in both Track 1 and Track 3. The demo videos can be viewed [here](http://allison.ee.washington.edu/thomas/aicity18/). 

### Single-camera Tracking (SCT)

In SCT, our loss function consists of motion, temporal and appearance attributes. Especially, a histogram-based adaptive appearance model is designed to encode long-term appearance change for enhanced robustness. The change of loss is incorporated with a bottom-up clustering strategy for the association of tracklets. Robust 2D-to-3D backprojection is achieved with EDA optimization applied to camera calibration for speed estimation. 

### Inter-camera Tracking (ICT)

The proposed appearance model together with DCNN features, license plates, detected car types and traveling time information are combined for the computation of cost function in ICT. 

## Code structure

### Track 1

Under the `./Track1/` folder, there are 6 software packages:

1. `VDO2IMG_IPL`: Converting each video file to a folder of frame images
2. `CAM_CAL_IPL`: Manual camera calibration based on minimization of reprojection error and EDA optimization
3. `YOLO_VEH_IPL`: Extension of the YOLOv2 object detector with our trained model for vehicle detection/classification
4. `TC_tracker`: Proposed tracklet-clustering-based tracking method
5. `APP_MDL_IPL`: Extraction of histogram-based adaptive apperance models and their comparison
6. `SPD_EST_IPL`: Speed estimation based on input of tracking results and camera parameters

Detailed description of each package is given in each subfolder. 

### Track 3

Under the `./Track3/` folder, there are 3 software packages:

1. `Multi-Camera Vehicle Tracking and Re-identification`: Multi-camera vehicle tracking based on a fusion of histogram-based adaptive appearance models, DCNN features, detected car types and traveling time information
2. `YOLO_LP_IPL`: Detection of license plate from each cropped vehicle image
3. `LP_COMP_IPL`: Comparison of license plates under low resolution

Detailed description of each package is given in each subfolder. 

The output of `Multi-Camera Vehicle Tracking and Re-identification` is the similarity score between each pair of vehicles for comparison. We can convert it into a distance score by inverse proportion. The output of `LP_COMP_IPL` is the distance score between each two license plates. The final distance score between two vehicles is the multiplication of the above two distance scores. Several vehicle pairs that enjoy low distance scores and appear in all 4 camera locations are submitted to Track 3 for evaluation. 

## Reference

Please cite these papers in your publications if it helps your research:

    @inproceedings{tang2018vehicle,
      author = {Zheng Tang and Gaoang Wang and Hao Xiao and Aotian Zheng and Jenq-Neng Hwang},
      booktitle = {CVPR Workshop (CVPRW) on the AI City Challenge},
      title = {Single-camera and Inter-camera Vehicle Tracking and 3D Speed Estimation Based on Fusion of Visual and Semantic Features},
      year = {2018},
      pages = {108--115}
    }

    @inproceedings{tang2017vehicle,
      author = {Zheng Tang and Gaoang Wang and Tao Liu and Young-Gun Lee and Adwin Jahn and Xu Liu and Xiaodong He and Jenq-Neng Hwang},
      booktitle = {arXiv preprint arXiv:1708.06831},
      title = {Multiple-kernel Based Vehicle Tracking Using 3D Deformable Model and Camera Self-Calibration},
      year = {2017}
    }

## Disclaimer

For any question you can contact [Zheng (Thomas) Tang](https://github.com/zhengthomastang).
