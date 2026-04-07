# Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift

**Authors**: Sergey Ioffe, Christian Szegedy
**Institution**: Google
**Published**: 2015 (ICML 2015)

---

## Overview

Batch Normalization (BatchNorm) normalizes the inputs to each layer during training, using statistics computed over the current mini-batch. It dramatically stabilized and accelerated deep network training, allowing much higher learning rates and reducing dependence on careful initialization. It became a standard component of CNNs through 2015-2020 and enabled the rapid progress in image recognition during that period.

---

## The Problem: Internal Covariate Shift

As a network trains, the distribution of each layer's inputs changes as parameters in previous layers update. This is called **internal covariate shift**. Each layer must constantly adapt to a shifting input distribution, slowing training and requiring careful learning rate tuning and initialization.

---

## The Solution: Normalize Per Layer

For each mini-batch, normalize each feature dimension to have zero mean and unit variance, then apply learnable scale (γ) and shift (β):

```
μ_B = (1/m) Σ x_i                    # batch mean
σ²_B = (1/m) Σ (x_i - μ_B)²         # batch variance
x̂_i = (x_i - μ_B) / sqrt(σ²_B + ε)  # normalize
y_i = γ * x̂_i + β                   # scale and shift
```

The learnable γ (scale) and β (shift) let the network undo normalization if that's optimal — preserving model capacity while still benefiting from stable training.

---

## Benefits

1. **Higher learning rates**: With stable activations, learning rates can be 10-100x higher
2. **Less sensitive to initialization**: Distribution is normalized regardless of weight init
3. **Regularization effect**: Adding noise via batch statistics — can reduce need for Dropout
4. **Faster convergence**: Training runs significantly fewer epochs to reach same accuracy

---

## Where It's Placed

Typically inserted between a linear/convolutional layer and its activation function:
```
Conv → BatchNorm → ReLU   (most common)
```
Some variants place it after activation.

---

## Train vs Inference Behavior

- **Training**: Normalizes using statistics of the current mini-batch
- **Inference**: Uses running averages of mean and variance accumulated during training (fixed statistics)

This train/inference discrepancy can cause issues if batch sizes are very small or if inference batches differ from training distribution.

---

## Limitations

- **Batch size dependency**: Performance degrades with very small batches (batch size < 8)
- **Sequence models**: Ineffective for RNNs/Transformers — each timestep has different statistics
- **Train/inference mismatch**: Running statistics can diverge from actual distribution
- **Not suitable for online learning**: Can't compute batch statistics one sample at a time

---

## Successors

- **Layer Normalization** (Ba et al., 2016): Normalizes across features for a single sample — works for Transformers and RNNs
- **Instance Normalization**: Normalizes per-sample per-channel — used in style transfer
- **Group Normalization**: Normalizes across groups of channels — works with small batches
- **RMS Norm**: Simplified layer norm without mean centering — used in LLaMA, Mistral

---

## Impact

BatchNorm enabled VGGNet, GoogLeNet's Inception modules, and the progression toward ResNet. It was the standard normalization for CNNs until vision transformers shifted the field toward Layer Normalization. In practice, every modern CNN still uses BatchNorm or a variant.

---

## Key Terms

- **Internal covariate shift**: Changing input distribution of a layer as earlier layers update
- **Normalization**: Transforming data to have zero mean, unit variance
- **γ (scale) and β (shift)**: Learnable parameters that restore the network's expressive power
- **Running statistics**: Accumulated mean/variance used at inference

---

## Authors

- **Sergey Ioffe** — Google; also known for work on probabilistic models
- **Christian Szegedy** — Google; lead architect of GoogLeNet/Inception

---

## Citation

Ioffe, S., & Szegedy, C. (2015). Batch normalization: Accelerating deep network training by reducing internal covariate shift. *Proceedings of the 32nd International Conference on Machine Learning*, 448–456.
