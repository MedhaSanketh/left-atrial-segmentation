# 🫀 Left Atrial Segmentation in Cardiac MRI using U-Net

This project implements a deep learning-based approach to segment the **left atrium** from **cardiac MRI scans** using a **U-Net model**.

## Problem Statement

Accurate segmentation of the left atrium is critical for assessing heart health and detecting atrial fibrillation. Manual segmentation is time-consuming and prone to inter-observer variability. We automate this task using deep learning on MRI volumes provided as `.nii` files.

## Dataset

The dataset consists of:
- **20 training volumes** (`imagesTr/`) with corresponding labels (`labelsTr/`)
- **10 testing volumes** (`imagesTs/`)

Each file is in **NIfTI (.nii)** format, with varying depths but consistent slice resolution (typically 320×320 or 400×400).

## Methodology

### 1. Preprocessing
- Loaded 3D MRI volumes and converted them into **2D axial slices**
- Normalized image intensities to `[0, 1]`
- Resized to a fixed shape of `(320, 320)`
- Split into training (512 slices) and validation (128 slices)

### 🧠 2. U-Net Model
- Input shape: `(320, 320, 1)`
- Encoder-decoder structure with **skip connections**
- Output: segmentation mask with sigmoid activation
- Loss: **Dice loss** for handling class imbalance
- Optimizer: `Adam`

### 3. Postprocessing
- Predicted masks were stacked back into 3D format
- Saved as `.nii` volumes to maintain spatial integrity
- Visual comparisons made between MRI slices and predicted masks

## Results
| Metric            | Value      |
|------------------|------------|
| Mean Dice Score  | 0.742      |
| Mean IoU         | 0.695      |

- The U-Net model showed good alignment between predicted and ground truth masks.
- Visual inspection confirmed accurate segmentation in most cases.

## Repository Structure
├── model
      ├──la_segmentation_model.keras
├── predictions/ # Predicted 3D masks (.nii) for test set
      ├──.nii files predicted for test set
├── unet_seg.ipynb # Full training, evaluation, and visualization notebook
├── README.md # This file

## Future Improvements

- Use **3D U-Net** to better capture spatial continuity
- Add **attention gates** or residual blocks
- Apply **data augmentation** for better generalization
- Explore **semi-supervised learning** for unlabeled test data

## 📌 Acknowledgements

- Dataset based on- https://www.kaggle.com/datasets/adarshsng/heart-mri-image-dataset-left-atrial-segmentation
- Architecture inspired by the original [U-Net paper](https://arxiv.org/pdf/1902.09063)

## Sample Output

A side-by-side comparison of input MRI slices and predicted masks:
![image](https://github.com/user-attachments/assets/df5afb85-dc3d-4329-b885-4f33bacfdc96)
![image](https://github.com/user-attachments/assets/a1abdaa2-e1fa-486e-abb2-7b8816648689)

