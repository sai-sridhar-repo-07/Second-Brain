# FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness

**Authors**: Tri Dao, Dan Fu, Stefano Ermon, Atri Rudra, Christopher Ré
**Institution**: Stanford University
**Published**: 2022 (NeurIPS 2022)

---

## Overview

FlashAttention is an IO-aware implementation of exact attention that is 2-4x faster than standard attention while using up to 5-20x less memory, without any approximation. The key insight: the bottleneck in attention is not floating-point operations (FLOPs) but memory bandwidth — repeatedly reading/writing large matrices to GPU HBM (high-bandwidth memory). By restructuring the computation to minimize memory reads/writes using tiling, FlashAttention achieves dramatic speedups. It enables longer context windows and is now the standard implementation used in all modern LLMs.

---

## The Problem: Standard Attention Is Memory-Bound

Standard attention computes:
```
S = QK^T       # [N×N] matrix — O(N²) memory
P = softmax(S) # [N×N] matrix — must be materialized
O = PV         # [N×d] output
```

For N=2048 tokens and d=64:
- S matrix: 2048 × 2048 × 4 bytes = 16MB per head per layer
- With 96 heads and 96 layers: ~150GB of intermediates just for S matrices
- These matrices must be written to GPU HBM and read back — slow

**The actual bottleneck is not computation (FLOPs) but memory bandwidth (IO)**. GPUs can compute much faster than they can move data to/from HBM.

---

## The Solution: Tiling + Kernel Fusion

FlashAttention avoids materializing the full N×N attention matrix by:

1. **Tiling**: Split Q, K, V into blocks that fit in fast SRAM (on-chip cache)
2. **Online softmax**: Compute softmax incrementally using running max and normalization — no need to store full row
3. **Kernel fusion**: Fuse the QK^T, softmax, and PV operations into a single GPU kernel

```
For each block of Q:
  For each block of K, V:
    Load block to SRAM
    Compute partial attention scores
    Update running softmax statistics
    Accumulate partial output
  Write final output block to HBM
```

**Result**: HBM reads = O(N²/B) instead of O(N²), where B is block size.

---

## Memory Complexity Improvement

| Method | Memory | HBM reads |
|--------|--------|-----------|
| Standard attention | O(N²) | O(N²) |
| FlashAttention | O(N) | O(N²/B) |
| FlashAttention-2 | O(N) | ~2x faster than v1 |

The N×N matrix is never fully materialized in HBM — it exists only in SRAM tiles.

---

## Backward Pass

Computing gradients requires the attention matrix. FlashAttention recomputes it from Q, K, V during the backward pass (recomputation) rather than storing it. This trades extra FLOPs for much lower memory.

---

## Results

- **2-4x speedup** vs PyTorch standard attention on A100 GPU
- **5-20x less memory** for the attention computation
- **Exact output**: No approximation — numerically identical to standard attention
- Enables training GPT-2 (1.3B) on 4k context (vs 1k) with same memory
- Enables longer context windows: 16k, 32k, 128k contexts become practical

---

## FlashAttention-2 (2023)

Tri Dao's follow-up with additional optimizations:
- Better parallelism across attention heads
- Reduced non-matrix multiply operations
- ~2x faster than FlashAttention v1
- Now standard implementation in PyTorch, HuggingFace, and all major frameworks

## FlashAttention-3 (2024)

Further optimizations for H100 GPU architecture using async computation.

---

## Impact on Context Length

Before FlashAttention, long contexts were impractical:
- Memory grows quadratically with context: 4k → 16k = 16x more memory
- FlashAttention linearizes memory, making 100k+ context windows practical
- Enabled: Claude 100k context, GPT-4 128k context, Gemini 1M context

---

## Broader Impact

- Now shipped in PyTorch (`torch.nn.functional.scaled_dot_product_attention`)
- Default in HuggingFace Transformers
- Used by every major LLM: GPT-4, Claude, LLaMA, Mistral, Gemini
- Tri Dao became one of the most cited ML engineers for enabling practical LLM scaling

---

## Key Terms

- **IO-aware algorithm**: Optimization that accounts for memory hierarchy (SRAM vs HBM)
- **HBM**: High Bandwidth Memory — main GPU memory, fast but slow vs SRAM
- **SRAM**: On-chip cache — tiny but extremely fast (10-100x bandwidth vs HBM)
- **Tiling**: Splitting computation into blocks that fit in fast memory
- **Kernel fusion**: Combining multiple GPU operations into a single pass
- **Online softmax**: Computing softmax without materializing the full matrix
- **Recomputation**: Recomputing intermediate values during backward pass to save memory

---

## Authors

- **Tri Dao** — Stanford PhD student; lead author; later created FlashAttention-2/3; now at Together AI / Princeton
- **Christopher Ré** — Stanford Professor; advisor; also known for Snorkel (weak supervision)

---

## Citation

Dao, T., Fu, D., Ermon, S., Rudra, A., & Ré, C. (2022). FlashAttention: Fast and memory-efficient exact attention with IO-awareness. *Advances in Neural Information Processing Systems*, 35.
