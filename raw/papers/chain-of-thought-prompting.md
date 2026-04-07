# Chain-of-Thought Prompting Elicits Reasoning in Large Language Models

**Authors**: Jason Wei, Xuezhi Wang, Dale Schuurmans, Maarten Bosma, Brian Ichter, Fei Xia, Ed Chi, Quoc Le, Denny Zhou
**Institution**: Google Research / Google Brain
**Published**: 2022 (NeurIPS 2022)

---

## Overview

Chain-of-Thought (CoT) prompting shows that including step-by-step reasoning examples in the prompt dramatically improves LLM performance on complex reasoning tasks. Rather than prompting a model with just "Question → Answer", chain-of-thought prompts include a reasoning trace: "Question → Reasoning steps → Answer". This simple idea unlocked reasoning capabilities that were previously hidden in large models and became the foundation of modern prompting strategies.

---

## The Core Finding

Standard few-shot prompting:
```
Q: Roger has 5 tennis balls. He buys 2 more cans of 3 balls. How many balls does he have?
A: 11
```

Chain-of-thought prompting:
```
Q: Roger has 5 tennis balls. He buys 2 more cans of 3 balls. How many balls does he have?
A: Roger starts with 5 balls. 2 cans of 3 tennis balls each is 6 tennis balls. 
   5 + 6 = 11. The answer is 11.

Q: [New question]
A: [Model generates reasoning trace, then answer]
```

Including reasoning examples in the prompt causes the model to generate intermediate reasoning steps — and this dramatically improves accuracy on tasks requiring multi-step logic.

---

## Why Chain-of-Thought Works

1. **Decomposition**: Complex problems are broken into manageable sub-steps
2. **Interpretability**: The model "shows its work" — errors are easier to diagnose
3. **Emergent at scale**: Small models can't benefit from CoT; large models (≥100B parameters) can
4. **Computation budget**: More tokens = more "thinking time" — the model allocates compute to intermediate steps

The key insight: language models are **autoregressive** — each generated token can be conditioned on all prior tokens. CoT forces the model to write out intermediate results, making them available as context for subsequent reasoning steps.

---

## Scale Dependency

Critical finding: CoT prompting only helps at scale:
- **GPT-3 (175B)**: Large improvement on math/reasoning with CoT
- **GPT-3 (13B)**: Marginal improvement
- **GPT-3 (1B)**: No improvement or slightly worse

This reveals an **emergent capability** — the ability to follow and produce reasoning chains is not present in smaller models and appears suddenly at ~100B parameters.

---

## Task Performance

| Task | Standard Prompting | Chain-of-Thought |
|------|--------------------|------------------|
| GSM8K (grade school math) | ~18% | ~58% (GPT-3) |
| SVAMP (arithmetic) | ~69% | ~89% |
| MultiArith | ~33% | ~93% |
| CommonsenseQA | ~73% | ~80% |

---

## Variants

### Zero-Shot CoT (Kojima et al., 2022)
Simply appending "Let's think step by step" to a question triggers chain-of-thought reasoning without any examples:
```
Q: [Question]. Let's think step by step.
A: [Model generates reasoning then answer]
```
Surprisingly effective — showed the reasoning ability was latent in the model.

### Least-to-Most Prompting
Decompose a problem into sub-problems, solve easiest first, use those solutions to solve harder ones.

### Self-Consistency (Wang et al., 2022)
Generate multiple CoT reasoning paths, take majority vote on final answer. Dramatically improves accuracy.

### Tree of Thoughts (Yao et al., 2023)
Explore multiple reasoning branches like a search tree, backtrack from dead ends.

### ReAct (Yao et al., 2022)
Interleave reasoning (chain-of-thought) with actions (tool use) — foundation of agentic AI.

---

## Impact on AI Implementation

CoT prompting is now **standard practice**:
- All modern AI assistants (Claude, GPT-4, Gemini) use CoT by default for reasoning tasks
- "Let's think step by step" is one of the most powerful prompt additions
- System prompts often instruct models to reason before answering
- CoT is the foundation of tool-use, agentic, and multi-step AI workflows

---

## Connection to Constitutional AI and RLHF

Chain-of-thought reasoning can be used to:
- Generate explanations for preference choices (used in Constitutional AI critique steps)
- Create training data for reasoning-capable models
- Evaluate the quality of model reasoning (not just final answers)
- Enable process-based supervision (reward reasoning steps, not just outcomes)

---

## Key Terms

- **Chain-of-Thought (CoT)**: Including step-by-step reasoning in prompts/outputs
- **Few-shot prompting**: Providing examples in the prompt
- **Zero-shot CoT**: Triggering reasoning with "Let's think step by step" without examples
- **Self-consistency**: Sampling multiple reasoning paths and taking majority vote
- **Emergent capability**: Ability that appears at scale, absent in smaller models
- **Process supervision**: Rewarding correct reasoning steps, not just correct final answers

---

## Authors

- **Jason Wei** — Google Brain; also contributed to scaling laws and emergent abilities research
- **Denny Zhou** — Google Brain; senior author; reasoning and prompting researcher
- **Quoc Le** — Google Brain; senior researcher; AutoML, neural architecture search

---

## Citation

Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E., Le, Q., & Zhou, D. (2022). Chain-of-thought prompting elicits reasoning in large language models. *Advances in Neural Information Processing Systems*, 35.
