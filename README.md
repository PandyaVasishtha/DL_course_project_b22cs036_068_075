# DeepLearning Course Project

## Project Overview

This project implements blood cell detection over the BCCD dataset using YOLOv9 object detection with PGI architecture as mentioned in the paper 'YOLOv9: Learning What You Want to Learn
Using Programmable Gradient Information'. The aim is to identify and classify blood cells into categories (e.g., RBC, WBC, Platelets) and compute detection metrics.

### Objectives (from report/presentation)

- Build a robust detector with YOLOv9 for cell-level object detection.
- Optimize model performance on the BCCD dataset across train/valid/test splits.
- Evaluate detection using mAP, precision, recall, and F1 score.
- Document results and visualization in report and slides (`YOLOv9-Learning_What_You_Want_to_Learn_Using_Programmable_Gradient_Information.pdf`, `DL_course_project_Phase-1_ppt.pdf`).

## Group Members

- Vasishtha Pandya (B22CS036)
- Yogita Mundankar (B22CS068)
- Yashraj Anupam (B22CS075)

## Dataset

- BCCD.v3-raw.yolov9 dataset:
  - `train/images`, `train/labels`
  - `valid/images`, `valid/labels`
  - `test/images`, `test/labels`
- `data.yaml` config for YOLOv9 includes class names and path references.

## Approach

1. Data loading and preprocessing (YAML path fix, image size 640, augmentations as needed)
2. Model config: `models/detect/yolov9-c.yaml`
3. Training:
   - epochs 10+ (adjustable)
   - batch size 8, workers 2
   - device GPU/CPU as available
4. Validation and testing via YOLOv9 built-in evaluation (mAP@0.5 etc.).

## Notebooks

- `dl-course-project.ipynb`: Main training and evaluation workflow.
- `dl-course-project_M3 task.ipynb`: M3-specific experiments/analysis.
- `dl-course-project-036-068-075_uptotrainingbothmodelsonbothmodelsforbothsplitsM3.ipynb`: Combined experimentation of model variants and data splits.

## Results (summary from PDFs)

- Best model checkpoint: `best_model.pt`
- Key metrics: mAP, precision, recall, F1 (values in report)
- Qualitative: bounding boxes over cell images, confusion analysis.

## Requirements

- Python 3.8+
- PyTorch
- yolov9 repository dependencies
- `pip install -r yolov9/requirements.txt`

## Usage

1. Clone repo.
2. Prepare dataset and update `data.yaml` with correct directories.
3. Run training cell in notebook or `python train.py --data data.yaml --cfg models/detect/yolov9-c.yaml ...`.
4. Evaluate with `python val.py --data data.yaml --weights best_model.pt` or notebook cells.
5. Refer to `DL_course_project.pdf` and `DL_course_project_ppt.pdf` for full experimental setup and insights.
