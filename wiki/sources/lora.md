# LoRA: Low-Rank Adaptation of Large Language Models

Microsoft's 2021 paper introducing LoRA — efficient fine-tuning by adding small trainable low-rank matrices to frozen pre-trained weights. Enables fine-tuning 175B models with 0.01% of parameters, and is now the dominant production fine-tuning method.

## Key Contributions
- Freezes pre-trained weights W₀; learns ΔW = B×A (low-rank decomposition)
- Rank r controls capacity/efficiency tradeoff (r=4, 8, 16 are common)
- Zero inference overhead — ΔW can be merged back into W₀
- Multiple adapters can be swapped or merged at inference

## Parameter Savings Example
- Full ΔW (4096×4096): 16.7M parameters
- LoRA r=4 (A+B): 32,768 parameters — 512× fewer

## Extensions
- **QLoRA**: 4-bit quantized base model + LoRA — fine-tune 65B on one GPU
- **DoRA**: Decompose weight into magnitude + direction

## Related Concepts
- [[parameter-efficient-fine-tuning]]
- [[pre-training-and-fine-tuning]]

## Related Entities
- [[microsoft-research]]

`Source: raw/lora-low-rank-adaptation.md`
