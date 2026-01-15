#  Module-2 — Contour Detection & ROI Extraction

Module-2 is responsible for extracting Regions of Interest (ROIs) corresponding to PCB defects after mask generation.  
It takes binary defect masks produced by **Module-1** and segments individual defect patches for downstream CNN classification.

---

##  Objectives

Module-2 performs the following key tasks:

 Detect defect contours using OpenCV  
 Generate bounding boxes around defect regions  
 Crop and store ROI patches from the test image  
 Label and organize ROI samples for model training  

These tasks match the official module definition:  
> “Use OpenCV to detect contours of defects… Extract bounding boxes and crop individual defect regions… Label defect ROIs for model training.” :contentReference[oaicite:1]{index=1}

---

##  Processing Pipeline

The Module-2 processing workflow is:


**Input:**  
- Binary defect masks from Module-1
- Original aligned test image (optional for cropping)

**Output:**  
- Cropped defect patches (ROI)
- Bounding box metadata (CSV/JSON)
- Visualization images with annotated contours

---

## Core Techniques Used

| Technique | Purpose |
|---|---|
| **cv2.findContours()** | Detects defect boundaries from binary mask |
| **cv2.boundingRect()** | Generates rectangular bounding boxes |
| **ROI Cropping** | Extracts defect patches for CNN training |
| **Filtering by Area** | Removes noise & small artifacts |

---

##  Input & Output Folder Structure

module_2:
  masks: "Binary masks from Module-1"
  images: "Aligned test PCB images"
  config.json: "Optional parameters"

module_2_outputs:
  roi: "Cropped defect patches"
  annotated: "Contour + bounding box visualization"
  labels.csv: "ROI label metadata"
  stats.json: "Optional processing stats"

## Evaluation Criteria

Module-2 is evaluated on:

 Precision of ROI detection  
 Bounding box accuracy  
 Correct cropping of relevant defect areas  

This aligns with the official evaluation criteria:  
> “Precision of ROI detection and bounding box accuracy” :contentReference[oaicite:2]{index=2}

---

## Parameters & Configuration

Key configurable parameters:

| Parameter | Description |
|---|---|
| min_contour_area | Removes tiny noise blobs |
| roi_padding | Optional padding around bounding box |
| save_visualization | Store contour-annotated images |
| save_csv | Save bounding box metadata |

---

##  Deliverables

Module-2 produces the following deliverables (as specified in PDF):

- **ROI extraction pipeline code**
- **Cropped + labeled defect samples**
- **Visualization of defect contours**

---
