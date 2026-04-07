# Transformer Architecture

The Transformer is a neural network architecture built entirely on attention mechanisms and feed-forward layers, with no recurrence or convolution. Introduced in 2017, it became the dominant architecture for language modeling and has since expanded to vision, audio, and multimodal systems.

## How Sources Explain This
- **[[attention-is-all-you-need]]**: Original encoder-decoder design. Encoder processes the full input sequence; decoder generates output autoregressively. Both use stacked layers of multi-head attention + feed-forward networks with residual connections and layer normalization. Key hyperparameters: N=6 layers, d_model=512 (base) or 1024 (big), 8 attention heads.

## Core Components
- **Multi-head self-attention**: Each token attends to all others — see [[multi-head-attention]]
- **Feed-forward network**: Applied position-wise (same weights, each position independently)
- **Residual connections**: `output = LayerNorm(x + sublayer(x))` — enables deep network training
- **Positional encoding**: Injects order information — see [[positional-encoding]]
- **Masked attention** (decoder only): Prevents attending to future tokens during generation

## Contradictions or Variations
- Original paper uses encoder-decoder; modern LLMs (GPT, Claude) use **decoder-only** Transformers
- BERT uses **encoder-only** for classification/understanding tasks
- Positional encoding has evolved significantly since the original sinusoidal approach (RoPE, ALiBi, learned embeddings)

## Related Concepts
- [[self-attention]]
- [[multi-head-attention]]
- [[positional-encoding]]
- [[encoder-decoder]]

## Related Entities
- [[google-brain]]
- [[ashish-vaswani]]

`Source: [[attention-is-all-you-need]]`
