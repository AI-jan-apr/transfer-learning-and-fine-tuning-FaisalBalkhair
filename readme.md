[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/DtxdB3_i)

# CNN Image Classification using EfficientNet (Transfer Learning)

## Project Overview

This project implements an **image classification model** using **Transfer Learning with EfficientNetB0**.

The objective is to classify images into multiple classes using a pretrained convolutional neural network and improve performance using **Fine-Tuning**.

The project includes:

- Data preprocessing
- Transfer Learning (Feature Extraction)
- Fine-Tuning
- Model evaluation
- Confusion Matrix
- Accuracy and Loss visualization
- Experiment tracking using MLflow and DagsHub

---

## Dataset

The dataset contains labeled images used for a **multi-class classification task**.

Before training the model:

- Images were resized to **224 × 224**
- EfficientNet preprocessing was applied
- The dataset was split into **training** and **validation** sets

---

## Model Architecture

The model is based on **EfficientNetB0**, a pretrained convolutional neural network trained on the ImageNet dataset.

### Architecture

Input Image (224x224x3)
↓
EfficientNetB0 (Pretrained)
↓
Global Average Pooling
↓
Dense Layer
↓
Softmax Output

---

## Transfer Learning (Feature Extraction)

In the first stage, we used **Transfer Learning**.

The EfficientNet base model was loaded with pretrained weights and **frozen** so that only the classifier layers were trained.

base_model.trainable = False

This allows the model to reuse pretrained visual features such as edges, shapes, and textures learned from ImageNet.

---

## Fine-Tuning

After training the classifier layers, **Fine-Tuning** was applied.

Some of the deeper layers of EfficientNet were unfrozen so the model could slightly adjust the pretrained features to better fit the dataset.

A smaller learning rate was used during this stage to prevent large updates that could damage the pretrained weights.

Fine-Tuning helped the model adapt the learned ImageNet features to the dataset and improved the final performance.

---

## Model Evaluation

The model was evaluated using several metrics:

- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix

The validation accuracy achieved by the model was approximately:

**~91% – 93%**

These metrics help measure how well the model performs on unseen validation data.

---

## Training Visualization

To understand the training behavior, several plots were generated:

- Training Accuracy
- Validation Accuracy
- Training Loss
- Validation Loss

Below are the training and validation curves for accuracy and loss.

### Feature Extraction:

![Feature Extraction :](plots/Feature_extraction.png)

### Fine Tuning:

![Fine Tuning :](plots/fine_tuning.png)

These visualizations help analyze:

- learning progress
- convergence behavior
- potential overfitting

---

## Confusion Matrix

A confusion matrix was generated to evaluate the prediction results across all classes.

The confusion matrix helps identify:

- correct classifications
- misclassified samples
- classes that the model confuses with each other

### Feature Extraction:

![Feature Extraction :](plots/feature_extraction_matrix.png)

### Fine Tuning:

![Fine Tuning :](plots/fine_tuning_matrix.png)

This provides deeper insight into the model's strengths and weaknesses.

---

## Experiment Tracking

Experiments were tracked using:

- **MLflow**
- **DagsHub**

These tools allow tracking:

- experiment runs
- model parameters
- training metrics
- validation accuracy

This makes it easier to compare different experiments such as:

- Feature Extraction
- Fine-Tuning

URL:
https://dagshub.com/Faisal27/food-efficientnet/experiments

---

## Experiment Summary

In this project, two training approaches were used.

**Feature Extraction**

- The EfficientNet base model was frozen.
- Only the final classification layers were trained.
- This method trains faster.

Validation accuracy: **about 91% – 92%**

**Fine-Tuning**

- Some layers of EfficientNet were unfrozen.
- The model was trained again using a smaller learning rate.

Validation accuracy: **about 92% – 93%**

Fine-Tuning slightly improved the model performance.

---

## Observations

### Feature Extraction vs Fine-Tuning

Feature Extraction trains faster because most of the network is frozen.

Fine-Tuning gives slightly better results because the model can adjust some of the pretrained layers to the dataset.

---

### Convergence

During training, the accuracy increased while the loss decreased.  
This shows that the model was learning and converging during training.

---

### Generalization

The validation accuracy is close to the training accuracy.  
This means the model generalizes well to unseen data.

---

### Overfitting

There is a small gap between training and validation results.  
This suggests mild overfitting, but it is not severe.

## Conclusion

Transfer Learning using EfficientNet enables building accurate image classification models even when datasets are relatively small.

Fine-Tuning further improves performance by allowing the model to adapt pretrained ImageNet features to the specific dataset.

## 🔗 Helpful Links

- 📚 EfficientNet models in Keras:  
  https://keras.io/api/applications/efficientnet/

- 🎓 Transfer Learning guide (Keras):  
  https://keras.io/guides/transfer_learning/

- 📦 MLflow for experiment tracking:  
  https://www.mlflow.org/docs/latest/index.html

- ☁️ DVC + DagsHub integration:  
  https://dagshub.com/docs/integrations/dvc/

- 🧑‍🍳 How to freeze/unfreeze layers in Keras:  
  https://keras.io/getting_started/faq/#how-can-i-freeze-layers-in-a-model

- 📈 Using callbacks in Keras (e.g. EarlyStopping, ReduceLROnPlateau):  
  https://keras.io/api/callbacks/
