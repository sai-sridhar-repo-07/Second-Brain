# Self-Attention

Self-attention is a mechanism that allows each token in a sequence to directly attend to every other token in the same sequence, computing a weighted representation based on relevance. Unlike RNNs, there is no sequential dependency — all positions are processed in parallel.

## How Sources Explain This
- **[[attention-is-all-you-need]]**: Defines self-attention using Query, Key, Value projections. Each token produces a Q (what it's looking for), K (what it offers), and V (its content). Attention scores are computed as `softmax(QK^T / sqrt(d_k)) * V`. The scaling by `sqrt(d_k)` prevents softmax from entering regions of extremely small gradients.

## Why It Matters for AI Implementation
- Enables **full parallelization** during training — no sequential bottleneck
- Creates **O(1) path length** between any two tokens — long-range dependencies are learned easily
- Attention weights are partially interpretable — useful for debugging model behavior

## Contradictions or Variations
- High attention weight does not necessarily equal causal importance — research has shown attention can be misleading as an explanation mechanism
- Variants like **sparse attention**, **linear attention**, and **local attention** trade exactness for efficiency

## Related Concepts
- [[multi-head-attention]]
- [[transformer-architecture]]
- [[positional-encoding]]
- [[cross-attention]]

`Source: [[attention-is-all-you-need]]`
