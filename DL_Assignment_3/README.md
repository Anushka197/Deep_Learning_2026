# IT549: Deep Learning - Lab 3 Assignment 
### Image-Based AQI Classification using CNN and Pretrained Models

**Name:** Anushka Prajapati
**Student ID:** 202301224

---

## Project Details
This project demonstrates the use of deep learning for image classification by predicting the `AQI_Class` (Air Quality Index) from images of various locations. The project implements a complete end-to-end image classification pipeline, including data preprocessing, model training, evaluation, and misclassification analysis. 

Two distinct approaches are implemented and compared:
1. **Basic CNN Model:** A custom Convolutional Neural Network trained from scratch.
2. **Pretrained CNN Model (Transfer Learning):** A ResNet-18 model fine-tuned on the AQI dataset.

## Dataset and Preprocessing
The dataset consists of a `data.csv` file mapping image paths to their corresponding AQI classes, alongside a folder of sampled images. 
* **Input Features:** `image_path` (Input Image) and `AQI_Class` (Target Label).
* **Preprocessing Pipeline:** * Images were resized to a consistent resolution of 224x224.
  * Pixel values were normalized.
  * The dataset was split into reproducible Train (70%), Validation (15%), and Test (15%) sets.

## Methodology
### 1. Basic CNN (From Scratch)
A standard Convolutional Neural Network consisting of three convolutional blocks (Conv2d -> ReLU -> MaxPool2d) followed by fully connected layers and a dropout layer for regularization. It was trained to classify images into AQI_Class categories.

### 2. Pretrained ResNet-18 (Transfer Learning)
A ResNet-18 model pre-loaded with ImageNet weights. The final classification layer was replaced to match the number of AQI classes in our dataset. To adapt the model to the specific visual markers of air quality (e.g., haze, smog), the network was fine-tuned using transfer learning.

## Results Summary
*(Note: As the input consisted solely of image data rather than tabular columns, this summary compares the performance across the two different model architectures used to process the image input.)*

| Metric | Basic CNN | Pretrained ResNet-18 (Fine-Tuned) |
| :--- | :--- | :--- |
| **Accuracy** | 0.860 | 0.982 |
| **Precision** | 0.864 | 0.982 |
| **Recall** | 0.860 | 0.982 |
| **F1-Score** | 0.860 | 0.982 |

### Discussion on Transfer Learning
Pretrained models typically outperform models trained from scratch because they have already learned to recognize complex shapes, colors, and textures from millions of images. A basic CNN must learn all these foundational visual rules from zero, relying solely on the limited samples within this dataset. Initially, transfer learning with frozen layers struggled because the model attempted to detect specific objects rather than overall environmental markers like haze. However, by fine-tuning the entire network, the model successfully adapted its extensive visual knowledge to accurately classify the AQI categories. Ultimately, transfer learning significantly aided the pretrained model in understanding complex image features much better than the basic model could.

## Misclassification Analysis
An analysis of misclassified images from the test set revealed several potential reasons for model confusion:
* **Borderline Classes:** Air quality exists on a continuous spectrum. The visual difference between adjacent classes (e.g., high "Moderate" vs. low "Poor") can be nearly imperceptible.
* **Weather Conditions vs. Pollution:** Natural weather phenomena, such as dense fog, heavy rain clouds, or overcast skies, reduce visibility and contrast. The model occasionally misinterprets this natural haziness as severe smog.
* **Lighting and Time of Day:** Images taken during sunrise or sunset often have a natural warm tint (orange/yellow) that the model can confuse with the chemical discoloration associated with poor air quality.

## Repository Contents
* `notebook.ipynb` (or `.py` scripts): Complete runnable code covering preprocessing, embeddings, training, evaluation, and analysis.
* `README.md`: Project documentation and results summary.
