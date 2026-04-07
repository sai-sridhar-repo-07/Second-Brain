# Dropout: A Simple Way to Prevent Neural Networks from Overfitting

**Authors**: Nitish Srivastava, Geoffrey Hinton, Alex Krizhevsky, Ilya Sutskever, Ruslan Salakhutdinov
**Institution**: University of Toronto
**Published**: 2014 (JMLR 2014)

---

## Overview

Dropout is a regularization technique that randomly sets a fraction of neuron activations to zero during each training forward pass. At inference, all neurons are used but their outputs are scaled by the dropout probability. Dropout prevents co-adaptation of neurons (where neurons become dependent on each other), effectively training an ensemble of many subnetworks. It became a standard regularization technique and was first used in AlexNet (2012) before being formally published.

---

## The Problem: Overfitting in Large Networks

Large neural networks have millions of parameters and can perfectly memorize training data. Overfitting occurs when:
- Training accuracy is high but test accuracy is low
- Neurons learn to co-adapt — a neuron corrects the errors of others, becoming overly specialized
- Adding more data or reducing model size both have costs

---

## The Solution: Random Neuron Dropout

During each training step, independently set each neuron's activation to zero with probability p (typically 0.5):

```
# During training
mask ~ Bernoulli(1-p)        # 1 with probability (1-p), 0 with probability p
output = activation * mask   # zero out dropped neurons

# During inference  
output = activation * (1-p)  # scale down to match expected training output
```

Or equivalently, use **inverted dropout** (more common in practice):
```
# During training
mask ~ Bernoulli(1-p)
output = activation * mask / (1-p)   # scale up during training

# During inference
output = activation   # no scaling needed
```

---

## Why Dropout Works

### Ensemble Interpretation
With n neurons and dropout probability p, there are 2^n possible subnetworks. Each forward pass trains a different subnetwork. At inference, the full network approximates averaging over all these subnetworks — implicit ensemble.

### Co-adaptation Prevention
A neuron cannot rely on specific other neurons being present. Each neuron must learn useful features independently. This forces more robust, distributed representations.

### Noise as Regularization
Dropout adds multiplicative noise to activations. Noisy training forces the network to be robust to perturbations in its internal representations.

---

## Where to Apply Dropout

- **Fully connected layers**: p=0.5 is typical (drops 50% of neurons)
- **Convolutional layers**: p=0.1 to 0.3 (spatial features are more structured, drop less)
- **Input layer**: p=0.2 occasionally used
- **Attention layers**: Used in Transformers for attention weights (p=0.1 typical)
- **NOT between conv layers**: Usually not between every conv layer in modern CNNs

---

## Dropout in Transformers

The original Transformer paper uses dropout on:
- Attention weights
- Residual connections (before adding to sublayer output)
- Embeddings

Modern LLMs typically use dropout at p=0.0 to 0.1 during pre-training (less regularization needed at scale), but higher dropout when fine-tuning on small datasets.

---

## Variants

- **DropConnect**: Drops individual weights instead of neurons
- **SpatialDropout**: Drops entire feature maps (channels) — better for CNNs
- **DropPath / Stochastic Depth**: Drops entire layers randomly — used in ViT, EfficientNet
- **Monte Carlo Dropout**: Using dropout at inference for uncertainty estimation (Gal & Ghahramani, 2016)

---

## Limitations

- **Slows training**: Network effectively has fewer neurons per step — takes more epochs
- **Not always beneficial**: Large datasets with sufficient diversity may not need dropout
- **Interaction with BatchNorm**: BatchNorm and Dropout can interfere — require careful ordering
- **Obsoleted in some settings**: Weight decay / L2 regularization and data augmentation often substitute for dropout in modern vision models

---

## Key Terms

- **Dropout probability p**: Fraction of neurons zeroed out each step (p=0.5 → 50% dropped)
- **Keep probability (1-p)**: Fraction of neurons retained
- **Inverted dropout**: Scaling activations by 1/(1-p) during training so inference needs no change
- **Co-adaptation**: Neurons becoming dependent on specific other neurons — what dropout prevents
- **Ensemble**: Averaging predictions from multiple models — what dropout approximates

---

## Authors

- **Nitish Srivastava** — University of Toronto; PhD student, lead author
- **Geoffrey Hinton** — University of Toronto; supervisor; Turing Award winner
- **Alex Krizhevsky** — University of Toronto; also lead author of AlexNet
- **Ilya Sutskever** — University of Toronto; later co-founded OpenAI
- **Ruslan Salakhutdinov** — University of Toronto; later Professor at CMU

---

## Citation

Srivastava, N., Hinton, G., Krizhevsky, A., Sutskever, I., & Salakhutdinov, R. (2014). Dropout: A simple way to prevent neural networks from overfitting. *Journal of Machine Learning Research*, 15(1), 1929–1958.
