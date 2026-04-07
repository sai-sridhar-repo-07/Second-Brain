# Adam: A Method for Stochastic Optimization

**Authors**: Diederik P. Kingma, Jimmy Ba
**Institution**: University of Amsterdam / University of Toronto
**Published**: 2014 (ICLR 2015)

---

## Overview

Adam (Adaptive Moment Estimation) is an optimization algorithm that combines the advantages of two earlier methods — AdaGrad (adapts learning rates per parameter) and RMSprop (uses moving average of squared gradients). Adam maintains per-parameter learning rates that adapt based on first and second moments of gradients. It is the most widely used optimizer in deep learning today, serving as the default for training LLMs, CNNs, and virtually all modern neural networks.

---

## The Problem with SGD

Standard Stochastic Gradient Descent (SGD) uses a single global learning rate:
```
θ = θ - η * ∇L(θ)
```

Problems:
- Same learning rate for all parameters — suboptimal when gradients vary wildly across dimensions
- Requires manual tuning of learning rate and schedule
- Slow convergence in ravines (common in neural network loss landscapes)
- Sensitive to initialization

---

## The Adam Algorithm

Adam maintains two moving averages (moments) for each parameter:
- **m_t** (first moment): exponential moving average of gradients (like momentum)
- **v_t** (second moment): exponential moving average of squared gradients (like RMSprop)

```
m_t = β₁ * m_{t-1} + (1 - β₁) * g_t        # gradient mean
v_t = β₂ * v_{t-1} + (1 - β₂) * g_t²       # gradient variance

m̂_t = m_t / (1 - β₁^t)                      # bias correction
v̂_t = v_t / (1 - β₂^t)                      # bias correction

θ_t = θ_{t-1} - η * m̂_t / (sqrt(v̂_t) + ε)
```

### Default Hyperparameters
- **β₁ = 0.9** (first moment decay)
- **β₂ = 0.999** (second moment decay)
- **ε = 1e-8** (numerical stability)
- **η = 0.001** (learning rate — usually the only thing tuned)

---

## Bias Correction

Early in training, m_t and v_t are initialized at 0 and are biased toward zero. The bias-correction terms (dividing by 1 - β^t) counteract this — critical in the first few training steps.

---

## Why Adam Works

- **Per-parameter learning rates**: Parameters with large gradients get smaller effective learning rates; sparse parameters (small gradients) get larger updates
- **Momentum**: m_t acts like momentum — smooths out oscillations, accelerates in consistent directions
- **Adaptive scaling**: v_t normalizes gradient magnitude — robust to gradient scale differences across layers
- **Low memory**: Only stores two extra vectors per parameter — O(n) overhead

---

## Variants

- **AdamW** (Loshchilov & Hutter, 2017): Decouples weight decay from gradient update — fixes a bug in Adam's L2 regularization. **Standard for LLM training.**
- **AMSGrad**: Uses maximum of past squared gradients — theoretically convergent but rarely better in practice
- **RAdam** (Liu et al., 2019): Rectified Adam — warm-up built in, stabilizes early training
- **Lamb** (You et al., 2019): Large-batch Adam variant — used for BERT training
- **Lion** (Chen et al., 2023): Google's optimizer using sign of gradient — more memory efficient

---

## Adam vs SGD with Momentum

| Property | Adam | SGD + Momentum |
|----------|------|----------------|
| Learning rate tuning | Minimal (default often works) | Critical, requires schedule |
| Convergence speed | Fast initially | Slower initially |
| Final performance | Sometimes slightly worse | Sometimes slightly better |
| LLM training | Standard | Rarely used |
| Vision training | Common | Still competitive |

SGD with momentum sometimes achieves better final accuracy on image classification — but requires careful learning rate scheduling and longer training. For LLMs, Adam/AdamW is universal.

---

## Usage in Practice

- **LLM training**: AdamW is standard (GPT, BERT, LLaMA, Claude all trained with AdamW)
- **Default learning rate**: 1e-4 to 3e-4 for most tasks
- **Weight decay**: 0.01 to 0.1 with AdamW
- **Gradient clipping**: Often combined with Adam to prevent gradient explosions (clip norm to 1.0)

---

## Key Terms

- **First moment (m_t)**: Exponential moving average of gradients — captures direction
- **Second moment (v_t)**: Exponential moving average of squared gradients — captures magnitude
- **Bias correction**: Adjusting moments for initialization at zero
- **AdamW**: Adam with decoupled weight decay — standard for LLMs
- **Adaptive learning rate**: Per-parameter learning rate scaling based on gradient history

---

## Authors

- **Diederik P. Kingma** — University of Amsterdam; also invented VAE (Variational Autoencoders)
- **Jimmy Ba** — University of Toronto; also co-authored Layer Normalization

---

## Citation

Kingma, D. P., & Ba, J. (2014). Adam: A method for stochastic optimization. *arXiv preprint arXiv:1412.6980*.
