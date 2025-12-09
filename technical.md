
If you don’t have example images yet, you can temporarily keep those image lines or remove them.

---

## 6. Page 2 – Technical Approach (`technical.md`)

Create `technical.md`:

```markdown
---
layout: page
title: Technical Approach with AlexNet
nav_order: 2
---

# Technical Approach Using AlexNet

## Model Choice: AlexNet

AlexNet is a classic convolutional neural network (CNN) architecture that was originally designed for the ImageNet competition. It is well-suited for image classification tasks like distinguishing **sharks vs dolphins** in overhead images.

Key reasons for choosing AlexNet:

- Pretrained weights on ImageNet allow transfer learning.
- Architecture is relatively simple and easy to explain.
- Good baseline for comparison with more modern architectures such as ResNet18.

## AlexNet Architecture (Layer by Layer)

The version used in this project is the standard AlexNet from `torchvision.models`, modified so that the final fully-connected layer outputs **2 classes** instead of 1000.

High-level structure:

1. **Input Layer**
   - Input: 3-channel RGB image of size **224 × 224**

2. **Convolutional + ReLU + Pooling Blocks**
   - Several convolutional layers with ReLU activations
   - Interleaved with **max pooling** to reduce spatial dimensions
   - Early layers learn low-level features (edges, textures)
   - Later layers learn more complex patterns (shapes of fins, body outlines, etc.)

3. **Fully Connected Layers**
   - Flattened feature maps pass through multiple fully connected (dense) layers
   - Act as a high-level classifier over the abstract features extracted by the conv layers

4. **Output Layer**
   - Final fully connected layer outputs **2 logits** corresponding to:
     - Class 0: Dolphin
     - Class 1: Shark
   - A softmax function converts logits into class probabilities.

## Data Preprocessing

Before being passed into AlexNet, each image is preprocessed as follows:

- **Resize:** All images are resized to 224 × 224 pixels.
- **Normalization:** Pixel values are normalized using ImageNet mean and standard deviation:
  - Mean: [0.485, 0.456, 0.406]
  - Std:  [0.229, 0.224, 0.225]

For some experiments, the training images are augmented with:

- Random resized cropping
- Random horizontal flips
- Small rotations (e.g., ±15 degrees)
- Color jitter (brightness, contrast, saturation)

This helps the model become more robust to different viewpoints and lighting conditions that might occur in real drone footage.

## Training Setup

The model is implemented and trained in **PyTorch** using Google Colab with GPU acceleration.

Key training details:

- **Loss function:** CrossEntropyLoss
- **Optimizer:** Adam
- **Epochs:** 10
- **Batch sizes tested:** 16, 32, 64
- **Learning rates tested:** 0.001 and 0.0001
- **Train/Validation split:** 138 train images, 39 validation images

Weights & Biases (wandb) is used to:

- Log training and validation loss
- Log training and validation accuracy
- Visualize curves over epochs
- Generate confusion matrices for each run

## Full Pipeline Overview

1. Load and preprocess drone images (resize, normalize, optionally augment).
2. Feed images into AlexNet and compute forward pass.
3. Compute loss using CrossEntropyLoss.
4. Backpropagate gradients and update weights with Adam optimizer.
5. Track metrics (loss, accuracy) on both training and validation sets.
6. Save the best-performing model weights based on validation accuracy.

![Pipeline Diagram](assets/pipeline.png)

*(The pipeline diagram above can show: Input image → Preprocessing → AlexNet → Output probabilities → Class label.)*
