# Batch Normalization: Accelerating Deep Network Training

Google's 2015 paper introducing Batch Normalization — normalizing layer inputs across the mini-batch to have zero mean and unit variance. Dramatically stabilized and accelerated CNN training; standard in vision models until Transformers popularized Layer Normalization.

## Key Contributions
- Normalizes using batch statistics: `x̂ = (x - μ_B) / sqrt(σ²_B + ε)`
- Learnable scale (γ) and shift (β) restore model capacity
- Enables much higher learning rates and less sensitive initialization
- Provides mild regularization effect

## Limitations
- Batch-size dependent — fails with very small batches
- Train/inference mismatch (uses running statistics at inference)
- Not suitable for sequence models or RNNs → led to [[layer-normalization]]

## Related Concepts
- [[normalization-techniques]]

## Related Entities
- [[christian-szegedy]]
- [[google-brain]]

`Source: raw/batch-normalization.md`
