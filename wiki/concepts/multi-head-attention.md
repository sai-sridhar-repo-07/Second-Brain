# Multi-Head Attention

Multi-head attention runs self-attention multiple times in parallel with different learned projections, then concatenates the results. Each "head" specializes in attending to different aspects of the input — one head may track syntactic dependencies, another coreference, another semantic similarity.

## How Sources Explain This
- **[[attention-is-all-you-need]]**: Uses 8 heads with `d_model=512`, so each head operates in dimension 64. The outputs of all heads are concatenated and projected back to `d_model`. Formula: `MultiHead(Q,K,V) = Concat(head_1,...,head_h) * W_O`

## Why It Matters for AI Implementation
- Multiple heads allow the model to capture **multiple types of relationships** simultaneously
- A single attention head can only produce one weighted average per position — multiple heads break this limitation
- In practice, different heads in trained LLMs attend to different structural patterns

## Contradictions or Variations
- Not all heads are equally useful — research shows many heads can be pruned with minimal performance loss
- The optimal number of heads varies; more is not always better

## Related Concepts
- [[self-attention]]
- [[transformer-architecture]]
- [[encoder-decoder]]

`Source: [[attention-is-all-you-need]]`
