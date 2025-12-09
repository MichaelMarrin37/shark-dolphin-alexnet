---
layout: page
title: Results & Visualizations
nav_order: 3
---

# Results, Experiments, and Takeaways

This section summarizes the main experiments performed with AlexNet (and ResNet18) on the **shark vs dolphin** dataset.

## Batch Size Experiments

**Model:** AlexNet (pretrained), learning rate = 0.0001, with augmentation.

- **Batch size 16 → Best validation accuracy ≈ 97.44%**
- **Batch size 64 → Best validation accuracy ≈ 89.74%**

Smaller batch size (16) provided better validation performance. The added noise in the gradient updates can act as a regularizer, helping the model generalize better on this small dataset.

![Batch size experiment](assets/batch_size_plot.png)

## Learning Rate Experiments

**Model:** AlexNet (pretrained), batch size = 32, with augmentation.

- **LR = 0.001 → Best validation accuracy ≈ 69.23%**
- **LR = 0.0001 → Best validation accuracy ≈ 92.31%**

A learning rate of **0.001** caused unstable training and worse generalization. Lowering the learning rate to **0.0001** led to smoother training curves and much higher validation accuracy, showing the importance of careful learning rate selection.

![Learning rate experiment](assets/lr_plot.png)

## Data Augmentation Experiments

**Model:** AlexNet (pretrained), batch size = 32, learning rate = 0.0001.

- **Without augmentation:**
  - Best validation accuracy ≈ **92.31%**
  - Training accuracy reaches **100%** (clear overfitting)
- **With augmentation:**
  - Best validation accuracy ≈ **89.74%**
  - Training accuracy stays lower, indicating less overfitting

Without augmentation, the model memorizes the training set and overfits, even though validation accuracy is high. With augmentation, the model must learn more robust features and is less overconfident, which is beneficial for generalization, especially when new drone images differ from the training set.

![Augmentation experiment](assets/augmentation_plot.png)

## Architecture Comparison: AlexNet vs ResNet18

**Setup:** pretrained models, batch size = 32, learning rate = 0.0001, with augmentation.

- **AlexNet → Best validation accuracy ≈ 84.62%**
- **ResNet18 → Best validation accuracy ≈ 89.74%**

ResNet18 slightly outperforms AlexNet on this task. ResNet18 is deeper and uses residual connections, which help it learn more complex patterns without suffering from vanishing gradients. This extra capacity appears to be useful for distinguishing subtle differences between sharks and dolphins in overhead images.

![Architecture comparison](assets/architecture_plot.png)

## Confusion Matrix

For each experiment, confusion matrices were generated using Weights & Biases to visualize how often each class was correctly or incorrectly classified.

Example confusion matrix for one of the best-performing runs:

![Confusion matrix](assets/confusion_matrix.png)

- Most predictions fall along the diagonal (correct classifications).
- A small number of images are misclassified, usually where dolphins and sharks look visually similar from above.

## Key Takeaways

- A **smaller batch size (16)** yielded the best performance for AlexNet on this small dataset.
- A **lower learning rate (0.0001)** was significantly better than 0.001.
- **Data augmentation** reduces overfitting and encourages learning more robust features, even if it slightly reduces validation accuracy on a small validation set.
- **ResNet18** outperformed **AlexNet**, suggesting that deeper networks with residual connections are helpful for this kind of drone-based animal classification.
- Overall, the model achieved **over 97% validation accuracy** in its best configuration, showing strong potential for real-world applications in beach safety and marine monitoring.
