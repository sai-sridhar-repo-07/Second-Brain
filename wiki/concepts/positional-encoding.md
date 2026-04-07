# Positional Encoding

Positional encoding is a technique for injecting information about token order into a Transformer, which otherwise treats input as a set (order-agnostic). Without positional encoding, "the cat sat on the mat" and "the mat sat on the cat" would produce identical representations.

## How Sources Explain This
- **[[attention-is-all-you-need]]**: Uses sinusoidal functions of different frequencies added to token embeddings before the first layer. Even positions use sine, odd positions use cosine: `PE(pos, 2i) = sin(pos / 10000^(2i/d_model))`. This design was chosen so the model can attend to relative positions — the encoding of position `pos+k` is a linear function of `pos`.

## Contradictions or Variations
- Sinusoidal encoding (original) vs **learned positional embeddings** (used in BERT, GPT-2): Learned embeddings perform similarly but don't generalize to unseen lengths
- **Relative positional encodings** (T5, Shaw et al.): Encode distance between tokens rather than absolute position — better for tasks requiring relative structure
- **RoPE** (Rotary Position Embedding): Used in LLaMA, Mistral, Claude — rotates Q/K vectors, enabling better length generalization
- **ALiBi**: Adds a bias to attention scores proportional to distance — no encoding in the embedding itself

## Related Concepts
- [[transformer-architecture]]
- [[self-attention]]

`Source: [[attention-is-all-you-need]]`
