# YURA_ICMS_SYSTEM

## Overview

This repository serves as the **central repository** for the **YURA ICMS (In-Cabin Monitoring System)** project.

Since the project consists of multiple AI models with independent development cycles, each model is maintained in a separate Git repository.

This repository acts as an index that provides an overview of each model, its purpose, and related repositories.

---

## Model List

### 1. Object Detection

#### Purpose

Detect objects inside the vehicle cabin to support OMS (Occupant Monitoring System) features.

Main features:

* Occupancy Detection
* Seatbelt Detection
* Child Presence Detection (CPD)
* Pet Detection
* Phone Detection
* Hands-on Detection (HOD)

#### Repository
https://github.com/DeltaX-AI-Lab/icms-yolox

#### Version

| Version | Date       | Name                  | Dataset | Train By | Note            | Origin                |
| ------- | ---------- | --------------------- | ------- | -------- | --------------- | --------------------- |
| v1.0.0  | 2026.04.22 | object_detection_v1.0.0 |    /Hippo/hdd/sami/detection/datasets/icms_datasets/oms_dataset_20260630_v3     | sami     | add child class | detection_20260630_v6 |

---

### 2. 2D Facial Landmark

#### Purpose

Estimate facial landmarks for driver monitoring and facial analysis.

Main features:

* Driver Drowsiness Detection
* Driver Distraction Detection
* Eye Openness Estimation
* Facial Analysis

#### Repository
https://github.com/DeltaX-AI-Lab/icms-face-landmark

#### Version

| Version | Date       | Name                | Dataset | Train By | Note                | Path                                   |
| ------- | ---------- | ------------------- | ------- | -------- | ------------------- | -------------------------------------- |
| v1.0.0  | 2026.04.14 | face_detection_v1.0.0 |    /hdd/binh/facial_landmark/data_binh/train_1120_crop_256_v2.txt    | binh     | Train with new data | facial_20260227_v2/model/20251120.onnx |

---

### 3. 3D Body Keypoint

#### Purpose

Estimate occupant body keypoints for posture analysis and occupant monitoring.

Main features:

* Out-of-Position Detection
* Driver Behavior

#### Repository
https://github.com/DeltaX-AI-Lab/icms-3d-body-metrabs

#### Version

| Version | Date       | Name                  | Dataset | Train By | Note                 | Path                                                              |
| ------- | ---------- | --------------------- | ------- | -------- | -------------------- | ----------------------------------------------------------------- |
| v1.0.0  | 2026.03.19 | 3d_body_keypoint_v1.0.0 |         | yunho    | merge driver & front | body_3d/body_3d_20260318_v2/model/eff2s_coco19_backbone_head.onnx |

---

### 4. 2D Body Keypoint

#### Purpose

Estimate occupant body keypoints for posture analysis and occupant monitoring.

Main features:

* Out-of-Position Detection
* Driver Behavior

#### Repository
https://github.com/DeltaX-AI-Lab/mobis-oms-pose-estimation-yolox

#### Version

| Version | Date | Name                  | Dataset | Train By | Note      | Path                                                           |
| ------- | ---- | --------------------- | ------- | -------- | --------- | -------------------------------------------------------------- |
| v1.0.0  |      | 2d_body_keypoint_v1.0.0 |    /hdd/binh/body_keypoints/finetune_dataset_0119     | binh     | PHA Final | EmbeddedAI/artifacts/AM67A/1100/16bit/body_kpts/body_kpts_20260225_v1 |

---

### 5. Driver Behavior Classification

#### Purpose

Classify driver behaviors to detect potentially unsafe driving actions.

Main features:

* Calling
* Drinking
* Eating
* Smoking
* Other

#### Repository
https://github.com/DeltaX-AI-Lab/icms-driver-behavior-classification

#### Version

| Version | Date | Name          | Dataset | Train By | Note                             | Path                                                                                      |
| ------- | ---- | ------------- | ------- | -------- | -------------------------------- | ----------------------------------------------------------------------------------------- |
| v1.0.0  |      | behavior_v1.0.0 |    /hdd/kwanjueun/project_repo/icms-integration-behavior/data_splits/dataset_V10   | binh     | accuracy improved + size reduced | EmbeddedAI/artifacts/AM67A/1100/16bit/driver_behaviour/driver_behaviour_20260518_v2 |

---

### 6. Gaze Estimation

#### Purpose

Estimate the driver's gaze direction for driver attention and distraction monitoring.

Main features:

* Driver Distraction Detection

#### Repository
https://github.com/DeltaX-AI-Lab/3D_Gaze_Ground_Truth

#### Version

| Version | Date       | Name      | Dataset | Train By | Note                                   | Path                                              |
| ------- | ---------- | --------- | ------- | -------- | -------------------------------------- | ------------------------------------------------- |
| v1.0.0  | 2026.05.14 | gaze_v1.0.0 |   /hdd/GT_LAB/Gaze-Pipelines/datasets/DeltaX/main/normalized/backup/2026-03-24_192x192      | maksym   | accuracy improved + input size changed | gaze_20260514_v4_qat_v1/model/best_model_qat.onnx |

---

### 7. Head Pose Estimation

#### Purpose

Estimate the driver's head orientation to support driver distraction detection.

Main features:

* Driver Distraction Detection

#### Repository
https://github.com/DeltaX-AI-Lab/3D_Gaze_Ground_Truth

---

### 8. Dynamic ROI (Auto Calibration)

#### Purpose

Automatically adjust the Region of Interest (ROI) according to camera position or vehicle model, minimizing manual calibration.

#### Repository
https://github.com/DeltaX-AI-Lab/icms-dynamicROI
