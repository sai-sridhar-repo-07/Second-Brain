# Scaling Laws for Neural Language Models

OpenAI's 2020 paper establishing quantitative power laws governing how language model performance improves with parameters (N), data (D), and compute (C). Scientific foundation for the "bigger is better" era and for making compute-optimal training decisions.

## Key Contributions
- Loss follows smooth power laws: L(N) ∝ N^(-0.076), L(D) ∝ D^(-0.095)
- Architecture details matter little for fixed parameter count
- Compute-optimal: N ∝ C^0.73, D ∝ C^0.27 (train larger model, fewer tokens)
- Models are typically undertrained — converging wastes compute

## Chinchilla Revision (DeepMind, 2022)
- Revised compute-optimal: 20 tokens per parameter
- Chinchilla 70B (1.4T tokens) outperforms Gopher 280B (300B tokens)
- Shifted the field toward smaller models trained on much more data

## Implications
- Directly informed decision to build GPT-3 at 175B
- Chinchilla laws drove LLaMA, Llama 2/3: smaller models on huge token budgets

## Related Concepts
- [[scaling-laws]]
- [[pre-training-and-fine-tuning]]
- [[in-context-learning]]

## Related Entities
- [[jared-kaplan]]
- [[dario-amodei]]
- [[openai]]
- [[anthropic]]

`Source: raw/scaling-laws-neural-language-models.md`
