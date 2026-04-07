# Diffusion Models: Denoising Diffusion Probabilistic Models (DDPM)

**Authors**: Jonathan Ho, Ajay Jain, Pieter Abbeel
**Institution**: UC Berkeley
**Published**: 2020 (NeurIPS 2020)

---

## Overview

DDPM introduced denoising diffusion probabilistic models — a class of generative models that learn to reverse a gradual noising process. The core idea: gradually add Gaussian noise to an image until it's pure noise, then train a neural network to reverse this process step by step. At inference, start from pure noise and denoise iteratively to generate a new image. DDPM became the foundation of all modern image generation systems including Stable Diffusion, DALL-E 2, Midjourney, and Imagen.

---

## The Core Idea

### Forward Process (Noising)
Gradually add noise to a real image over T timesteps:
```
x_0 (real image) → x_1 → x_2 → ... → x_T (pure Gaussian noise)
```

Each step adds a small amount of Gaussian noise according to a fixed variance schedule β_t:
```
q(x_t | x_{t-1}) = N(x_t; sqrt(1-β_t) * x_{t-1}, β_t * I)
```

**Key property**: The forward process has a closed-form solution — you can jump directly from x_0 to any x_t:
```
q(x_t | x_0) = N(x_t; sqrt(ᾱ_t) * x_0, (1 - ᾱ_t) * I)
```
where ᾱ_t is the product of (1 - β_i) for all timesteps up to t.

### Reverse Process (Denoising)
Learn a neural network p_θ to reverse the noising:
```
x_T (noise) → x_{T-1} → ... → x_1 → x_0 (generated image)
```

The network predicts the noise that was added at each step, then subtracts it.

---

## Training Objective

Train a U-Net to predict the noise ε added to a clean image at timestep t:

```
L = E_{t, x_0, ε} [ ||ε - ε_θ(x_t, t)||² ]
```

Simple mean squared error between actual noise and predicted noise. The simplification from the variational lower bound to this noise-prediction objective was a key finding — it improved sample quality.

---

## Architecture: U-Net

The denoising network uses a **U-Net** — an encoder-decoder with skip connections:
- Encoder: downsamples image, extracts features at multiple scales
- Decoder: upsamples, uses skip connections from encoder
- Timestep embedding: sinusoidal embedding of t, injected into each layer
- Later versions add attention layers at lower resolutions

---

## Inference

1. Sample x_T ~ N(0, I) (pure Gaussian noise)
2. For t = T, T-1, ..., 1:
   - Predict noise: ε_θ(x_t, t)
   - Compute x_{t-1} using reverse process formula
3. Return x_0

**Problem**: T = 1,000 steps required → slow inference (seconds per image on GPU)

---

## Results

- **FID score on CIFAR-10**: 3.17 (competitive with GANs)
- **FID on 256×256 LSUN Bedroom**: 4.90 (better than progressive GAN)
- Unconditional image generation quality competitive with GANs for the first time
- More diverse samples than GANs (GANs suffer from mode collapse)

---

## Why DDPM Beats GANs

GANs (Generative Adversarial Networks) were the dominant generative model before diffusion:

| Property | GANs | Diffusion |
|----------|------|-----------|
| Training stability | Unstable (mode collapse, training collapse) | Stable (simple MSE loss) |
| Sample diversity | Low (mode collapse) | High |
| Sample quality | High (sharp) | High |
| Inference speed | Fast (single forward pass) | Slow (1000 steps) |
| Likelihood | Not directly available | Available (approximate) |
| Controllability | Difficult | Good (via guidance) |

Diffusion's stable training and high diversity made it more practical for production systems.

---

## Successors and Extensions

- **DDIM** (Song et al., 2020): Deterministic sampling in 10-50 steps instead of 1000 — huge speedup
- **Improved DDPM** (Nichol & Dhariwal, 2021): Learned noise schedules, better FID
- **Classifier Guidance** (Dhariwal & Nichol, 2021): Condition generation on class labels using a classifier
- **Classifier-Free Guidance** (Ho & Salimans, 2021): Conditioning without a separate classifier — backbone of all modern text-to-image
- **Latent Diffusion Models / Stable Diffusion** (Rombach et al., 2022): Run diffusion in latent space of a VAE — much cheaper
- **DALL-E 2** (OpenAI, 2022): CLIP + diffusion for text-to-image
- **Imagen** (Google, 2022): Cascaded diffusion models for photorealistic text-to-image
- **Sora** (OpenAI, 2024): Diffusion applied to video via transformer backbone (DiT)

---

## Key Terms

- **Forward process**: Gradually adding noise to data over T timesteps
- **Reverse process**: Neural network learning to denoise step by step
- **Score function**: Gradient of log probability — what the network implicitly learns
- **Variance schedule**: β_t controls how much noise is added at each step
- **FID (Fréchet Inception Distance)**: Metric for generative model quality — lower is better
- **Mode collapse**: GAN failure where generator produces limited variety
- **U-Net**: Encoder-decoder architecture with skip connections used as the denoising network
- **Classifier-free guidance**: Technique to steer generation toward a condition without a separate classifier

---

## Authors

- **Jonathan Ho** — UC Berkeley PhD student; lead author; later joined Google Brain
- **Ajay Jain** — UC Berkeley PhD student; co-author
- **Pieter Abbeel** — Professor, UC Berkeley; robotics and RL researcher

---

## Citation

Ho, J., Jain, A., & Abbeel, P. (2020). Denoising diffusion probabilistic models. *Advances in Neural Information Processing Systems*, 33, 6840–6851.
