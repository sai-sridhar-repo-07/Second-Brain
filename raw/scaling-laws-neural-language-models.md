# Scaling Laws for Neural Language Models

**Authors**: Jared Kaplan, Sam McCandlish, Tom Henighan, Tom B. Brown, Benjamin Chess, Ramesh Ganesh, Sam Gray, Alec Radford, Jeffrey Wu, Dario Amodei
**Institution**: OpenAI
**Published**: 2020 (arXiv preprint)

---

## Overview

This paper established quantitative scaling laws governing how language model performance improves as a function of model size (N parameters), dataset size (D tokens), and compute budget (C FLOPs). The key finding: language model loss follows precise power laws with respect to each of these variables, independently of architecture details. These laws allow predicting performance before training and guide decisions about how to allocate a compute budget. Scaling laws are the scientific foundation for the "bigger is better" era of LLMs.

---

## The Core Finding: Power Laws

Language model cross-entropy loss L scales as smooth power laws with respect to:

```
L(N) ∝ N^(-0.076)        # parameters (dataset not limiting)
L(D) ∝ D^(-0.095)        # dataset size (model not limiting)
L(C) ∝ C^(-0.050)        # compute budget
```

These relationships hold across many orders of magnitude — from millions to hundreds of billions of parameters. The loss-vs-parameter curves are remarkably smooth and predictable.

---

## The Compute-Optimal Frontier

For a fixed compute budget C, there's an optimal allocation between model size N and training tokens D:

```
N_optimal ∝ C^0.73       # model size scales as 0.73 power of compute
D_optimal ∝ C^0.27       # tokens scale as 0.27 power of compute
```

**Key implication**: Given a compute budget, it's better to train a larger model on fewer tokens than a smaller model on more tokens (up to a point). This drove the trend of training ever-larger models.

---

## What Doesn't Matter Much

Surprisingly robust findings:
- **Architecture details**: Transformer depth vs width matters little for fixed parameter count
- **Optimizer**: Adam vs others — similar final loss
- **Batch size**: Flexible within a range — critical insight for large-scale training

The dominant factors are N, D, and C — not architecture tuning.

---

## Convergence Is Wasteful

A key practical finding: models are typically undertrained relative to their optimal token count. Training a model to convergence (until loss stops improving) wastes compute — you should stop earlier and train a larger model instead.

---

## Chinchilla Scaling Laws (Hoffmann et al., DeepMind, 2022)

The original Kaplan et al. scaling laws led to the "underfitting hypothesis" — train larger models on less data. DeepMind's Chinchilla paper revised this:

```
Chinchilla finding: Optimal tokens D ≈ 20 × N  (parameters)
```

To train optimally: for every parameter, you need ~20 training tokens.

| Model | Parameters | Training Tokens | Tokens/Param |
|-------|------------|-----------------|--------------|
| GPT-3 | 175B | 300B | 1.7 |
| Chinchilla | 70B | 1.4T | 20 |

Chinchilla (70B) outperforms Gopher (280B) — 4x fewer parameters, trained on 4x more data. This revised the field toward training smaller models on more data.

---

## Impact on LLM Development

Scaling laws changed how AI labs think about model development:

1. **Before scaling laws**: Train a model, evaluate, guess at next steps
2. **After scaling laws**: Predict final loss before training, optimize compute allocation
3. **Drove GPT-3**: Kaplan's laws directly informed the decision to build a 175B model
4. **Drove LLaMA**: Meta trained smaller models on more tokens (following Chinchilla)
5. **Drove Llama 2/3**: 70B model on 2T tokens — better than 175B on 300B tokens

---

## Emergent Abilities and Scaling

A related finding (Wei et al., 2022): some capabilities appear discontinuously at scale — present at 100B+ parameters, absent at 10B. These "emergent abilities" include:
- Chain-of-thought reasoning
- Multi-step arithmetic
- Instruction following

This raised debates about whether scaling alone leads to qualitatively new capabilities.

---

## Practical Rules of Thumb

From Chinchilla scaling laws:
- **Token budget = 20× parameter count** for compute-optimal training
- **7B model**: Train on ~140B tokens (Llama uses 1T+ — inference-optimal, not compute-optimal)
- **70B model**: Train on ~1.4T tokens
- For inference-optimized models (deployed many times): train smaller models on more data than compute-optimal

---

## Key Terms

- **Power law**: Relationship L ∝ x^α where α is the scaling exponent
- **Cross-entropy loss**: Standard language model training objective (predicting next token)
- **Compute budget (C)**: Total FLOPs for training (N × D × ~6 FLOPs/parameter/token)
- **Compute-optimal**: Allocation of N and D that minimizes loss for a given C
- **Chinchilla**: DeepMind's revision of scaling laws; recommended 20 tokens per parameter
- **Emergent abilities**: Capabilities that appear at large scale, absent at small scale

---

## Authors

- **Jared Kaplan** — OpenAI; lead author; also co-authored GPT-3; later co-founded Anthropic
- **Dario Amodei** — OpenAI VP Research during this work; later co-founded Anthropic (CEO)
- **Sam McCandlish** — OpenAI; co-author; later joined Anthropic

---

## Citation

Kaplan, J., McCandlish, S., Henighan, T., Brown, T. B., Chess, B., Child, R., ... & Amodei, D. (2020). Scaling laws for neural language models. *arXiv preprint arXiv:2001.08361*.
