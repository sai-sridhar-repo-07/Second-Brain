# Generative Models

Generative models learn to produce new samples that resemble a training distribution — generating images, text, audio, video, or other data. The main families are autoregressive models (LLMs), diffusion models, and GANs, each with different tradeoffs.

## How Sources Explain This
- **[[gan]]**: Two-network adversarial game. Fast inference (single forward pass), but mode collapse and training instability. Dominated image generation 2014–2021.
- **[[diffusion-models]]**: Learn to reverse a gradual noising process. Stable training, high diversity, supports text conditioning. Now dominant for image generation. Slow inference (1000 steps, addressed by DDIM/latent diffusion).
- **[[gpt3]]**: Autoregressive text generation — each token predicted from all prior tokens. Decoder-only Transformer. Most capable text generators use this paradigm.

## Contradictions or Variations
- GANs (fast, unstable, low diversity) vs Diffusion (stable, diverse, slow) — trade different things
- Autoregressive models generate token by token — flexible but can't parallelize generation
- Latent diffusion (Stable Diffusion) runs diffusion in compressed latent space — best of both: quality + speed

## Related Concepts
- [[encoder-decoder]]
- [[transformer-architecture]]
- [[rlhf-and-rlaif]]
