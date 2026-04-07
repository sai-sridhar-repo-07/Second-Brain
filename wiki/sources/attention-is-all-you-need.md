# Attention Is All You Need

Published in 2017 by researchers at Google Brain and Google Research, this paper introduced the Transformer architecture — replacing recurrent and convolutional layers entirely with self-attention. It became the foundation of every modern large language model.

## Key Contributions
- Introduced the **Transformer**: an encoder-decoder architecture using only attention and feed-forward layers
- Proposed **multi-head attention**: running attention in parallel across multiple learned subspaces
- Showed that self-attention alone achieves better translation quality than RNN-based models, in less training time
- Introduced **scaled dot-product attention** with the formula: `softmax(QK^T / sqrt(d_k)) * V`

## Core Architecture
- **Encoder**: 6 stacked layers of multi-head self-attention + feed-forward network
- **Decoder**: 6 stacked layers of masked self-attention + cross-attention + feed-forward network
- **Positional encoding**: Sinusoidal functions added to embeddings to inject position information
- **Residual connections + layer norm** around every sub-layer

## Results
- WMT 2014 EN→DE: 28.4 BLEU (new SOTA, beat prior ensembles)
- WMT 2014 EN→FR: 41.0 BLEU (new SOTA)
- Trained in 3.5 days on 8 P100 GPUs — much faster than prior models

## Limitations
- O(n²) attention complexity — expensive for long sequences
- No inherent positional awareness — requires explicit positional encoding
- Attention weight ≠ causal importance (interpretability debate)

## Impact
Led directly to [[bert]], [[gpt]], and all modern LLMs including Claude, Gemini, and LLaMA. Extended beyond NLP to vision ([[vision-transformer]]), audio, and multimodal models.

## Related Concepts
- [[self-attention]]
- [[multi-head-attention]]
- [[transformer-architecture]]
- [[positional-encoding]]
- [[encoder-decoder]]

## Related Entities
- [[ashish-vaswani]]
- [[noam-shazeer]]
- [[aidan-gomez]]
- [[google-brain]]

`Source: raw/attention-is-all-you-need.md`
