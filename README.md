# YURA_ICMS_SYSTEM

## Overview

This repository serves as the **central repository** for the **YURA ICMS (In-Cabin Monitoring System)** project.

Since the project consists of multiple AI models with independent development cycles, each model is maintained in a separate Git repository.

This repository acts as an index that provides an overview of each model, its purpose, and related repositories.

---
## Rules
### 1. Model Registration

Whenever a new model version is created, the corresponding **Version table** in this repository must be updated.

A model version is considered officially registered only after all required information has been added to the table.

The following fields are mandatory:

| Field | Description |
| --- | --- |
| Version | Model version in `vX.Y.Z` format |
| Date | Model registration or release date in `YYYY-MM-DD` format |
| Name | Official model name following the naming convention |
| Dataset | Exact dataset path and dataset version used for training |
| Owner | Person responsible for training and validating the model |
| Note | Summary of the changes, purpose, validation result, or original model name |


### 2. ONNX Model Storage

All ONNX model files must be stored on the **Hippo server**.

```text
Server: Hippo
Root Directory: /hdd/EmbeddedAI/icms_models
```

Each model must have its own directory.

Each model version must be stored in a separate version directory.

Required ONNX file name:

```text
<model_name>_<version>.onnx
```

Since `<version>` already includes the `v` prefix, the resulting file name will follow this format:

```text
object_detection_v1.0.0.onnx
```

### 3. Versioning Policy

All models must use the following version format:

```text
vX.Y.Z
```

This project uses a custom model versioning policy:

```text
X = TI Release Version
Y = Model Revision
Z = Training Revision
```

This policy does not follow standard Semantic Versioning exactly.

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

| Version | Date       | Name                  | Dataset | Owner | Note            |
| ------- | ---------- | --------------------- | ------- | -------- | --------------- |
| v1.0.0  | 2026-04-22 | object_detection_v1.0.0 |    /Hippo/hdd/sami/detection/datasets/icms_datasets/oms_dataset_20260630_v3     | sami | (origin : detection_20260630_v6) add child class |

---

### 2. Facial Landmark

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
| Version | Date       | Name                  | Dataset | Owner | Note            |
| ------- | ---------- | ------------------- | ------- | -------- | ------------------- | 
| v1.0.0  | 2026-04-14 | facial_landmark_v1.0.0 |    /hdd/binh/facial_landmark/data_binh/train_1120_crop_256_v2.txt    | binh     | (origin : facial_20260227_v2) Train with new data | 

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

| Version | Date       | Name                  | Dataset | Owner | Note                 | 
| ------- | ---------- | --------------------- | ------- | -------- | -------------------- |
| v1.0.0  | 2026-03-19 | 3d_body_keypoint_v1.0.0  |         | yunho    | (origin : body_3d_20260318_v2) merge driver & front |

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

| Version | Date | Name                  | Dataset | Owner | Note      | 
| ------- | ---- | --------------------- | ------- | -------- | --------- | 
| v1.0.0  |      | 2d_body_keypoint_v1.0.0  |    /hdd/binh/body_keypoints/finetune_dataset_0119     | binh     | (origin : body_kpts_20260225_v1) PHA Final |

---

### 5. Behavior

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

| Version | Date | Name          | Dataset | Train By | Note                             | 
| ------- | ---- | ------------- | ------- | -------- | -------------------------------- |
| v1.0.0  |      | behavior_v1.0.0  |    /hdd/kwanjueun/project_repo/icms-integration-behavior/data_splits/dataset_V10   | binh     | (origin : driver_behaviour_20260518_v2) accuracy improved + size reduced |

---

### 6. Gaze

#### Purpose

Estimate the driver's gaze direction for driver attention and distraction monitoring.

Main features:

* Driver Distraction Detection

#### Repository
https://github.com/DeltaX-AI-Lab/3D_Gaze_Ground_Truth

#### Version

| Version | Date       | Name      | Dataset | Train By | Note                                   |
| ------- | ---------- | --------- | ------- | -------- | -------------------------------------- | 
| v1.0.0  | 2026-05-14 | gaze_v1.0.0  |   /hdd/GT_LAB/Gaze-Pipelines/datasets/DeltaX/main/normalized/backup/2026-03-24_192x192      | maksym   | (origin : gaze_20260514_v4_qat_v1) accuracy improved + input size changed |

---

### 7. Head Pose

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
