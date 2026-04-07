# Scaling Laws

Scaling laws are quantitative relationships between model performance (loss) and the three axes of scale: parameters (N), training tokens (D), and compute budget (C). They follow smooth power laws across many orders of magnitude, enabling prediction of performance before training.

## How Sources Explain This
- **[[scaling-laws]]** (Kaplan et al.): L(N) ∝ N^(-0.076), L(D) ∝ D^(-0.095), L(C) ∝ C^(-0.050). Compute-optimal: train larger model on fewer tokens (N ∝ C^0.73). Architecture details matter little.
- **[[gpt3]]**: GPT-3's size (175B) was directly informed by Kaplan's scaling laws — expected performance was predictable from the curves.
- **[[scaling-laws]]** (Chinchilla, DeepMind): Revised compute-optimal recipe: 20 tokens per parameter. Smaller model trained longer outperforms larger undertrained model. 70B Chinchilla > 280B Gopher.

## Contradictions or Variations
- Kaplan et al. said: more parameters > more tokens (for fixed compute)
- Chinchilla (Hoffmann et al.) contradicted this: equal scaling of both is optimal; 20 tokens/param
- Scaling laws predict loss, not downstream capabilities — "emergent abilities" appear discontinuously at scale (Wei et al., 2022), which smooth loss curves don't predict

## Related Concepts
- [[pre-training-and-fine-tuning]]
- [[in-context-learning]]
- [[transformer-architecture]]
