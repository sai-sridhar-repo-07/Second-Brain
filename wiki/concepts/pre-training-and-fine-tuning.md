# Pre-training and Fine-tuning

Pre-training is the process of training a large model on a massive general dataset (text, images) to learn broadly useful representations. Fine-tuning adapts this pre-trained model to a specific task with a smaller dataset and fewer compute resources. Together they form the dominant paradigm for building production AI systems.

## How Sources Explain This
- **[[bert]]**: Pre-train a bidirectional Transformer on 3.3B tokens (Books + Wikipedia) using MLM + NSP; fine-tune on specific tasks by adding a small output head. Achieved SOTA on 11 tasks from one base model.
- **[[gpt3]]**: Pre-train a 175B decoder-only Transformer on 300B tokens; the model can perform tasks in-context without any fine-tuning (few-shot learning).
- **[[scaling-laws]]**: Pre-training loss follows power laws. Compute-optimal pre-training allocates budget between N (parameters) and D (tokens). Chinchilla: 20 tokens per parameter for compute-optimal training.
- **[[lora]]**: Full fine-tuning is expensive; LoRA enables parameter-efficient fine-tuning by adding small low-rank adapters to a frozen pre-trained model.

## Contradictions or Variations
- Original BERT paradigm: always fine-tune on downstream task
- GPT-3 showed fine-tuning is often unnecessary — in-context learning can match it
- Chinchilla revised the compute-optimal pre-training recipe: more tokens, smaller model vs. original Kaplan et al. recommendation of larger model, fewer tokens

## Related Concepts
- [[parameter-efficient-fine-tuning]]
- [[in-context-learning]]
- [[masked-language-model]]
- [[scaling-laws]]
- [[transfer-learning]]
