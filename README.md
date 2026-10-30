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

## 6. Implementation Details

### A. Dataset Loading

The dataset is downloaded using the `kagglehub` Python library.

- Dataset: Skin Disease Classification Image Dataset.
- Dataset subset: `Split_smol`.
- Training directory: `Split_smol/train`.

### B. CGAN Configuration

The Conditional GAN was implemented using TensorFlow/Keras with the following configuration:

| Parameter | Value |
|---|---:|
| Image height | 64 pixels |
| Image width | 64 pixels |
| Image channels | 3 (RGB) |
| Batch size | 64 |
| Latent dimension | 128 |
| Number of classes | 9 |
| Training epochs | 200 |
| Learning rate | 0.0002 |
| Random seed | 42 |
| Sample generation interval | Every 5 epochs |

The generator receives a random latent vector and a one-hot encoded class label to generate class-conditioned images.

### C. Synthetic Data Generation

After CGAN training, the generator was used to produce 20 synthetic images for each of the nine disease categories, resulting in 180 synthetic images.

### D. CNN Classifier Implementation

A CNN-based classifier was implemented using TensorFlow/Keras.

The model architecture consists of:

- Three convolutional blocks.
- Global Average Pooling (GAP).
- Dense layer.
- Dropout layer.
- Nine-class softmax output layer.

The classifier contains 102,089 trainable parameters and was trained for 10 epochs in each experimental condition.

### E. Experimental Comparison

Two training configurations were evaluated:

1. **Real-only:** The classifier was trained using 697 real training images.
2. **Real + synthetic:** The classifier was trained using 697 real images and 180 generated images, giving 877 training images.

Both configurations were evaluated using the same 181 real validation images.

Accuracy and macro F1-score were used to compare classification performance.

The complete implementation is available in the notebooks directory.

## 7. Evaluation of Generated Images

A preliminary evaluation was also performed by checking the agreement between the generated images' requested class labels and predictions from the baseline classifier.

The classifier agreed with the requested labels for 21.11% of the 180 synthetic images.

This result should be interpreted cautiously because the baseline classifier itself had limited classification performance. It does not independently establish whether the generated images have correct medical labels.

## 8. Repository Structure

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

## 9. Technologies Used

- Python
- TensorFlow / Keras
- Convolutional Neural Networks (CNN)
- Conditional Generative Adversarial Networks (CGAN)
- NumPy
- Matplotlib
- Google Colab
- Kaggle

## 10. How to Run

The project is implemented using Google Colab notebooks.

### Prerequisites
- A Google account with access to Google Colab.
- Internet connectivity.
- Access to the Kaggle dataset.
- Python environment with TensorFlow/Keras and the required libraries.

### Step 1: Access the Notebooks
1. Open the `notebooks/` directory in this repository.
2. Open `cgan_skin_disease_fixed.ipynb` in Google Colab.
3. Open `evaluation_pipeline.ipynb` separately for classification evaluation.

### Step 2: Download the Dataset
1. Open the Kaggle dataset page: [Skin Disease Classification Image Dataset](https://www.kaggle.com/datasets/riyaelizashaju/skin-disease-classification-image-dataset).
2. Follow the dataset download procedure specified in the CGAN notebook.
3. Ensure the `Split_smol` dataset directory is available in the expected location.

### Step 3: Run the CGAN Notebook
1. Execute the notebook cells in order.
2. Download and load the dataset.
3. Configure the image size, batch size and latent dimension.
4. Train the Conditional GAN.
5. Generate synthetic images for the nine disease categories.

### Step 4: Run the Evaluation Pipeline
1. Open `evaluation_pipeline.ipynb` in Google Colab.
2. Execute the cells in sequence.
3. Load the real dataset and generated synthetic images.
4. Train and evaluate the real-only and real-plus-synthetic classifiers.
5. Review the validation metrics and generated results.

### Step 5: Review the Results
- Trained models are available in the `models/` directory.
- Experimental metrics and training histories are available in `results/`.
- The final report and presentation are available in `submission/`.

**Note:** Exact dataset paths and dependencies should follow the configuration cells in the respective notebooks.

## 11. Limitations

- The dataset is relatively small.
- The generated images have limited visual detail.
- Synthetic image labels were not independently verified by medical experts.
- The baseline classifier has limited classification performance.
- The experiments used a validation set rather than an independent test set.
- Only one experimental run per training condition was evaluated.

## 12. Conclusion

This project demonstrates a basic CGAN-based approach to generating synthetic skin disease images and evaluates their use in a CNN-based classification task.

Although synthetic images increased the training dataset size, they did not improve validation accuracy in the experiments conducted.

The findings highlight that increasing dataset size with generated images does not necessarily improve classification performance. The quality, diversity and reliability of synthetic data are important considerations.

**Disclaimer:** This project is intended solely for academic and experimental purposes. It is not a clinically validated medical diagnostic system and must not be used for medical diagnosis or treatment decisions.
