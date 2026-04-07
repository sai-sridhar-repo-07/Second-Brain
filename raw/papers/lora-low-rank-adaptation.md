# LoRA: Low-Rank Adaptation of Large Language Models

**Authors**: Edward J. Hu, Yelong Shen, Phillip Wallis, Zeyuan Allen-Zhu, Yuanzhi Li, Shean Wang, Lu Wang, Weizhu Chen
**Institution**: Microsoft
**Published**: 2021 (ICLR 2022)

---

## Overview

LoRA (Low-Rank Adaptation) enables efficient fine-tuning of large language models by adding small trainable low-rank matrices to frozen pre-trained weights, rather than updating all parameters. Instead of fine-tuning a 175B parameter model (expensive), LoRA adds tiny trainable adapters — often just 0.01% of the original parameters — achieving comparable performance. LoRA is now the dominant method for fine-tuning LLMs in production.

---

## The Problem: Full Fine-Tuning Is Expensive

Fine-tuning a 175B parameter GPT-3 requires:
- Storing 175B parameter gradients
- Optimizer states (Adam stores 2x gradients = 350B more values)
- Updated copy of all weights
- Total: ~1TB of GPU memory for a single training run

This is prohibitive for most organizations. Even inference of fine-tuned models requires storing separate copies per task.

---

## The Core Idea: Low-Rank Decomposition

The hypothesis: weight updates during fine-tuning have **low intrinsic rank** — they lie in a much lower-dimensional subspace than the full weight matrix.

For a pre-trained weight matrix W₀ ∈ ℝ^(d×k), instead of learning a full update ΔW ∈ ℝ^(d×k), learn:

```
ΔW = B × A
where B ∈ ℝ^(d×r), A ∈ ℝ^(r×k), rank r << min(d,k)
```

The forward pass becomes:
```
h = W₀x + ΔWx = W₀x + BAx
```

- W₀ is frozen — never updated
- A is initialized with random Gaussian
- B is initialized to zero (so ΔW = 0 at start, preserving original behavior)
- Only A and B are trained

### Parameter Savings
For d=k=4096 and r=4:
- Full ΔW: 4096 × 4096 = 16.7M parameters
- LoRA (A+B): 4096×4 + 4×4096 = 32,768 parameters
- **Reduction: 512x fewer parameters**

---

## Where to Apply LoRA

Applied to attention weight matrices (Q, K, V, O projections):
- The paper finds applying to Q and V attention matrices is most effective
- Can also apply to feed-forward layers (less common)
- Scaling factor α/r controls contribution magnitude (typically α = r or α = 2r)

---

## Results

Tested on GPT-3 (175B) and RoBERTa fine-tuning:
- **WikiSQL**: LoRA matches full fine-tuning with 10,000x fewer trainable parameters
- **MultiNLI**: Comparable to full fine-tuning
- **E2E NLG**: Comparable performance with 0.3% of parameters
- Memory reduction: ~3x for training, enabling fine-tuning on consumer GPUs

---

## Why LoRA Is Used Everywhere

1. **Single GPU fine-tuning**: A 7B model can be LoRA fine-tuned on a 24GB consumer GPU
2. **Mergeable**: After training, ΔW = BA can be added to W₀ — zero inference overhead
3. **Swappable**: Multiple LoRA adapters can be swapped at inference (different tasks, same base model)
4. **Composable**: Multiple LoRAs can be merged or mixed
5. **Open source tooling**: HuggingFace PEFT library makes LoRA trivial to apply

---

## Variants and Extensions

- **QLoRA** (Dettmers et al., 2023): Quantize base model to 4-bit, apply LoRA in 16-bit — enables 65B model fine-tuning on a single 48GB GPU
- **LoftQ**: Better initialization for quantized LoRA
- **DoRA**: Decomposes weight into magnitude + direction, applies LoRA to direction
- **LoRA+**: Different learning rates for A and B matrices
- **AdaLoRA**: Adaptive rank allocation — more rank budget to important layers

---

## Practical Usage

```python
# Using HuggingFace PEFT
from peft import LoraConfig, get_peft_model

config = LoraConfig(
    r=16,              # rank
    lora_alpha=32,     # scaling factor
    target_modules=["q_proj", "v_proj"],
    lora_dropout=0.1,
)
model = get_peft_model(base_model, config)
# Only 0.1% of parameters are trainable
```

---

## Key Terms

- **Rank r**: Dimensionality of the low-rank decomposition — controls capacity/efficiency tradeoff
- **LoRA alpha (α)**: Scaling factor for the LoRA update: final update = (α/r) * BAx
- **PEFT**: Parameter-Efficient Fine-Tuning — umbrella term; LoRA is one method
- **Adapter**: Generic term for small trainable modules added to frozen models
- **QLoRA**: LoRA applied to quantized base model — 4-bit base + 16-bit adapters
- **Intrinsic rank**: The true dimensionality of the task-relevant weight update subspace

---

## Authors

- **Edward J. Hu** — Microsoft; lead author
- **Weizhu Chen** — Microsoft Research; senior author

---

## Citation

Hu, E. J., Shen, Y., Wallis, P., Allen-Zhu, Z., Li, Y., Wang, S., Wang, L., & Chen, W. (2021). LoRA: Low-rank adaptation of large language models. *arXiv preprint arXiv:2106.09685*.
