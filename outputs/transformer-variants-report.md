# Transformer Variants — Comparison Report

**Generated**: 2026-04-07
**Sources consulted**: [[transformer-architecture]], [[encoder-decoder]], [[positional-encoding]], [[attention-is-all-you-need]]

---

## 1. The Three Main Transformer Variants

All modern AI models are built on the Transformer, but they use different subsets of the architecture depending on what task they're designed for.

### Encoder-Decoder (Original)
**Examples**: Original Transformer (2017), T5, BART

| Property | Detail |
|----------|--------|
| What it does | Encoder reads full input → Decoder generates output |
| Attention type | Encoder: bidirectional self-attention. Decoder: masked self-attention + cross-attention to encoder |
| Best for | Translation, summarization, structured generation |
| Key trait | Input and output are treated as separate sequences |

The encoder sees the whole input at once (no masking). The decoder generates one token at a time and looks back at the encoder's output via **cross-attention** at every step.

---

### Encoder-Only
**Examples**: BERT, RoBERTa

| Property | Detail |
|----------|--------|
| What it does | Reads and understands text, does not generate |
| Attention type | Fully bidirectional — every token sees every other token |
| Best for | Classification, named entity recognition, search/retrieval |
| Key trait | No autoregressive generation — processes entire input at once |

Because it's bidirectional, it builds richer representations of existing text. The tradeoff: it cannot generate new text.

---

### Decoder-Only
**Examples**: GPT, Claude, LLaMA, Mistral, Gemini

| Property | Detail |
|----------|--------|
| What it does | Generates text autoregressively |
| Attention type | Masked self-attention — each token only sees tokens before it |
| Best for | Chat, code generation, reasoning, instruction following |
| Key trait | Input and output live in the same context window |

This is now the **dominant pattern** for LLMs. The model reads your prompt and continues generating tokens one at a time, each conditioned on everything before it.

---

## 2. Side-by-Side Comparison

| Feature | Encoder-Decoder | Encoder-Only | Decoder-Only |
|---------|----------------|--------------|--------------|
| Can generate text | Yes | No | Yes |
| Bidirectional context | Encoder only | Yes (full) | No (masked) |
| Cross-attention | Yes | No | No |
| Used in modern LLMs | Rarely | Rarely | Yes (dominant) |
| Examples | T5, BART | BERT, RoBERTa | Claude, GPT, LLaMA |
| Best use case | Translation, summarization | Classification, retrieval | Generation, chat, reasoning |

---

## 3. Positional Encoding Variants

A separate but related dimension of variation — how models inject token order:

| Method | Used In | How It Works | Key Property |
|--------|---------|--------------|--------------|
| Sinusoidal (original) | Original Transformer | Fixed sine/cosine functions | Generalizes to unseen lengths |
| Learned embeddings | BERT, GPT-2 | Trainable position vectors | Performs well, doesn't generalize past training length |
| Relative (T5, Shaw) | T5 | Encodes distance between tokens | Better for structure-sensitive tasks |
| RoPE | LLaMA, Mistral, Claude | Rotates Q/K vectors by position | Strong length generalization, now widely adopted |
| ALiBi | Some open models | Adds distance bias to attention scores | Simple, no embedding overhead |

---

## 4. Key Takeaway for AI Implementation

If you're building on top of LLMs (Claude, GPT, LLaMA):
- You're working with **decoder-only** models
- They have a **context window** (not separate encoder/decoder)
- Positional encoding is likely **RoPE** — this is why models can sometimes handle longer contexts than their training length

If you're building **retrieval or classification** systems:
- Encoder-only models (like `text-embedding-ada-002` or `nomic-embed`) are often used for embeddings
- They produce richer representations because they're bidirectional

---

## Sources
- [[attention-is-all-you-need]]
- [[transformer-architecture]]
- [[encoder-decoder]]
- [[positional-encoding]]
