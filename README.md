# CNN Image Classification – Cats, Dogs, Birds

This project implements a convolutional neural network (CNN) to classify images of three animal categories: cats, dogs, and birds. It includes two model architectures (simple and complex), comparison of training strategies, overfitting mitigation techniques, and post-training interpretability using SHAP.

## Overview

- **Dataset**: 19,000+ images across 3 classes.
- **Models**:
  - **Simple CNN**: 2 convolutional layers with dropout and L2 regularization.
  - **Complex CNN**: 4 convolutional layers with batch normalization and dropout.
- **Frameworks**: TensorFlow, Keras
- **Evaluation**: Accuracy, Loss, Confusion Matrix, SHAP Explanation

## Features

- Data preprocessing, filtering invalid image files
- Standardization of input data to [0, 1] range
- Training-validation-test split
- Model compilation with multiple optimizers (Adam, SGD)
- Training with TensorBoard logging
- Visualization of training accuracy and loss
- Use of SHAP for model interpretability
- Model saving and loading with history tracking

## Dataset Details

Images are organized in subdirectories by class under the `data/` folder. The input size is standardized to 128x128 pixels, with 3 color channels. Files with invalid image extensions are filtered out prior to training.

## Model Architectures

### 1. Simple CNN

```python
Conv2D(32) → MaxPooling → Conv2D(64) → MaxPooling → Flatten → Dense(128) → Dropout → Dense(3, softmax)
```

- Regularization: Dropout (0.5)
- Initial version prone to overfitting
- Improved with kernel L2 regularization and intermediate Dropout layers

### 2. Complex CNN

```python
Conv2D(32) → MaxPooling → Conv2D(64) → MaxPooling → Conv2D(128) → MaxPooling → Conv2D(256) → MaxPooling → Flatten → Dense(256) → Dropout → Dense(3, softmax)
```

- Designed to extract features progressively
- Overfitting delayed compared to simpler architecture

## Training Strategy

- Optimizers tested: `Adam`, `SGD`
- Trained for 10 epochs
- TensorBoard used for live performance monitoring
- Validation set used to monitor overfitting

## Model Evaluation

- Accuracy and loss tracked across epochs
- Confusion matrices plotted for model versions
- SHAP (SHapley Additive exPlanations) applied to analyze model predictions and feature importance

## Performance Summary

- **Simple CNN (v1)**: High accuracy on training but poor validation loss after epoch 4.
- **Simple CNN (v2)**: Lower accuracy but improved generalization; less overfitting.
- **Complex CNN**: More stable training; slight overfitting observed near epoch 7.

> Note: Class imbalance (e.g., bird images outnumbering cats and dogs) influences training dynamics and evaluation metrics.
