# ResNet: Deep Residual Learning for Image Recognition

**Authors**: Kaiming He, Xiangyu Zhang, Shaoqing Ren, Jian Sun
**Institution**: Microsoft Research
**Published**: 2015 (CVPR 2016, Best Paper Award)

---

## Overview

ResNet introduced **residual connections** (skip connections) — a simple architectural change that enabled training of extremely deep neural networks (100+ layers, later 1000+ layers). Before ResNet, adding more layers made networks perform worse due to the vanishing gradient problem. ResNet solved this and won the ImageNet 2015 competition by a massive margin. The residual connection idea became one of the most universally adopted techniques in deep learning, used in Transformers, diffusion models, and virtually every modern architecture.

---

## The Problem: Degradation

Theoretically, a deeper network should perform at least as well as a shallower one — the extra layers could simply learn identity mappings. In practice, deeper networks were harder to optimize:

- **Vanishing gradients**: Gradients shrink as they backpropagate through many layers, making early layers learn very slowly
- **Degradation problem**: Training accuracy actually got *worse* with more layers — not just overfitting, but genuine optimization failure

A 56-layer plain network performed worse than a 20-layer plain network on CIFAR-10. This was the problem ResNet set out to solve.

---

## The Solution: Residual Connections

Instead of learning a direct mapping H(x), the network learns the **residual** F(x) = H(x) - x, then adds back the input:

```
output = F(x) + x
```

This is called a **skip connection** or **shortcut connection**. The layer only needs to learn what to *add* to the input, not the full transformation.

### Why This Works
- If a layer is not useful, it can simply learn F(x) = 0, making output = x (identity mapping)
- Gradients can flow directly through the skip connection to earlier layers — no vanishing
- The network can be made very deep without degradation because learning identity is trivial

---

## Architecture

### Building Block (Shallow: ResNet-18, ResNet-34)
```
x → [Conv → BN → ReLU → Conv → BN] → + x → ReLU
```

### Bottleneck Block (Deep: ResNet-50, ResNet-101, ResNet-152)
```
x → [1x1 Conv → BN → ReLU → 3x3 Conv → BN → ReLU → 1x1 Conv → BN] → + x → ReLU
```
The 1×1 convolutions reduce then expand dimensions — allows efficient computation in very deep networks.

### Model Variants
| Model | Layers | Parameters |
|-------|--------|------------|
| ResNet-18 | 18 | 11M |
| ResNet-34 | 34 | 21M |
| ResNet-50 | 50 | 25M |
| ResNet-101 | 101 | 44M |
| ResNet-152 | 152 | 60M |

The paper also tested ResNet-1202 (1,202 layers) — it worked, though performance slightly degraded, suggesting other factors limit very deep models.

---

## Results

- **ImageNet ILSVRC 2015**: 3.57% top-5 error — won by a large margin
- **ImageNet classification**: ResNet-152 achieves 4.49% top-5 error vs VGG's 7.3%
- **COCO object detection**: 28% relative improvement
- **COCO segmentation**: 28.5% relative improvement
- **CIFAR-10**: 6.43% error with 110-layer ResNet

---

## Why ResNet Matters Beyond Image Recognition

The residual connection is a **universal principle**, not just a vision trick:

- **Transformers**: The `LayerNorm(x + sublayer(x))` pattern in every Transformer layer is a residual connection
- **Diffusion models**: U-Net architectures with skip connections (a form of residual)
- **Dense prediction**: Feature Pyramid Networks, U-Net use skip connections for multi-scale features
- **Highway networks**: Earlier work in same direction (Srivastava et al., 2015) — ResNet simplified and scaled it

---

## Key Concepts Introduced

- **Residual learning**: Learning the difference (residual) from input, not the full mapping
- **Skip/shortcut connections**: Direct path from input to output bypassing intermediate layers
- **Bottleneck design**: Using 1×1 convolutions to reduce computation in deep layers
- **Batch normalization integration**: Used extensively in ResNet blocks (from Ioffe & Szegedy, 2015)

---

## Influence on Later Work

- **ResNeXt** (Xie et al., 2017): Grouped convolutions + residual connections
- **DenseNet** (Huang et al., 2017): Dense connections — each layer connects to all subsequent layers
- **Wide ResNet**: Wider rather than deeper — comparable performance with fewer layers
- **EfficientNet**: Compound scaling of depth/width/resolution
- **Vision Transformer (ViT)**: Uses residual connections in every block
- **All modern LLMs**: Every Transformer layer uses residual connections — directly from ResNet's influence

---

## Key Terms

- **Residual connection**: Adding input x to the output of a layer: output = F(x) + x
- **Skip connection**: Synonymous with residual connection — the shortcut path
- **Bottleneck**: Using 1×1 convolutions to reduce/expand channels around a 3×3 conv
- **Degradation problem**: Deeper networks performing worse than shallower ones (solved by ResNet)
- **Identity mapping**: Output equals input — what skip connections default to when layer learns zero

---

## Authors

- **Kaiming He** — Microsoft Research; also invented PReLU initialization (He initialization)
- **Xiangyu Zhang** — Microsoft Research
- **Shaoqing Ren** — Microsoft Research; also co-invented Faster R-CNN
- **Jian Sun** — Microsoft Research

---

## Citation

He, K., Zhang, X., Ren, S., & Sun, J. (2016). Deep residual learning for image recognition. *Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition*, 770–778.
