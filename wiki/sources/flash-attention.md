# FlashAttention: Fast and Memory-Efficient Exact Attention

Stanford's 2022 paper introducing IO-aware attention — restructuring attention computation using tiling to minimize GPU memory reads/writes. 2–4× faster and 5–20× less memory than standard attention, with no approximation. Now the standard implementation in all major LLMs and frameworks.

## Key Contributions
- Tiling: process Q/K/V in blocks that fit in fast SRAM, avoid materializing N×N matrix
- Online softmax: compute incrementally without storing full attention matrix
- Kernel fusion: single GPU kernel for QK^T + softmax + PV
- Recomputation during backward pass instead of storing attention matrix

## Results
- 2–4× speedup on A100 GPU
- Memory: O(N) instead of O(N²)
- Enables 4k, 16k, 100k+ context windows

## Versions
- FlashAttention-2: ~2× faster than v1 (better parallelism)
- FlashAttention-3: H100-optimized with async computation
- Shipped natively in PyTorch (`scaled_dot_product_attention`)

## Related Concepts
- [[self-attention]]
- [[multi-head-attention]]
- [[positional-encoding]]

## Related Entities
- [[tri-dao]]
- [[stanford-university]]

`Source: raw/flash-attention.md`
