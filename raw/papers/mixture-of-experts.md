# Mixture of Experts for Transformers (GShard / Switch Transformers)

**Key Papers**:
- GShard: Scaling Giant Models with Conditional Computation and Automatic Sharding (Lepikhin et al., Google, 2021)
- Switch Transformers: Scaling to Trillion Parameter Models with Simple and Efficient Sparsity (Fedus et al., Google Brain, 2022)

---

## Overview

Mixture of Experts (MoE) is an architecture that replaces the dense feed-forward layers in a Transformer with a set of "expert" sub-networks, activating only a subset for each token. A learned routing function selects which experts process each token. This enables scaling model capacity (number of parameters) without proportionally increasing compute — a 1 trillion parameter MoE model can have the same inference cost as a 100B dense model. MoE is believed to be a key component of GPT-4 and is used in Mixtral, Grok, and other frontier models.

---

## The Core Idea: Sparse Activation

Dense Transformer: every token is processed by every parameter
```
FFN(x) = W₂ · ReLU(W₁ · x)     # all parameters used for every token
```

MoE Transformer: each token is processed by only k of N experts
```
MoE(x) = Σᵢ G(x)ᵢ · Eᵢ(x)     # only top-k experts activated
```

Where:
- Eᵢ is the i-th expert (a separate feed-forward network)
- G(x) is the gating/routing function that selects which experts to use
- Only k experts (k=1 or k=2) are activated per token

**Result**: Parameters ↑ N×, compute stays roughly constant.

---

## The Gating / Routing Mechanism

A learned linear layer produces a score for each expert, then top-k experts are selected:

```
scores = softmax(W_gate · x)
top_k_indices = argtopk(scores, k)
output = Σ scores[i] * Expert_i(x) for i in top_k_indices
```

**Switch Transformer** uses k=1 (Top-1 routing) — each token goes to exactly one expert. Simpler and more efficient than k=2.

---

## Load Balancing Problem

A naive router tends to route all tokens to the same few experts (routing collapse). Solutions:
- **Auxiliary load balancing loss**: Penalize uneven expert utilization during training
- **Expert capacity**: Each expert processes at most C tokens per batch — overflow tokens are dropped or passed through without routing
- **Random routing**: Add noise to gating scores during training

---

## Switch Transformer Key Results

- Trained a 1.6 trillion parameter model
- Achieves 7x speedup vs T5-XXL (11B dense) at same compute budget
- Demonstrates scaling of sparse models improves with more experts
- Works with up to 2,048 experts

---

## GShard

- Applied MoE to machine translation
- Scaled to 600B parameters across 2,048 TPU cores
- Key contribution: automatic model parallelism — compiler shards model across devices
- Enabled models too large to fit on any single device

---

## Modern MoE Models

- **Mixtral 8x7B** (Mistral AI, 2023): 8 experts, top-2 routing, 46.7B total params, 12.9B active — outperforms LLaMA 2 70B
- **Mixtral 8x22B** (Mistral AI, 2024): 141B total, 39B active parameters
- **GPT-4**: Rumored to use MoE architecture (not officially confirmed)
- **Grok-1** (xAI, 2024): 314B parameters, MoE architecture, open-sourced
- **DeepSeek-V2** (2024): 236B total, 21B active — efficient MoE

---

## MoE vs Dense Models

| Property | Dense | MoE |
|----------|-------|-----|
| Parameters | N | k*N (much larger) |
| Compute per token | O(N) | O(k) |
| Memory | N | k*N (all experts must be loaded) |
| Training stability | High | Lower (routing instability) |
| Inference latency | Predictable | Can vary |
| Communication overhead | Low | High (distributed experts) |

---

## Key Terms

- **Expert**: A sub-network (usually a feed-forward network) within an MoE layer
- **Gating network**: The routing function that selects which experts process each token
- **Top-k routing**: Selecting k experts per token (k=1 or k=2 most common)
- **Sparse activation**: Only a fraction of parameters are active for any given input
- **Load balancing**: Ensuring all experts receive roughly equal amounts of tokens
- **Expert capacity**: Maximum tokens an expert can process in one batch

---

## Citation

Fedus, W., Zoph, B., & Shazeer, N. (2022). Switch transformers: Scaling to trillion parameter models with simple and efficient sparsity. *Journal of Machine Learning Research*, 23(1), 5232–5270.

Lepikhin, D., et al. (2021). GShard: Scaling giant models with conditional computation and automatic sharding. *ICLR 2021*.
