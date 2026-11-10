# Automated Bearing Pin Quality Inspection System
### Multi-Stage Deep Learning for Industrial Visual Quality Control

An automated industrial Computer Vision system designed to inspect multiple bearings from a single tray image, detect missing pins, and classify individual bearings as **OK (Good)** or **NG (Defective)** using a two-stage YOLOv8 detection pipeline.

The system combines object detection, Region of Interest (ROI) extraction, pin counting, rule-based quality validation, and an application layer built with FastAPI and Streamlit.

---

## Project Overview

Manual bearing inspection requires operators to visually examine individual components and verify their internal pin configurations. This process can be repetitive and susceptible to human error.

This project automates the inspection workflow by detecting individual bearings, analyzing their internal pins, and generating quality decisions based on a predefined manufacturing specification.

**Quality specification:**
- **16 pins:** OK (Good Bearing)
- **Fewer than 16 pins:** NG (Defective Bearing)

## Key Highlights

- Two-stage YOLOv8 architecture for bearing localization and pin-level inspection.
- ROI-based image processing for individual bearing analysis.
- Automated pin detection and object counting.
- Rule-based OK/NG classification using a 16-pin quality specification.
- GPU-accelerated inference using an NVIDIA RTX GPU.
- Approximately 1–2 seconds of end-to-end inspection latency per multi-bearing tray image.
- FastAPI backend and Streamlit inspection interface.
- Annotated detection visualization and structured JSON/TXT reporting.

---

## System Architecture

The inspection pipeline consists of two deep learning detection stages followed by rule-based quality validation.

![System_architecture 1](output/![Output 1](output/bearing_pin_counting_inspection.png)

## Technical Workflow

### Stage 1: Bearing Detection

**Model:** Custom-trained YOLOv8

- Accepts a tray image containing multiple bearings.
- Detects and localizes individual bearings using bounding boxes.
- Extracts each detected bearing as a separate Region of Interest (ROI).
- Passes the cropped bearing images to the next inspection stage.

**Output:** Individual bearing crops.

### Stage 2: Pin Detection and Counting

**Model:** Custom-trained YOLOv8

- Processes individual bearing ROIs.
- Detects and localizes internal pins.
- Counts the detected pins for each bearing.
- Generates pin-level detection results for quality evaluation.

**Output:** Detected pin locations and individual bearing pin counts.

### Stage 3: Rule-Based Quality Classification

The detected pin count is evaluated against the predefined quality specification.

| Pin count | Classification |
|---|---|
| Exactly 16 | OK |
| Fewer than 16 | NG |

The resulting classification is associated with the corresponding bearing inspection result.

### Stage 4: Application and Result Visualization

**Backend:** FastAPI  
**Frontend:** Streamlit

The application integrates the inspection pipeline and presents the results through an interactive interface.

Key capabilities:
- Detection bounding boxes and annotated images.
- Individual bearing pin counts.
- OK/NG classification visualization.
- Total inspected, OK, and NG bearing summaries.
- Structured JSON and TXT result exports.

---

## Model Performance

Both detection models were evaluated on held-out test data.

| Evaluation metric | Bearing Detection | Pin Detection |
|---|---:|---:|
| mAP@50 | **95.2%** | **94.6%** |
| mAP@50-95 | **88.5%** | **58.2%** |
| Precision | **96.6%** | **95.2%** |
| Recall | **95.4%** | **93.7%** |
| F1-score | **95.9%** | **96.6%** |

*Note: Reported mAP@50 values represent the respective detection models, not the final OK/NG classification accuracy.*

## Inference Performance

| Parameter | Implementation |
|---|---|
| Processing input | Multi-bearing tray image |
| Inference hardware | NVIDIA RTX GPU |
| Detection architecture | Two-stage YOLOv8 |
| Processing latency | Approximately 1–2 seconds per tray |
| Backend | FastAPI |
| Frontend | Streamlit |

*Latency represents the reported end-to-end inspection processing time. It is not an FPS measurement.*

---

## Technology Stack

| Component | Technology |
|---|---|
| Programming Language | Python |
| Deep Learning Framework | PyTorch |
| Object Detection | YOLOv8 |
| Image Processing | OpenCV, NumPy |
| Model Inference | NVIDIA RTX GPU |
| Backend API | FastAPI |
| Frontend Interface | Streamlit |
| Visualization | Matplotlib, PIL |
| Result Reporting | JSON, TXT |

---

## Example Inspection Outputs

The following output examples illustrate the system's inspection capabilities.

### 1. Bearing Detection

Individual bearings are localized from a tray image using the first YOLOv8 detection stage.

<!-- Add your bearing detection screenshot here -->
<!-- ![Bearing Detection](output/bearing_detection.png) -->

### 2. Pin Detection and Counting

The second detection stage identifies internal bearing pins within individual ROI crops.

<!-- Add your pin detection screenshot here -->
<!-- ![Pin Detection](output/pin_detection.png) -->

### 3. OK/NG Quality Classification

Bearings are classified based on their detected pin counts and the predefined quality specification.

<!-- Add your OK/NG inspection screenshot here -->
<!-- ![Bearing Quality Results](output/quality_inspection.png) -->

*Replace the example image paths with the actual filenames available in the output folder.*

---

## 🧪 Example Output

Below are examples of the system’s output —  
showing detected bearings, pin counts, and defective rings highlighted for review:

<div align="center">

### 🖼️ Output 1 – Bearing Detection
![Output 1](output/output1.png)

### 🖼️ Output 2 – Pin Counting & Defective Ring Highlighting
![Output 2](output/output2.png)

</div>

## Project Outcomes

- Implemented a multi-stage object detection workflow for automated bearing inspection.
- Achieved 95.2% bearing detection mAP@50 and 94.6% pin detection mAP@50 on held-out test data.
- Automated individual bearing localization, ROI extraction, pin detection, and count-based quality classification.
- Achieved approximately 1–2 seconds of end-to-end processing latency per multi-bearing tray image.
- Integrated inspection visualization and structured reporting through a FastAPI and Streamlit application.

---

## Engineering Scope

This project demonstrates practical application of:

- Industrial Computer Vision
- Multi-Stage Object Detection
- YOLOv8 Model Development
- Region of Interest (ROI) Extraction
- Object Detection and Counting
- Rule-Based Quality Classification
- GPU-Accelerated Inference
- Computer Vision Application Development
- Automated Visual Quality Inspection

---
## Repository Scope

This repository provides a project overview, system architecture, technical workflow, performance results, and example inspection outputs.

It focuses on communicating the solution and its engineering approach rather than exposing confidential implementation code or model artifacts.
