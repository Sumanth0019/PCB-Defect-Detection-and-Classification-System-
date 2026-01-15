# Module-1 — Image Subtraction & Mask Generation

Module-1 prepares raw PCB images for ROI extraction by performing template-based alignment, defect highlighting, and binary mask generation.  
It follows the **DeepPCB workflow** and outputs **high-quality binary masks** used by downstream defect classification modules.

---

## Objectives

Module-1 performs the following key tasks:

- Load template & test PCB images  
- Align test image to golden template (ECC Warp)  
- Convert images to grayscale  
- Histogram equalization for contrast normalization  
- Compute pixel-wise absolute difference  
- Apply **Otsu global thresholding**  
- Morphological filtering to remove noise  
- Connected-component filtering to extract clean defect masks  

---

##  Processing Pipeline
```text
┌──────────┐ ┌────────────┐ ┌────────────┐
│ Template │ │ Test PCB │ │ Defect(s) │
└─────┬────┘ └──────┬─────┘ └────┬──────┘
│ │ │
└─────➤ Alignment ◄─┘ │
(ECC Warp) │
│ │
➤ Grayscale + Equalization │
│ │
➤ abs(Image₁ − Image₂) │
│ │
➤ Otsu Thresholding │
│ │
➤ Morphological Filtering │
│ │
➤ Connected Components │
│ │
┌─────────▼────────┐
│ Final Binary Mask │
└───────────────────┘
```

---

## ⚙️ Techniques & Purpose

| Technique                       | Purpose                                                |
|---------------------------------|--------------------------------------------------------|
| **ECC Alignment**               | Aligns test PCB to template to reduce geometric noise |
| **Histogram Equalization**      | Normalizes lighting & improves contrast                |
| **Absolute Difference**         | Highlights defect regions                              |
| **Otsu Thresholding**           | Converts difference image into binary mask             |
| **Morphological Opening/Closing** | Removes noise & fills gaps                           |
| **Connected Component Filtering** | Discards tiny noise blobs based on area              |

---

##  Alignment (ECC Warp)

ECC (**Enhanced Correlation Coefficient**) alignment produces stable geometric correction compared to feature-based ORB/SIFT for PCB layouts.

**Optimization Objective:**

\[
W^* = \arg\max_W \rho(T(x), I(W(x)))
\]

Where:

- \( T(x) \) = template image  
- \( I(x) \) = test image  
- \( \rho \) = correlation coefficient  
- \( W \) = warp function  

---

## Difference Computation

Defects are detected using **pixel-wise absolute difference**:

\[
D(x, y) = |T(x, y) - A(x, y)|
\]

Where:

- \( T \) = template image  
- \( A \) = aligned test image  

---

## Thresholding (Otsu)

Otsu's method finds an optimal threshold \( \tau \) such that:

\[
Mask(x, y) =
\begin{cases}
1, & D(x, y) \ge \tau \\
0, & D(x, y) < \tau
\end{cases}
\]

This creates a binary defect map.

---

## Morphological Filtering

Two primary morphology operations are used:

| Operation                         | Effect                                |
|----------------------------------|----------------------------------------|
| **Opening** (erosion → dilation) | Removes salt-pepper noise              |
| **Closing** (dilation → erosion) | Closes small holes inside defect blobs |

---

##  Connected Component Filtering

Final noise removal step ensures only meaningful defects remain:

\[
Area(Component_i) \ge \alpha
\]

Where \( \alpha \) is the minimum valid component area.  
Small components are removed as noise.

---




