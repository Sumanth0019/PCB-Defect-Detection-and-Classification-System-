# PCB Defect Detection & Classification System

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.x-green.svg)](https://opencv.org/)
[![Status](https://img.shields.io/badge/Status-In--Development-orange.svg)]()

An automated end-to-end pipeline for detecting and classifying manufacturing defects in Printed Circuit Boards (PCBs) using Computer Vision and Deep Learning.



---

## Project Overview
Manual inspection of PCBs is prone to human error and fatigue. This system implements a robust automated pipeline that identifies defects by comparing a **Test PCB** against a **Golden Template** (defect-free) image.

The system performs precision alignment, digital subtraction, and Region of Interest (ROI) extraction, preparing the data for a CNN-based classification model.

###  Key Features
* **Precision Alignment:** Uses Enhanced Correlation Coefficient (ECC) maximization to align test images to templates.
* **Advanced Image Processing:** Subtraction-based defect localization with morphological noise reduction.
* **Automatic ROI Extraction:** Generates cropped image segments of detected defects for model training.
* **Scalable Pipeline:** Designed to handle batch processing via Google Drive or local directories.
* **Modular Architecture:** Easily swap out the CV backend or the Deep Learning classifier.

---

## System Architecture

The project is divided into four strategic milestones:

| Milestone | Phase | Description | Status |
| :--- | :--- | :--- | :--- |
| **M1** | **Image Processing** | Template matching, ECC alignment, and ROI extraction.
| **M2** | **Deep Learning** | Training CNN/EfficientNet on extracted ROIs.
| **M3** | **Integration** | Building the Flask/Streamlit Frontend and API. 
| **M4** | **Deployment** | Documentation and Cloud Deployment.



---

## Dataset Structure
The system expects the following directory hierarchy for seamless processing:

```text
PCB_DATASET/
├── PCB_USED/              # Golden (Defect-free) template images
│    ├── 01.png
│    └── 02.png
├── images/                # Raw Test images categorized by defect type
│    ├── spur/             # e.g., 01_spur_01.jpg
│    ├── short/            # e.g., 05_short_02.jpg
│    └── open/             # e.g., 10_open_01.jpg
└── outputs/               # Auto-generated artifacts
     ├── aligned/          # Result of ECC alignment
     ├── diff/             # Raw subtraction results
     ├── mask/             # Binary masks of defects
     └── rois/             # Cropped defect images for CNN input
