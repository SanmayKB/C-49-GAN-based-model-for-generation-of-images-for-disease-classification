# GAN-Based Medical Image Generation for Skin Disease Classification

## 1. Project Overview

This project explores the use of Generative Adversarial Networks (GANs) to generate synthetic medical images of skin diseases and investigates whether these generated images can help improve skin disease classification.

The project uses a Conditional Generative Adversarial Network (CGAN), which generates images based on a specified disease class.

The generated images are combined with real training images to evaluate their potential contribution to a CNN-based classification model.

**Project type:** Academic / Experimental  
**Domain:** Medical Image Generation and Deep Learning

## 2. Objectives

- Implement a Conditional GAN for skin disease image generation.
- Generate synthetic images belonging to different skin disease categories.
- Build a CNN-based skin disease classification model.
- Compare classification performance using real-only and real-plus-synthetic training datasets.
- Evaluate the usefulness and limitations of synthetic medical images.

## 3. Dataset

The project uses the Skin Disease Classification Image Dataset.

Dataset source: [Kaggle – Skin Disease Classification Image Dataset](https://www.kaggle.com/datasets/riyaelizashaju/skin-disease-classification-image-dataset)

The experiments used the `Split_smol` dataset.

The dataset contains nine disease categories:

1. Actinic keratosis
2. Atopic Dermatitis
3. Benign keratosis
4. Dermatofibroma
5. Melanocytic nevus
6. Melanoma
7. Squamous cell carcinoma
8. Tinea Ringworm Candidiasis
9. Vascular lesion

The available data used in the experiments consisted of:
- Training images: 697
- Validation images: 181

An independent test split was not available in the dataset used.

## 4. Methodology

### A. Conditional GAN (CGAN)

A Conditional GAN was used to generate synthetic skin disease images.

The generator receives:
- A random latent vector of dimension 128.
- A one-hot encoded disease-class label of dimension 9.

It generates an RGB image of size 64 × 64 pixels.

### B. Synthetic Image Generation

The trained generator was used to produce 20 synthetic images for each of the nine disease categories.

Total synthetic images generated: **180**.

### C. CNN Classification

A CNN-based classifier was trained under two experimental conditions:

**Experiment 1: Real-only training**
- 697 real training images.

**Experiment 2: Real + synthetic training**
- 697 real training images.
- 180 synthetic images.
- Total: 877 images.

Both experiments used the same validation set of 181 real images.

## 5. Experimental Results

| Metric | Real-only | Real + synthetic |
|---|---:|---:|
| Training images | 697 | 877 |
| Final validation accuracy | 29.28% | 28.73% |
| Macro F1-score | 0.2223 | 0.2315 |

### Additional observations

- The best validation accuracy during real-only training was 32.60%.
- The best validation accuracy during real-plus-synthetic training was 31.49%.
- The final validation accuracy was slightly lower after adding synthetic images.
- Macro F1-score increased slightly from 0.2223 to 0.2315.

The results indicate that adding synthetic images did not produce an improvement in overall validation accuracy in these experiments, although a small improvement in macro F1-score was observed.

## 6. Evaluation of Generated Images

A preliminary evaluation was also performed by checking the agreement between the generated images' requested class labels and predictions from the baseline classifier.

The classifier agreed with the requested labels for 21.11% of the 180 synthetic images.

This result should be interpreted cautiously because the baseline classifier itself had limited classification performance. It does not independently establish whether the generated images have correct medical labels.

## 7. Repository Structure

```text
GAN-based-model-for-generation-of-images-for-disease-classification/
│
├── notebooks/
│   ├── cgan_skin_disease_fixed.ipynb
│   └── evaluation_pipeline.ipynb
│
├── models/
│   ├── generator_final.keras
│   ├── real_only_final.keras
│   └── real_plus_synthetic_final.keras
│
├── results/
│   ├── README.md
│   ├── results_summary.csv
│   ├── training_histories.json
│   └── validation_accuracy.png
│
├── submission/
│   ├── C_C49_Final_Evaluation_Presentation.pptx
│   ├── C_C49_Final_Project_Report.pdf
│   └── README.md
│
└── README.md
```

## 8. Technologies Used

- Python
- TensorFlow / Keras
- Convolutional Neural Networks (CNN)
- Conditional Generative Adversarial Networks (CGAN)
- NumPy
- Matplotlib
- Google Colab
- Kaggle

## 9. How to Run

1. Open the CGAN notebook in Google Colab.
2. Download or connect the required dataset from Kaggle.
3. Install the dependencies specified in the notebook.
4. Run the notebook cells to load the dataset and work with the CGAN.
5. Open the evaluation pipeline notebook to generate synthetic images and perform the classification experiments.

The trained generator model is provided in the `models` directory.

## 10. Limitations

- The dataset is relatively small.
- The generated images have limited visual detail.
- Synthetic image labels were not independently verified by medical experts.
- The baseline classifier has limited classification performance.
- The experiments used a validation set rather than an independent test set.
- Only one experimental run per training condition was evaluated.

## 11. Conclusion

This project demonstrates a basic CGAN-based approach to generating synthetic skin disease images and evaluates their use in a CNN-based classification task.

Although synthetic images increased the training dataset size, they did not improve validation accuracy in the experiments conducted.

The findings highlight that increasing dataset size with generated images does not necessarily improve classification performance. The quality, diversity and reliability of synthetic data are important considerations.

**Disclaimer:** This project is intended solely for academic and experimental purposes. It is not a clinically validated medical diagnostic system and must not be used for medical diagnosis or treatment decisions.
