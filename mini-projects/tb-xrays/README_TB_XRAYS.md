# Project: Classifying Tuberculosis in Chest X-Rays

This project walks through the process of building and evaluating a deep learning model to classify chest X-ray images as either "Healthy" or showing signs of "Tuberculosis (TB)". We started with a small, specialized dataset and used it as a practical exercise to learn key concepts in image classification.

## The Plan: A Four-Step Approach

Our goal was to learn best practices by following a structured plan:

1.  **Preprocessing:** Prepare the images for the model.
2.  **Modeling:** Build two different types of models to compare their strategies.
3.  **Evaluation:** Use robust metrics to see which model performed better.
4.  **ROC Curve Analysis:** Visualize the performance trade-offs.

### 1. Preprocessing: Cleaning the Data

Before a model can learn, the data must be clean and consistent. Our steps were:

* **Standardizing Size:** We resized all images to 224x224 pixels because models need inputs to be of the same shape.
* **Normalization:** We scaled pixel values from the \[0, 255\] range to \[0, 1\]. This helps the model train faster and more stably.
* **Data Augmentation:** On the training data, we applied small, random rotations and zooms. This creates "new" training examples, which is crucial for small datasets like ours to prevent the model from just "memorizing" the images (overfitting).

### 2. Modeling: Two Competing Strategies

We built two models to see which approach was better for our specific problem:

* **Model A: Simple CNN from Scratch:** We built a standard Convolutional Neural Network (CNN). This is like teaching a new student from scratch using only our X-ray images. It learns to spot the specific patterns relevant only to our dataset.
* **Model B: Transfer Learning (MobileNetV2):** We used a powerful, pre-trained model. This is like hiring an expert who has already seen millions of diverse images. We froze the expert's knowledge and only trained a small final layer to make the "Healthy" or "TB" decision.

### 3. Evaluation: The Surprising Results

This is where the project got interesting. When evaluating on the unseen test data, we found a clear winner.

| **Metric** | **Simple CNN** | **Transfer Learning** | **What it Means** |
| :--- | :---: | :---: | :--- |
| **Sensitivity** | **78%** | 34% | Correctly identifies actual TB cases. **(Most Important)** |
| **Specificity** | 80% | **100%** | Correctly identifies healthy cases. |
| **Precision (PPV)** | 80% | **100%** | How often a "TB" prediction is correct. |
| **NPV** | **78%** | 60% | How often a "Healthy" prediction is correct. |

The **Simple CNN** was the balanced and more useful model. The **Transfer Learning model**, while perfect at identifying healthy patients, was dangerously overcautious and missed two-thirds of the actual TB cases. For a medical screening tool, a high rate of false negatives is a critical failure.

### 4. ROC Curve & The AUC Paradox

To visualize performance, we plotted the ROC curves.

This revealed a fascinating paradox:

* **Simple CNN (AUC = 0.81):** A good, solid score reflecting its balanced performance.
* **Transfer Learning (AUC = 0.99):** A near-perfect score!

The high AUC showed that the transfer model was excellent at *ranking* TB images higher than healthy ones. However, its extreme bias towards predicting "healthy" made it unusable at a practical decision threshold. This was a key lesson: a high AUC doesn't always mean a model is useful for a specific task.

## Conclusion: The Winner and Why

The **Simple CNN model is the clear winner**.

Although the transfer learning model had a spectacular AUC score, its real-world performance was poor for our specific need. In medical screening, **Sensitivity (correctly identifying the sick) is paramount**. We would rather have a model that occasionally flags a healthy person for a second look than one that tells a sick person they are fine. The Simple CNN provided a much better and more reliable balance for this critical task.