# AlexNet: ImageNet Classification with Deep Convolutional Neural Networks

**Authors**: Alex Krizhevsky, Ilya Sutskever, Geoffrey E. Hinton
**Institution**: University of Toronto
**Published**: 2012 (NeurIPS 2012)

---

## Overview

AlexNet is the deep convolutional neural network that won the ImageNet Large Scale Visual Recognition Challenge (ILSVRC) 2012 by a massive margin — achieving 15.3% top-5 error vs 26.2% for the second-place entry. This single result launched the modern deep learning era. Before AlexNet, the best computer vision systems used hand-crafted features (SIFT, HOG). After AlexNet, deep neural networks became the dominant paradigm for virtually every perception task.

---

## Historical Context

The ImageNet dataset contained 1.2 million labeled images across 1,000 categories — orders of magnitude larger than anything previously used for training. The question was: could a neural network actually learn from this data?

The challenge: neural networks had been stuck in a "winter" for years. Backpropagation worked on small networks but was believed to fail on deep ones. AlexNet proved this wrong by combining:
1. A large labeled dataset (ImageNet)
2. GPU-accelerated training
3. Key architectural innovations (ReLU, Dropout, Local Response Normalization)

---

## Architecture

AlexNet has 8 learned layers: 5 convolutional + 3 fully connected.

```
Input (224×224×3)
→ Conv1 (96 filters, 11×11, stride 4) → ReLU → LRN → MaxPool
→ Conv2 (256 filters, 5×5) → ReLU → LRN → MaxPool
→ Conv3 (384 filters, 3×3) → ReLU
→ Conv4 (384 filters, 3×3) → ReLU
→ Conv5 (256 filters, 3×3) → ReLU → MaxPool
→ FC6 (4096 units) → ReLU → Dropout
→ FC7 (4096 units) → ReLU → Dropout
→ FC8 (1000 units) → Softmax
```

Total parameters: ~60 million

### Key Implementation Detail
AlexNet was split across **two GTX 580 GPUs** (3GB VRAM each) — half the feature maps on each GPU, with cross-GPU communication only at certain layers. This was necessary due to memory constraints in 2012.

---

## Key Innovations

### 1. ReLU Activation
- Previous standard: tanh or sigmoid activations
- Problem: Saturating activations cause vanishing gradients in deep networks
- ReLU (Rectified Linear Unit): f(x) = max(0, x) — non-saturating, trains 6x faster than tanh
- **Still the default activation in most networks today**

### 2. GPU Training
- First major network to train on GPUs
- ~5-6 days training on 2 GPUs — impractical on CPU
- Demonstrated that GPU computing was the future of deep learning
- Triggered the entire GPU deep learning industry

### 3. Dropout
- Applied to fully connected layers with p=0.5
- Randomly zeroes half of neurons during each forward pass
- Acts as regularization — prevents co-adaptation of neurons
- Halves the effective number of parameters without reducing capacity
- (Later formalized in the Dropout paper by Srivastava et al., 2014)

### 4. Data Augmentation
- Random crops (256×256 → 224×224)
- Horizontal reflections
- PCA color augmentation
- Multiplied effective dataset size, reduced overfitting

### 5. Local Response Normalization (LRN)
- Normalizes activity across neighboring feature maps
- Inspired by neuroscience (lateral inhibition)
- Later found to be less important — Batch Normalization superseded it

---

## Results

- **ILSVRC 2012**: 15.3% top-5 error (2nd place: 26.2%)
- **ILSVRC 2012 top-1**: 37.5% error
- The margin of victory (~11 percentage points) was unprecedented in any ML competition

---

## Why AlexNet Changed Everything

1. **Proved deep learning could scale**: Skeptics believed deep networks were untrainable — AlexNet proved them wrong
2. **GPU computing became central**: Every lab immediately switched to GPU training
3. **Feature learning won over feature engineering**: Hand-crafted features (SIFT, HOG) were abandoned
4. **Started the ImageNet race**: Triggered years of rapid architecture improvements (ZFNet, VGG, GoogLeNet, ResNet)
5. **Transfer learning**: AlexNet features trained on ImageNet transferred to other vision tasks
6. **Hinton's influence**: Demonstrated the power of Hinton's connectionist/neural network approach after decades of skepticism

---

## Path from AlexNet to Modern Models

| Year | Model | Top-5 Error | Innovation |
|------|-------|-------------|------------|
| 2012 | AlexNet | 15.3% | Deep CNNs, GPU, ReLU |
| 2013 | ZFNet | 11.2% | Visualizing features |
| 2014 | VGG | 7.3% | Deeper, smaller filters |
| 2014 | GoogLeNet | 6.7% | Inception modules |
| 2015 | ResNet | 3.57% | Residual connections |
| 2017 | SENet | 2.25% | Channel attention |
| 2020 | ViT | ~2% | Pure attention, no conv |

---

## Key Terms

- **CNN (Convolutional Neural Network)**: Network using convolutional layers to learn spatial features
- **ReLU**: Rectified Linear Unit — f(x) = max(0, x), non-saturating activation
- **Dropout**: Randomly zeroing neurons during training for regularization
- **Data augmentation**: Artificially expanding training data via transformations
- **Top-5 error**: Fraction of test images where correct class is not in top 5 predictions
- **ILSVRC**: ImageNet Large Scale Visual Recognition Challenge — annual competition 2010-2017

---

## Authors

- **Alex Krizhevsky** — PhD student at University of Toronto; AlexNet named after him; later joined Google
- **Ilya Sutskever** — PhD student at University of Toronto; later co-founded OpenAI
- **Geoffrey E. Hinton** — Professor, University of Toronto; "Godfather of Deep Learning"; won Turing Award 2018; later joined Google Brain

---

## Citation

Krizhevsky, A., Sutskever, I., & Hinton, G. E. (2012). ImageNet classification with deep convolutional neural networks. *Advances in Neural Information Processing Systems*, 25, 1097–1105.
