# Retina OCT Explainability Project
Course: MDSC 523
Author: Keaton Banik

## Project Title
Exploring the Limitations of Justifiable Machine Learning on Retina OCT Scans of Choroidal Neovascularization

## Overview
In clinical settings, “black-box” deep models must be paired with reliable explanations before doctors will trust them. This project investigates whether a popular post-hoc technique—GradCAM heatmaps—can meaningfully explain a Keras CNN’s decisions when classifying retina OCT scans as healthy vs. diseased (Choroidal Neovascularization, CNV).

## Objectives
- Build & evaluate a convolutional neural network (CNN) that separates healthy vs. CNV OCT images with high accuracy.

- Generate GradCAM heatmaps for every test image and assess whether they highlight clinically relevant regions.

- Demonstrate that, despite near–perfect classification performance, GradCAM fails to produce trustworthy, lesion-focused explanations.

## Methods
### Data
- Sourced from a public OCT dataset on Kaggle (84 495 images across four classes).
- Selected only the “Normal” and “CNV” subsets (63 520 training, 16 975 test/validation).

### Model Architecture
- A sequential Keras CNN with four convolutional/ReLU blocks, followed by flatten + sigmoid output.
- Trained with binary cross-entropy, learning rate = 0.001, 100 epochs, 5 steps/epoch.

### Explainability
- Applied the off-the-shelf GradCAM implementation to every test scan.
- Compared raw heatmap, original image, and overlay to see if the model “looked” at the CNV lesion.

## Key Results
### Classification
- Training loss ≈ 0.3, validation loss ≈ 0.1
- Accuracy ≈ 1.00 on both sets
- Test‐set misclassification: 5/242 healthy, 3/242 CNV (∼1–2% error)

### GradCAM Heatmaps
- Heatmaps were diffuse and failed to highlight the actual lesion areas.
- Overlays showed almost uniform coloring—no clear “attention” on neovascular regions.
- Even misclassified scans produced visually similar, uninformative maps.

## Conclusions
### Performance ≠ Explainability
- Our CNN is a near-perfect “black box,” yet GradCAM does not reveal where it’s looking.
- This aligns with recent critiques that post-hoc heatmaps can give false confidence, especially under adversarial or edge-case inputs.

### Clinical Implication
- Relying on GradCAM alone could mislead practitioners into trusting a model that may be “right for the wrong reasons.”

## Future Directions
- Investigate alternative—or inherently interpretable—architectures (e.g., attention models, concept bottlenecks).

- Test other explainability techniques (e.g., LIME, SHAP) on OCT data.

- Explore adversarial-robust explanations to detect when a model’s “focus” is spurious.

*All code (data loading, model training, GradCAM visualization) was implemented in Python using JupyterLab and Keras. Figures and detailed write-up are in the submitted project document. Source Code is not available for this project (lost)*
