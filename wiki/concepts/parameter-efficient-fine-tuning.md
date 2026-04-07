# Parameter-Efficient Fine-Tuning (PEFT)

PEFT methods adapt large pre-trained models to specific tasks by training only a small fraction of parameters, rather than updating all weights. They make fine-tuning of billion-parameter models practical on limited hardware.

## How Sources Explain This
- **[[lora]]**: Most widely used PEFT method. Adds trainable low-rank matrices B×A (where rank r << d) to frozen pre-trained weights. Achieves comparable performance to full fine-tuning with 0.01% of parameters. Post-training, ΔW = BA is merged back — zero inference overhead.

## Methods Comparison

| Method | Approach | Inference overhead | Notes |
|--------|----------|--------------------|-------|
| LoRA | Low-rank weight update | None (can merge) | Most popular |
| Prefix tuning | Trainable prompt prepended | Slight | Good for generation |
| Prompt tuning | Soft prompt tokens | Slight | Simplest |
| Adapter | Small modules inside layers | Yes | Earlier approach |
| QLoRA | LoRA on 4-bit quantized base | None | GPU memory champion |

## Contradictions or Variations
- LoRA rank selection: higher rank = more capacity but more parameters. r=4–16 covers most cases
- Full fine-tuning still wins on tasks with very large fine-tuning datasets
- QLoRA enables fine-tuning 65B models on a single consumer GPU — game changer for practitioners

## Related Concepts
- [[pre-training-and-fine-tuning]]
- [[scaling-laws]]
