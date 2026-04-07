# In-Context Learning

In-context learning (ICL) is the ability of a language model to perform a task by reading examples or instructions in its prompt, without any weight updates. The model adapts to a task at inference time purely through the context window.

## How Sources Explain This
- **[[gpt3]]**: Introduced zero-shot, one-shot, and few-shot ICL. Model reads task examples in the prompt and generalizes to new instances. Performance scales with model size — only emerges robustly at ~100B+ parameters.
- **[[chain-of-thought]]**: Extends ICL by including reasoning traces in examples. "Thinking out loud" dramatically improves performance on multi-step tasks — a form of ICL for reasoning.
- **[[constitutional-ai]]**: Uses ICL for critique-revision: provides the model with a principle and asks it to identify violations in its own response — no fine-tuning required for the critique step.

## Contradictions or Variations
- ICL vs fine-tuning: GPT-3 showed ICL can match fine-tuned performance on many tasks; but fine-tuning still wins on task-specific benchmarks requiring precise behavior
- ICL is sensitive to: prompt format, order of examples, and choice of examples — not fully understood

## Related Concepts
- [[few-shot-prompting]]
- [[chain-of-thought-prompting]]
- [[pre-training-and-fine-tuning]]
- [[scaling-laws]]
