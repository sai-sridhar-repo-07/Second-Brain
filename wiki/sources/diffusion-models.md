# Diffusion Models: Denoising Diffusion Probabilistic Models (DDPM)

UC Berkeley's 2020 paper introducing diffusion models — generative models that learn to reverse a gradual noising process. Foundation of Stable Diffusion, DALL-E 2, Midjourney, and all modern image generation systems.

## Key Contributions
- Forward process: gradually add Gaussian noise over T=1000 steps
- Reverse process: train U-Net to predict and remove noise step by step
- Simple MSE noise-prediction objective: `L = ||ε - ε_θ(x_t, t)||²`
- Stable training unlike GANs — no mode collapse

## Results
- CIFAR-10 FID: 3.17 (competitive with GANs)
- LSUN Bedroom FID: 4.90 (better than progressive GAN)

## Limitations
- 1000 inference steps — very slow (addressed by DDIM, latent diffusion)
- High compute for training

## Related Concepts
- [[generative-models]]
- [[score-based-models]]

## Related Entities
- [[jonathan-ho]]
- [[uc-berkeley]]

`Source: raw/diffusion-models-ddpm.md`
