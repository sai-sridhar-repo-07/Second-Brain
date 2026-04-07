# Vision Transformer (ViT): An Image is Worth 16x16 Words

**Authors**: Alexey Dosovitskiy, Lucas Beyer, Alexander Kolesnikov, Dirk Weissenborn, Xiaohua Zhai, Thomas Unterthiner, Mostafa Dehghani, Matthias Minderer, Georg Heigold, Sylvain Gelly, Jakob Uszkoreit, Neil Houlsby
**Institution**: Google Research / Brain Team
**Published**: 2020 (ICLR 2021)

---

## Overview

Vision Transformer (ViT) applies the Transformer architecture directly to images by splitting an image into fixed-size patches, treating each patch as a "token", and processing them with standard Transformer self-attention. ViT showed that a pure Transformer, with no convolutional inductive biases, can match or exceed CNNs on image classification when trained on sufficient data. It triggered a paradigm shift in computer vision from CNNs to Transformers and enabled multimodal models (vision + language).

---

## The Core Idea: Images as Sequences of Patches

Before ViT, applying attention to images was expensive — N×M pixels = N×M tokens with O(N²M²) attention.

ViT's solution: treat images as sequences of **patches**:
1. Split 224×224 image into 16×16 patches → 196 patches
2. Linearly embed each patch → 768-dimensional vector
3. Add a learnable [CLS] token (like BERT) for classification
4. Add positional embeddings
5. Feed sequence of 197 tokens through standard Transformer encoder
6. Use [CLS] token representation for classification

```
Image (224×224×3) → 196 patches (16×16×3)
→ Linear projection → 196 × 768 embeddings
→ + [CLS] token + position embeddings
→ Transformer Encoder (12 layers)
→ [CLS] representation → MLP head → class probabilities
```

---

## Key Finding: Data Is Everything

ViT has fewer image-specific inductive biases than CNNs (no translation equivariance, no locality). This is a disadvantage on small datasets but an advantage at scale:

| Dataset | ResNet-50 | ViT-L/16 |
|---------|-----------|---------|
| ImageNet only | ~76% | ~76% (similar) |
| ImageNet-21k pretrain | ~83% | ~86% |
| JFT-300M pretrain | ~85% | ~88% |

**With enough data, ViT outperforms CNNs.** Without enough data, CNNs win.

The threshold: ~14M images minimum; JFT-300M (Google's internal dataset of 300M images) is where ViT clearly wins.

---

## Why ViT Matters for Modern AI

### Unified Architecture
Before ViT, vision and language used different architectures (CNNs vs Transformers). ViT enabled:
- **CLIP** (Radford et al., OpenAI, 2021): Vision Transformer + text Transformer trained together on image-text pairs
- **DALL-E** (OpenAI, 2021): ViT-based image tokenizer + language model
- **Flamingo** (DeepMind, 2022): Interleaved vision and language Transformers
- **GPT-4V, Claude 3**: Vision + language in a single Transformer

### Scaling Behavior
ViT scales better than CNNs with more data and compute — consistent with language model scaling laws. Larger ViT models + more data always help.

---

## ViT Variants

| Model | Patches | Params | ImageNet Top-1 |
|-------|---------|--------|----------------|
| ViT-S/16 | 16×16 | 22M | 81.4% |
| ViT-B/16 | 16×16 | 86M | 84.2% |
| ViT-L/16 | 16×16 | 307M | 86.5% |
| ViT-H/14 | 14×14 | 632M | 88.5% |

Naming: ViT-B/16 = Base model, 16×16 patches

---

## Successors

- **DeiT** (Facebook, 2021): ViT trained efficiently on ImageNet alone (knowledge distillation)
- **Swin Transformer** (Microsoft, 2021): Hierarchical ViT with shifted window attention — scales to detection/segmentation
- **MAE** (He et al., Meta/Facebook, 2021): Masked Autoencoder — self-supervised ViT pretraining (analogous to BERT's MLM)
- **CLIP**: ViT + contrastive learning on image-text pairs
- **SAM** (Meta, 2023): Segment Anything Model — ViT-based foundation model for image segmentation

---

## Attention in Vision

A key finding: ViT attention heads learn to attend to semantically meaningful image regions:
- Some heads focus on local texture
- Some heads attend to long-range semantic relationships (distant parts of the same object)
- Attention maps visualize what the model "looks at"

This interpretability advantage over CNNs has driven research into attention-based vision models.

---

## Key Terms

- **Image patch**: Fixed-size (e.g., 16×16 pixel) region of an image treated as a token
- **Patch embedding**: Linear projection of a flattened patch to a vector
- **[CLS] token**: Classification token prepended to the sequence, used for final prediction
- **Inductive bias**: Prior assumptions built into an architecture (e.g., CNNs assume local correlations)
- **CLIP**: Contrastive Language-Image Pretraining — connects image and text representations
- **Masked Autoencoder (MAE)**: Self-supervised ViT pretraining via masked patch prediction

---

## Authors

- **Alexey Dosovitskiy** — Google Brain; lead author
- **Jakob Uszkoreit** — Google Research; also co-authored "Attention Is All You Need"

---

## Citation

Dosovitskiy, A., Beyer, L., Kolesnikov, A., Weissenborn, D., Zhai, X., Unterthiner, T., ... & Houlsby, N. (2020). An image is worth 16x16 words: Transformers for image recognition at scale. *arXiv preprint arXiv:2010.11929*.
