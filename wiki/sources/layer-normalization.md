# Layer Normalization

University of Toronto's 2016 paper introducing Layer Normalization — normalizing across the feature dimension for a single sample rather than across the batch. Critical for Transformer training; standard in all LLMs.

## Key Contributions
- Normalizes over feature dimension (d_model) per sample — batch-size independent
- Works for variable-length sequences and RNNs (unlike BatchNorm)
- No train/inference mismatch
- Pre-LN variant (normalize before sublayer) is more stable than Post-LN

## Variants
- **RMSNorm**: Removes mean centering — just normalizes by root mean square. Used in LLaMA, Mistral, most modern LLMs. Faster than full LayerNorm.

## Related Concepts
- [[normalization-techniques]]
- [[transformer-architecture]]

## Related Entities
- [[jimmy-ba]]
- [[geoffrey-hinton]]

`Source: raw/layer-normalization.md`
