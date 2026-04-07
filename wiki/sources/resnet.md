# ResNet: Deep Residual Learning for Image Recognition

Microsoft Research's 2015 paper introducing residual (skip) connections, enabling training of extremely deep networks (100-1000+ layers). Won ImageNet 2015 and the residual connection became a universal building block adopted by Transformers, diffusion models, and all modern architectures.

## Key Contributions
- Residual connection: output = F(x) + x — learns the residual rather than full mapping
- Solved the degradation problem: deeper networks no longer perform worse
- Bottleneck blocks using 1×1 convolutions for efficiency in deep models
- ResNet-50/101/152 — all widely used today

## Results
- ImageNet ILSVRC 2015: 3.57% top-5 error (prior SOTA ~7%)
- COCO detection: 28% relative improvement

## Related Concepts
- [[residual-connections]]
- [[transfer-learning]]

## Related Entities
- [[kaiming-he]]
- [[microsoft-research]]

`Source: raw/resnet-deep-residual-learning.md`
