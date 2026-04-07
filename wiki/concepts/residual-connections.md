# Residual Connections

A residual connection (skip connection) adds the input of a layer directly to its output: `output = F(x) + x`. The layer learns the residual (what to add) rather than the full transformation. This enables training of very deep networks by ensuring gradient flow and making identity mappings easy to learn.

## How Sources Explain This
- **[[resnet]]**: Introduced residual connections to solve the degradation problem — deeper networks performing worse than shallower ones. Skip connections allow gradients to flow directly to early layers; identity mapping is learned when F(x)=0.
- **[[attention-is-all-you-need]]**: Every Transformer layer wraps each sublayer with a residual connection: `LayerNorm(x + sublayer(x))`. This is directly borrowed from ResNet and is essential for training deep Transformers.
- **[[layer-normalization]]**: Placed around residual connections in Transformers. Pre-LN: `x + sublayer(LayerNorm(x))` is more stable than Post-LN.

## Why It Matters
- Without residuals, deep networks suffer from vanishing gradients
- With residuals, adding more layers never hurts (worst case: layer learns identity)
- Universal in modern deep learning: CNNs, Transformers, diffusion U-Nets, all use skip connections

## Related Concepts
- [[transformer-architecture]]
- [[normalization-techniques]]
