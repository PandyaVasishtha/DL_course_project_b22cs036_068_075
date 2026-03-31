# Blood Cell Detection using YOLOv9 (PGI)

**Deep Learning Course Project** — BCCD Dataset · YOLOv9 · Programmable Gradient Information

---

## Project Overview

This project implements **blood cell detection** on the [BCCD dataset](https://github.com/Shenggan/BCCD_Dataset) using **YOLOv9** with its novel **Programmable Gradient Information (PGI)** architecture, as introduced in:

> *"YOLOv9: Learning What You Want to Learn Using Programmable Gradient Information"*

The system detects and classifies blood cells into three categories — **RBC (Red Blood Cells)**, **WBC (White Blood Cells)**, and **Platelets** — and evaluates performance using standard object detection metrics.

---

## Objectives

- Build a robust cell-level object detector using YOLOv9's PGI architecture.
- Optimize model performance on the BCCD dataset across train/validation/test splits.
- Evaluate detection quality using **mAP**, **Precision**, **Recall**, and **F1 Score**.
- Document all results and visualizations in the project report and presentation slides.

---

## Group Members

| Name | Roll Number |
|------|-------------|
| Vasishtha Pandya | B22CS036 |
| Yogita Mundankar | B22CS068 |
| Yashraj Anupam | B22CS075 |

---

## Repository Structure
```
.
├── BCCD.v3-raw.yolov9/
│   ├── train/
│   │   ├── images/
│   │   └── labels/
│   ├── valid/
│   │   ├── images/
│   │   └── labels/
│   └── test/
│       ├── images/
│       └── labels/
├── yolov9/
│   ├── models/
│   │   └── detect/
│   │       └── yolov9-c.yaml
│   ├── train.py
│   ├── val.py
│   └── requirements.txt
├── data.yaml
├── best_model.pt
├── dl-course-project.ipynb
├── dl-course-project_M3 task.ipynb
├── dl-course-project-036-068-075_uptotrainingbothmodelsonbothmodelsforbothsplitsM3.ipynb
├── YOLOv9-Learning_What_You_Want_to_Learn_Using_Programmable_Gradient_Information.pdf
├── DL_course_project_Phase-1_ppt.pdf
├── DL_course_project.pdf
└── README.md
```

---

## Dataset

**BCCD v3 — YOLOv9 Format**

| Split | Contents |
|-------|----------|
| `train/` | Training images + YOLO-format labels |
| `valid/` | Validation images + YOLO-format labels |
| `test/`  | Test images + YOLO-format labels |

The `data.yaml` file specifies class names (`RBC`, `WBC`, `Platelets`) and paths to each split. Update the path fields to match your local directory structure before training.

---

## Approach

### 1. Data Preparation
- Load dataset using `data.yaml` (fix absolute/relative paths as needed).
- Input image resolution: **640x640**.
- Augmentations applied as per YOLOv9 defaults.

### 2. Model Configuration
- Architecture: `models/detect/yolov9-c.yaml`
- Backbone enhanced with **PGI (Programmable Gradient Information)** for improved gradient flow during deep network training.

### 3. Training
- Epochs: 10+ (adjustable)
- Batch size: `8`
- Workers: `2`
- Device: GPU (falls back to CPU if unavailable)

### 4. Evaluation
- Validation and testing via YOLOv9's built-in `val.py`.
- Key metric: **mAP@0.5**, along with Precision, Recall, F1.

---

## Notebooks

| Notebook | Description |
|----------|-------------|
| `dl-course-project.ipynb` | Main training and evaluation workflow |
| `dl-course-project_M3 task.ipynb` | M3-specific experiments and analysis |
| `dl-course-project-036-068-075_uptotrainingbothmodelsonbothmodelsforbothsplitsM3.ipynb` | Combined experimentation across model variants and data splits |

---

## Results

| Metric | Value |
|--------|-------|
| mAP@0.5 | See report |
| Precision | See report |
| Recall | See report |
| F1 Score | See report |

- Best model checkpoint: `best_model.pt`
- Qualitative outputs include bounding-box overlays on cell images and confusion matrix analysis.
- Full results and insights are documented in `DL_course_project.pdf` and `DL_course_project_ppt.pdf`.

---

## Requirements

- Python 3.8+
- PyTorch (CUDA-compatible recommended)
- YOLOv9 repository dependencies

Install all dependencies:
```bash
pip install -r yolov9/requirements.txt
```

---

## Usage

### 1. Clone the Repository
```bash
git clone <your-repo-url>
cd <repo-directory>
```

### 2. Prepare the Dataset

Update `data.yaml` with the correct paths to your dataset splits:
```yaml
train: /path/to/BCCD.v3-raw.yolov9/train/images
val:   /path/to/BCCD.v3-raw.yolov9/valid/images
test:  /path/to/BCCD.v3-raw.yolov9/test/images

nc: 3
names: ['Platelets', 'RBC', 'WBC']
```

### 3. Train the Model

**Via script:**
```bash
python yolov9/train.py \
  --data data.yaml \
  --cfg yolov9/models/detect/yolov9-c.yaml \
  --weights '' \
  --batch-size 8 \
  --epochs 10 \
  --img 640 \
  --device 0
```

**Via notebook:** Open `dl-course-project.ipynb` and run the training cells sequentially.

### 4. Evaluate / Validate
```bash
python yolov9/val.py \
  --data data.yaml \
  --weights best_model.pt \
  --img 640 \
  --device 0
```

### 5. Run Inference
```bash
python yolov9/detect.py \
  --weights best_model.pt \
  --source /path/to/test/images \
  --img 640 \
  --device 0
```

---

## References

- Wang, C.-Y. et al. *YOLOv9: Learning What You Want to Learn Using Programmable Gradient Information.* (2024)
- [YOLOv9 Official Repository](https://github.com/WongKinYiu/yolov9)
- [BCCD Dataset](https://github.com/Shenggan/BCCD_Dataset)
- Project report: `DL_course_project.pdf`
- Presentation: `DL_course_project_ppt.pdf`

---

*B22CS036 · B22CS068 · B22CS075*
