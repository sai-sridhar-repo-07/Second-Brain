# GAN: Generative Adversarial Networks

Université de Montréal's 2014 paper introducing GANs — a two-player game between Generator (creates fake data) and Discriminator (classifies real vs fake). Dominated image generation 2014–2021 before being superseded by diffusion models.

## Key Contributions
- Minimax game: G minimizes log(1 - D(G(z))), D maximizes log D(x) + log(1 - D(G(z)))
- No explicit likelihood required — implicit generative model
- Nash equilibrium: G produces true data distribution, D outputs 0.5 everywhere
- Demonstrated photorealistic synthesis at scale (StyleGAN, BigGAN)

## Key Problems
- Mode collapse: generator produces limited variety
- Training instability: loss doesn't reliably indicate quality
- No likelihood: can't detect out-of-distribution inputs

## Status (2024)
- Largely replaced by diffusion models for high-quality generation
- Still used for real-time applications (single forward pass inference)

## Related Concepts
- [[generative-models]]
- [[adversarial-training]]

## Related Entities
- [[ian-goodfellow]]
- [[yoshua-bengio]]

`Source: raw/gan-generative-adversarial-networks.md`
