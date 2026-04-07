# Adam: A Method for Stochastic Optimization

Kingma & Ba's 2014 paper introducing the Adam optimizer — combining momentum (first moment) and adaptive learning rates (second moment). Now the most widely used optimizer in deep learning, with AdamW as the standard for LLM training.

## Key Contributions
- Maintains per-parameter adaptive learning rates
- First moment (m): exponential moving average of gradients (momentum)
- Second moment (v): exponential moving average of squared gradients (adaptive scale)
- Bias correction for initialization
- Default hyperparameters (β₁=0.9, β₂=0.999, ε=1e-8) work well across tasks

## Variants
- **AdamW**: Decoupled weight decay — standard for all LLM training
- **RAdam**: Built-in warmup
- **Lamb**: Large-batch variant used for BERT

## Related Concepts
- [[optimization-algorithms]]

## Related Entities
- [[diederik-kingma]]
- [[jimmy-ba]]

`Source: raw/adam-optimizer.md`
