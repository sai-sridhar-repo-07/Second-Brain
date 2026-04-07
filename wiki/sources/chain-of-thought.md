# Chain-of-Thought Prompting

Google Research's 2022 paper showing that including step-by-step reasoning examples in prompts dramatically improves LLM performance on complex reasoning tasks. Foundation of modern prompting strategies and agentic AI.

## Key Contributions
- Including reasoning traces in few-shot examples triggers the model to reason step-by-step
- Only helps large models (≥100B parameters) — reveals emergent capability
- Zero-shot CoT: "Let's think step by step" triggers reasoning without examples
- Self-consistency: sample multiple CoT paths, take majority vote on final answer

## Performance Gains
- GSM8K (math): 18% → 58% with GPT-3 + CoT
- MultiArith: 33% → 93%

## Extensions
- Tree of Thoughts (ToT): explore branching reasoning trees
- ReAct: interleave reasoning with tool use (foundation of agents)

## Related Concepts
- [[in-context-learning]]
- [[few-shot-prompting]]
- [[agentic-workflows]]

## Related Entities
- [[google-brain]]
- [[jason-wei]]

`Source: raw/chain-of-thought-prompting.md`
