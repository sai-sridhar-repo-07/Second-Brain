# Optimization Algorithms

Optimization algorithms update neural network weights to minimize the training loss. The choice of optimizer affects convergence speed, final performance, and required compute. AdamW is standard for LLMs; SGD with momentum remains competitive for vision.

## How Sources Explain This
- **[[adam-optimizer]]**: Adam maintains per-parameter adaptive learning rates using first moment (gradient mean/momentum) and second moment (gradient variance). Bias correction stabilizes early training. Default β₁=0.9, β₂=0.999 work across most tasks. AdamW decouples weight decay — standard for all LLM training.

## Key Algorithms

| Algorithm | Key Feature | Common Use |
|-----------|-------------|------------|
| SGD | Baseline — fixed global LR | Rarely used alone |
| SGD + Momentum | Smooths oscillations | Vision (ResNet, ViT) |
| AdaGrad | Decays LR per parameter | Sparse features |
| RMSprop | Moving avg of squared gradients | RNNs |
| Adam | Momentum + adaptive LR | Default for most DL |
| AdamW | Adam + decoupled weight decay | All LLM training |
| Lion | Sign of gradient update | Efficient alternative |

## Contradictions or Variations
- SGD + momentum sometimes achieves better final accuracy on image classification than Adam — but requires careful LR scheduling
- For LLMs: AdamW is universal; alternatives (Lion, Adafactor) used to reduce memory or cost
- Gradient clipping (clip norm to 1.0) is typically combined with Adam for LLMs

## Related Concepts
- [[pre-training-and-fine-tuning]]
- [[scaling-laws]]
