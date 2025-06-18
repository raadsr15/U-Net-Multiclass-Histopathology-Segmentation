# U-Net-Multiclass-Histopathology-Segmentation

This repository contains a practical implementation of U-Net for multiclass segmentation of histopathology images in PyTorch. The code demonstrates the complete workflow for training a segmentation model to distinguish between background, nuclei, and border regions in microscopy images. Mask preprocessing includes conversion of RGB-encoded annotations to integer class maps, enabling multiclass semantic segmentation rather than binary classification.

All steps of the process are covered within a single Jupyter notebook, including dataset preparation, data augmentation, model definition, training and validation loops, evaluation with Dice and IoU metrics for each class, and visualization of results. The approach follows established methods in biomedical image segmentation and is built to be reproducible and straightforward to understand.

The dataset used is the 2018 Kaggle Data Science Bowl collection, which provides diverse cell images and masks in a public research context. Dataset files themselves are not included in this repository; users are instructed on how to download and arrange the data for training and evaluation.

## Dataset Description

This project uses images from the [2018 Kaggle Data Science Bowl](https://www.kaggle.com/competitions/data-science-bowl-2018/data), a large-scale biomedical imaging challenge focused on cell nuclei segmentation. The dataset contains thousands of microscopy images of cell samples collected from a variety of organisms and imaging conditions, making it an excellent benchmark for developing and evaluating segmentation algorithms.

### Key Features

- **Input images:** Variable-size RGB microscopy images containing single or multiple nuclei.
- **Annotation masks:** Each image is accompanied by a ground truth mask, where nuclei are labeled and encoded as separate objects. For this project, color-coded masks are converted to multiclass (background, nucleus, border) segmentation maps.
- **Diversity:** The dataset includes images from different cell types, tissues, and imaging modalities, enhancing model robustness and generalizability.
- **Use case:** Supports training, validation, and testing of semantic segmentation models in biomedical research.

  
## Pipeline Overview

- **Data Preparation:** Organize and preprocess raw microscopy images and RGB-encoded mask files.
- **Mask Conversion:** Convert color-coded masks to integer class maps (background, nuclei, border).
- **Dataset & Augmentation:** Build PyTorch datasets and apply basic augmentations for training.
- **Model Definition:** Implement a U-Net architecture with three output channels for multiclass segmentation.
- **Training Loop:** Train the model using CrossEntropyLoss and Adam optimizer, monitoring per-class Dice and IoU metrics.
- **Validation & Evaluation:** Assess performance on a held-out validation set after each epoch.
- **Visualization:** Display input images, ground truth masks, and predicted segmentations for qualitative assessment.
- **Inference:** Apply the trained model to new/unseen images for segmentation.

## Results

After 100 epochs of training, the U-Net model achieved the following validation scores (averaged over the last epoch):

- **Dice Coefficient (background, nucleus, border):**
  - [0.9703754  0.86121219 0.37682778]

- **IoU Score (background, nucleus, border):**
  - [0.94507935 0.7692299  0.27852891]

### Score Interpretation

| Dice Coefficient | IoU (Jaccard) | Interpretation           |
|------------------|--------------|--------------------------|
| 0.90 – 1.00      | 0.81 – 1.00  | Excellent (near-perfect) |
| 0.80 – 0.90      | 0.65 – 0.81  | Very Good                |
| 0.70 – 0.80      | 0.50 – 0.65  | Good                     |
| 0.60 – 0.70      | 0.36 – 0.50  | Fair/Usable              |
| < 0.60           | < 0.36       | Poor                     |

- **Background and nucleus classes achieved strong segmentation performance.**
- **Border class segmentation remains challenging, with lower Dice/IoU.**

*(See training logs for full epoch-by-epoch metrics.)*

  
