# GAN: Generative Adversarial Networks

**Authors**: Ian J. Goodfellow, Jean Pouget-Abadie, Mehdi Mirza, Bing Xu, David Warde-Farley, Sherjil Ozair, Aaron Courville, Yoshua Bengio
**Institution**: Université de Montréal
**Published**: 2014 (NeurIPS 2014)

---

## Overview

GANs introduced a framework for training generative models using a two-player game: a Generator that creates fake data and a Discriminator that distinguishes real from fake. The two networks train against each other — the generator improves by fooling the discriminator, the discriminator improves by catching fakes. At convergence, the generator produces samples indistinguishable from real data. GANs dominated image generation from 2014-2021 before being largely superseded by diffusion models.

---

## The Core Idea: Adversarial Training

Two networks play a minimax game:

**Generator G**: Takes random noise z → produces fake sample G(z)
**Discriminator D**: Takes a sample x → outputs probability it is real (vs. generated)

The training objective:
```
min_G max_D V(D,G) = E[log D(x)] + E[log(1 - D(G(z)))]
```

- D wants to maximize: correctly label real samples as real (D(x) → 1) and fake as fake (D(G(z)) → 0)
- G wants to minimize: fool D into thinking G(z) is real (D(G(z)) → 1)

At Nash equilibrium: G produces samples from the true data distribution, D outputs 0.5 for everything (can't distinguish real from fake).

---

## Training Process

1. Sample real data x from dataset
2. Sample noise z from prior distribution (usually N(0,1))
3. Generate fake data: x̃ = G(z)
4. **Train D**: Maximize log D(x) + log(1 - D(G(z)))
5. **Train G**: Minimize log(1 - D(G(z))) [or maximize log D(G(z)) — non-saturating]
6. Repeat alternating D and G updates

---

## Problems with GANs

### Mode Collapse
Generator learns to produce a small variety of outputs that always fool D — ignores most of the data distribution. Common failure: GAN trained on diverse faces only generates a few face types.

### Training Instability
- D can become too strong (G gets no gradient signal) or too weak (G learns nothing useful)
- Loss curves don't reliably indicate training quality
- Requires careful hyperparameter tuning and architecture choices

### No Likelihood
Can't compute probability of a sample — can't use for density estimation or detect out-of-distribution inputs.

### Evaluation Difficulty
FID (Fréchet Inception Distance) and IS (Inception Score) are standard metrics but imperfect.

---

## Major GAN Variants

| Year | Model | Innovation |
|------|-------|------------|
| 2014 | DCGAN | Convolutional architecture, stable training guidelines |
| 2017 | WGAN | Wasserstein distance, more stable training |
| 2018 | StyleGAN | Style-based generator, high-quality face synthesis |
| 2019 | BigGAN | Large-scale class-conditional generation |
| 2020 | StyleGAN2 | Improved artifacts, PPL regularization |
| 2021 | StyleGAN3 | Alias-free generation |

---

## GANs vs Diffusion Models

| Property | GANs | Diffusion |
|----------|------|-----------|
| Training stability | Unstable | Stable |
| Sample quality | High (sharp) | High |
| Sample diversity | Low (mode collapse) | High |
| Inference speed | Fast (single forward) | Slow (many steps) |
| Likelihood | Not available | Available |
| Text conditioning | Difficult | Natural |

By 2022, diffusion models overtook GANs for image generation due to better diversity, stability, and text conditioning. However, GANs remain faster at inference and are used in real-time applications.

---

## Legacy and Current Use

GANs are still used for:
- **Super-resolution**: ESRGAN enhances low-res images
- **Image editing**: Pix2Pix, CycleGAN for style transfer
- **Video generation**: Some video synthesis pipelines
- **Medical imaging**: Data augmentation, anomaly detection
- **Fast inference applications**: Where 1000-step diffusion is too slow

The adversarial training concept also influenced other areas:
- **Adversarial training for robustness**: Training classifiers to be robust to adversarial examples
- **Reward modeling**: RLHF can be seen as adversarial (policy vs reward model)

---

## Key Terms

- **Generator (G)**: Network that maps noise to fake samples
- **Discriminator (D)**: Network that classifies real vs. generated samples
- **Adversarial training**: Training G and D against each other
- **Nash equilibrium**: Game theory concept — stable point where neither player can improve unilaterally
- **Mode collapse**: Generator producing limited variety of outputs
- **FID**: Fréchet Inception Distance — quality metric for generative models (lower = better)

---

## Authors

- **Ian Goodfellow** — Université de Montréal; lead author; later Google Brain, OpenAI, Apple
- **Yoshua Bengio** — Université de Montréal; supervisor; Turing Award winner

---

## Citation

Goodfellow, I., Pouget-Abadie, J., Mirza, M., Xu, B., Warde-Farley, D., Ozair, S., Courville, A., & Bengio, Y. (2014). Generative adversarial nets. *Advances in Neural Information Processing Systems*, 27.
