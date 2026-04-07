# Encoder-Decoder Architecture

The encoder-decoder pattern splits a sequence model into two components: an encoder that processes and compresses the full input into representations, and a decoder that generates output autoregressively while attending to those representations via cross-attention.

## How Sources Explain This
- **[[attention-is-all-you-need]]**: The encoder reads the entire source sentence at once (bidirectional attention). The decoder generates output one token at a time — it uses masked self-attention (can't see future tokens) plus cross-attention to the encoder output. This is the original Transformer design, optimized for translation.

## Variants
- **Encoder-only** (BERT, RoBERTa): No decoder. Used for classification, extraction, understanding. Bidirectional context.
- **Decoder-only** (GPT, Claude, LLaMA): No separate encoder. Input and output share the same context. Autoregressive generation only. Now the dominant LLM pattern.
- **Encoder-decoder** (T5, BART, original Transformer): Still used for translation, summarization, structured generation tasks.

## Related Concepts
- [[transformer-architecture]]
- [[self-attention]]
- [[multi-head-attention]]

`Source: [[attention-is-all-you-need]]`
