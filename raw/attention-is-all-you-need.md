# Attention Is All You Need

**Authors**: Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N. Gomez, Łukasz Kaiser, Illia Polosukhin
**Published**: 2017, Google Brain / Google Research
**Venue**: NeurIPS 2017

---

## Overview

"Attention Is All You Need" introduced the Transformer architecture, which replaced recurrent and convolutional layers entirely with a mechanism called self-attention. Published in 2017 by researchers at Google Brain and Google Research, it became one of the most cited and influential papers in the history of machine learning. The Transformer architecture is now the foundation of virtually every modern large language model including GPT, BERT, Claude, Gemini, and LLaMA.

---

## The Problem With Prior Architectures

Before Transformers, sequence-to-sequence tasks (like translation) relied on:

- **RNNs (Recurrent Neural Networks)**: Process tokens one at a time, left to right. This creates a bottleneck — long-range dependencies are hard to learn because information must travel through many time steps.
- **LSTMs / GRUs**: Improved RNNs with gating mechanisms to better handle long sequences, but still fundamentally sequential.
- **CNNs for sequences**: Used in some architectures (e.g., ByteNet, ConvS2S) to parallelize computation, but require many layers to connect distant positions.

Key problems with all of these:
1. **Sequential computation** — can't parallelize across token positions during training
2. **Long-range dependency degradation** — information from early tokens fades over long sequences
3. **Slow training** on long sequences

---

## The Core Idea: Self-Attention

Self-attention allows every token in a sequence to directly attend to every other token, regardless of distance. It computes a weighted sum of all token representations, where the weights are determined by how relevant each token is to the current one.

### How It Works

For each token, three vectors are computed:
- **Query (Q)**: What this token is looking for
- **Key (K)**: What this token offers to others
- **Value (V)**: The actual content this token contributes

The attention score between two tokens is computed as:

```
Attention(Q, K, V) = softmax(QK^T / sqrt(d_k)) * V
```

- `QK^T` — dot product measures similarity between query and key
- `/ sqrt(d_k)` — scaling factor to prevent vanishing gradients in softmax
- `softmax(...)` — converts scores to probabilities (attention weights)
- `* V` — weighted sum of value vectors

### Why This Is Powerful
- Any two tokens can interact directly in a single layer — O(1) path length vs O(n) for RNNs
- Fully parallelizable across all positions
- Attention weights are interpretable — you can see what the model "focuses on"

---

## Multi-Head Attention

Instead of computing one attention function, the Transformer computes attention `h` times in parallel with different learned projections. Each "head" can attend to different aspects of the input (syntax, semantics, coreference, etc.).

```
MultiHead(Q, K, V) = Concat(head_1, ..., head_h) * W_O
where head_i = Attention(Q * W_i_Q, K * W_i_K, V * W_i_V)
```

The paper uses **8 attention heads** with dimension `d_model = 512`.

---

## The Transformer Architecture

### Encoder
Processes the input sequence. Stacked N=6 identical layers, each containing:
1. **Multi-head self-attention** — each position attends to all positions
2. **Feed-forward network** — applied independently to each position
3. **Residual connections + Layer normalization** around each sub-layer

### Decoder
Generates the output sequence. Also N=6 layers, each containing:
1. **Masked multi-head self-attention** — prevents attending to future positions (autoregressive)
2. **Cross-attention** — attends to encoder output (connects encoder to decoder)
3. **Feed-forward network**
4. **Residual connections + Layer normalization**

### Positional Encoding
Since self-attention has no inherent notion of order, the model adds positional encodings to token embeddings. The paper uses sinusoidal functions:

```
PE(pos, 2i)   = sin(pos / 10000^(2i/d_model))
PE(pos, 2i+1) = cos(pos / 10000^(2i/d_model))
```

This lets the model learn relative positions and generalize to longer sequences than seen during training.

---

## Key Design Choices and Their Rationale

| Choice | Reason |
|--------|--------|
| No recurrence | Enables full parallelization |
| Scaled dot-product attention | Avoids gradient issues in high dimensions |
| Multi-head attention | Attends to multiple representation subspaces simultaneously |
| Residual connections | Enables training deep networks (gradient flow) |
| Layer normalization | Stabilizes training |
| Sinusoidal positional encoding | Generalizes to unseen sequence lengths |

---

## Results

Evaluated primarily on machine translation:

- **WMT 2014 English-to-German**: 28.4 BLEU — outperformed all prior models including ensembles
- **WMT 2014 English-to-French**: 41.0 BLEU — new state of the art
- **Training time**: The big Transformer trained in 3.5 days on 8 P100 GPUs — far faster than prior SOTA

The model also showed strong performance on English constituency parsing, demonstrating generalization beyond translation.

---

## Why This Paper Changed Everything

### Immediate Impact
- Enabled BERT (2018) — bidirectional Transformer encoder pre-trained on masked language modeling
- Enabled GPT series (2018–present) — Transformer decoder trained autoregressively
- Replaced RNNs as the dominant architecture for NLP almost overnight

### Long-Term Impact
- Extended to vision (Vision Transformer, ViT 2020)
- Extended to audio, video, multimodal models
- Foundation of every modern LLM: Claude, GPT-4, Gemini, LLaMA, Mistral, etc.
- The scaling laws that govern LLMs (Chinchilla, etc.) are all about Transformer training

### Key Insight That Generalized
Attention is a general-purpose differentiable memory lookup. Given any set of (key, value) pairs and a query, it can softly retrieve relevant information. This abstraction is domain-agnostic — it works on text, images, audio, code, protein sequences, and more.

---

## Limitations Acknowledged in the Paper

- Quadratic complexity in sequence length: O(n²) attention computation — expensive for very long sequences
- No built-in notion of position (requires positional encodings)
- Interpretability of attention weights is debated — high attention weight ≠ causal importance

---

## Subsequent Work Addressing Limitations

- **Sparse attention** (Longformer, BigBird): Reduce O(n²) to O(n log n) or O(n)
- **Relative positional encodings** (T5, RoPE, ALiBi): Better generalization to longer sequences
- **Flash Attention**: IO-aware exact attention that is much faster in practice
- **Linear attention** approximations: Various methods to reduce quadratic cost

---

## Key Terms

- **Self-attention**: A token attending to all other tokens in the same sequence
- **Cross-attention**: Decoder tokens attending to encoder representations
- **Query / Key / Value**: The three projections used to compute attention
- **d_model**: The main hidden dimension (512 in base, 1024 in big model)
- **d_k**: Dimension of queries and keys (d_model / num_heads)
- **Autoregressive**: Generating tokens one at a time, each conditioned on all prior tokens
- **Encoder-decoder**: Architecture where encoder processes input and decoder generates output

---

## Authors

- **Ashish Vaswani** — Google Brain, lead author
- **Noam Shazeer** — Google Brain, co-inventor of many Transformer components, later co-founded Character.AI
- **Niki Parmar** — Google Research
- **Jakob Uszkoreit** — Google Research, later founded Inceptive
- **Llion Jones** — Google Research
- **Aidan N. Gomez** — University of Toronto (intern), later co-founded Cohere
- **Łukasz Kaiser** — Google Brain, also co-authored Tensor2Tensor
- **Illia Polosukhin** — Google Research, later co-founded NEAR Protocol

---

## Citation

Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., Kaiser, Ł., & Polosukhin, I. (2017). Attention is all you need. *Advances in Neural Information Processing Systems*, 30.
