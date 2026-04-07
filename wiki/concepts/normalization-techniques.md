# Normalization Techniques

Normalization layers stabilize neural network training by transforming activations to have consistent statistics. They appear in every modern deep learning architecture and differ in what dimension they normalize over and when they compute statistics.

## How Sources Explain This
- **[[batch-normalization]]**: Normalizes over the batch dimension — zero mean, unit variance per feature. Requires large batches; causes train/inference mismatch. Standard in CNNs.
- **[[layer-normalization]]**: Normalizes over the feature dimension for each individual sample. Batch-size independent; no train/inference mismatch. Standard in Transformers and LLMs.

## Methods Comparison

| Method | Normalizes over | Best for | Notes |
|--------|----------------|----------|-------|
| BatchNorm | Batch | CNNs, vision | Fails with small batches |
| LayerNorm | Features (per sample) | Transformers, LLMs | Standard in all modern LLMs |
| InstanceNorm | Spatial (per channel per sample) | Style transfer | |
| GroupNorm | Channel groups | Small-batch vision | Between BN and IN |
| RMSNorm | RMS over features | LLMs (LLaMA, Mistral) | Faster than LayerNorm |

## Contradictions or Variations
- Original Transformer (2017): Post-LN placement. Modern LLMs: Pre-LN (before sublayer) — more stable, no warmup needed
- RMSNorm removes mean centering from LayerNorm — empirically equivalent, faster. Adopted by LLaMA, Mistral, Falcon

## Related Concepts
- [[transformer-architecture]]
- [[residual-connections]]
