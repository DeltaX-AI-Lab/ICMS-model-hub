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

Required Weight file name:

```text
<model_name>_<version>.pt
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

#### 2.1. Training Revision: `Z`

Increment `Z` when the model architecture and input/output interface remain unchanged, but the model is retrained or slightly updated.

Examples:

- Retraining the same model with a different dataset
- Adding new training data
- Correcting labels
- Updating data augmentation
- Updating training parameters
- Fine-tuning the existing model
- Improving accuracy without changing the model structure

Example:

```text
v1.0.0 -> v1.0.1
v1.0.1 -> v1.0.2
```

When only `Z` is incremented, `X` and `Y` remain unchanged.

---

#### 2.2. Model Revision: `Y`

Increment `Y` when the model structure, model interface, or model behavior changes.

Examples:

- Changing the model architecture
- Changing the backbone or model head
- Changing the input resolution
- Changing the input tensor shape or format
- Changing the output tensor shape or format
- Changing the number or definition of classes
- Changing the facial landmark schema
- Changing the body keypoint schema
- Making an incompatible preprocessing change
- Making an incompatible postprocessing change

When `Y` is incremented, `Z` must be reset to `0`.

Example:

```text
v1.0.3 -> v1.1.0
v1.1.4 -> v1.2.0
```

---

#### 2.3. TI Release Version: `X`

Increment `X` when a validated model has passed the required verification process and its corresponding **TI model artifact** has been officially uploaded or registered.

When `X` is incremented:

- `Y` must be reset to `0`
- `Z` must be reset to `0`
- The previous candidate model version should be recorded in the `Note` field

Example:

```text
v1.2.3 -> v2.0.0
v2.1.4 -> v3.0.0
```

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

#### Object Detection (OMS) Model

| Version | Date       | Name                  | Dataset | Owner | Note            |
| ------- | ---------- | --------------------- | ------- | -------- | --------------- |
| v1.0.0  | 2026-06-30 | object_detection_v1.0.0 |    /Hippo/hdd/sami/detection/datasets/icms_datasets/oms_dataset_20260630_v3     | sami | (origin : detection_20260630_v6) add child class |

---
### Pet Detection Model
| Version | Date | Name | Dataset | Owner | Note |
|---|---|---|---|---|---|
| v1.0.0 | 2026-06-02 | pet_detection_v1.0.0 | /hdd/sami/detection/datasets/pet_detection/synthetic_generation/synthetic_pets_in_cars-1-2 | sami | synthetic data, only trained with 2 classes |

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
### 7. Hand Gesture

#### Purpose

Estimate the driver's hand gesture.

Main features:

* Driver Hand Gesture

#### Repository
https://github.com/DeltaX-AI-Lab/3D_Gaze_Ground_Truth

#### Version

| Version | Date       | Name      | Dataset | Train By | Note                                   |
| ------- | ---------- | --------- | ------- | -------- | -------------------------------------- | 
| v1.0.0  | - | hand_gesture_v1.0.0  |   /aiteam5/ICMS/datasets/HandGesture/PHA_hand/data_split (NAS)      | hoa   | (origin : hand_gesture_20260225_v1) |

---

### 8. Head Pose

#### Purpose

Estimate the driver's head orientation to support driver distraction detection.

Main features:

* Driver Distraction Detection

#### Repository
https://github.com/DeltaX-AI-Lab/3D_Gaze_Ground_Truth

---

### 9. Dynamic ROI (Auto Calibration)

#### Purpose

Automatically adjust the Region of Interest (ROI) according to camera position or vehicle model, minimizing manual calibration.

#### Repository
https://github.com/DeltaX-AI-Lab/icms-dynamicROI
