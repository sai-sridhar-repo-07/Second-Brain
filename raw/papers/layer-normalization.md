# Layer Normalization

**Authors**: Jimmy Lei Ba, Jamie Ryan Kiros, Geoffrey E. Hinton
**Institution**: University of Toronto
**Published**: 2016 (arXiv preprint)

---

## Overview

Layer Normalization (LayerNorm) normalizes the inputs across the feature dimension for each individual sample, rather than across the batch dimension like Batch Normalization. This makes it batch-size independent and well-suited for sequence models like Transformers and RNNs. LayerNorm is a critical component of every Transformer architecture and is used in all modern LLMs.

---

## The Problem with BatchNorm for Sequences

BatchNorm computes statistics across the mini-batch dimension. This fails for:
- **Variable-length sequences**: Different samples in a batch have different lengths
- **Small batches**: Statistics become noisy and unstable
- **RNNs**: Each timestep has a different distribution; batch stats don't capture this well
- **Online/streaming inference**: Can't compute batch statistics for single samples

---

## Layer Normalization Formula

For a single sample with H features in a layer:

```
μ = (1/H) Σ a_i              # mean over features
σ² = (1/H) Σ (a_i - μ)²     # variance over features
â_i = (a_i - μ) / sqrt(σ² + ε)   # normalize
y_i = g_i * â_i + b_i        # scale (g) and shift (b)
```

Where g and b are learnable per-feature scale and shift parameters.

Key difference from BatchNorm: statistics are computed over the feature dimension (H) for a single sample, not over the batch dimension.

---

## BatchNorm vs LayerNorm

| Property | BatchNorm | LayerNorm |
|----------|-----------|-----------|
| Normalizes over | Batch dimension | Feature dimension |
| Per-sample statistics | No | Yes |
| Batch-size dependent | Yes | No |
| Works for sequences | Poorly | Yes |
| Used in CNNs | Standard | Rarely |
| Used in Transformers | No | Standard |
| Train/inference mismatch | Yes | No |

---

## Why LayerNorm Works for Transformers

In a Transformer, each position in a sequence is processed independently. LayerNorm normalizes the embedding dimension for each position independently:

```
Input shape: [batch, sequence_length, d_model]
LayerNorm normalizes over: [d_model] for each (batch, position)
```

This ensures each token's representation has consistent scale, regardless of batch size or sequence length.

---

## Placement in Transformers

Two common variants:
- **Post-LN** (original Transformer): LayerNorm applied after residual addition: `LayerNorm(x + sublayer(x))`
- **Pre-LN** (modern standard): LayerNorm applied before sublayer: `x + sublayer(LayerNorm(x))`

Pre-LN is more stable and has become standard in modern LLMs (GPT-3, LLaMA, Claude). It allows training without learning rate warmup in some cases.

---

## Variants

- **RMSNorm** (Zhang & Sennrich, 2019): Simplifies LayerNorm by removing mean centering — only normalizes by root mean square. Used in LLaMA, Mistral, and many modern LLMs. ~10-15% faster than full LayerNorm.
- **Group Normalization**: Normalizes over groups of channels — between BatchNorm and LayerNorm
- **Power Normalization**: Replaces L2 norm with Lp norm

---

## RMSNorm (Commonly Used Variant)

```
RMSNorm(x) = x / RMS(x) * g
where RMS(x) = sqrt((1/H) Σ x_i²)
```

Removes the mean subtraction step — empirically equivalent to LayerNorm in practice, but cheaper to compute. Adopted by LLaMA, Mistral, Falcon, and most modern open-source LLMs.

---

## Key Terms

- **Feature dimension normalization**: Computing statistics across the embedding/hidden dim for one sample
- **g (scale) and b (bias)**: Learnable parameters restoring the network's expressive capacity
- **Pre-LN vs Post-LN**: Where LayerNorm is placed relative to the residual connection
- **RMSNorm**: Simplified LayerNorm without mean centering — faster, widely used in modern LLMs

---

## Authors

- **Jimmy Lei Ba** — University of Toronto; also co-authored Adam optimizer
- **Jamie Ryan Kiros** — University of Toronto; visual-semantic embedding researcher
- **Geoffrey E. Hinton** — University of Toronto; Turing Award winner; Godfather of Deep Learning

---

## Citation

Ba, J. L., Kiros, J. R., & Hinton, G. E. (2016). Layer normalization. *arXiv preprint arXiv:1607.06450*.
