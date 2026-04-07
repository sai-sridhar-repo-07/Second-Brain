# RLHF and RLAIF

RLHF (Reinforcement Learning from Human Feedback) trains a reward model on human preference labels, then uses RL (typically PPO) to optimize the language model to maximize that reward. RLAIF (RL from AI Feedback) replaces human labels with AI-generated preferences, enabling cheaper and more scalable alignment training.

## How Sources Explain This
- **[[constitutional-ai]]** (Anthropic): Introduces RLAIF — a model trained on human harmlessness preferences is used to evaluate response pairs. The written constitution guides the AI evaluator. Produces models that are simultaneously more helpful and more harmless.
- **[[alphago-alphazero]]**: AlphaGo's self-play loop is structurally analogous: generate outputs (games) → evaluate with win/loss signal → improve policy. The difference is RLHF uses learned human preference as the reward vs. objective win/loss.
- **[[gpt3]]**: GPT-3 was the base for InstructGPT (2022) — first major RLHF-trained model, far more useful than base GPT-3.

## Contradictions or Variations
- RLHF requires human labelers to view potentially harmful content — psychological burden
- RLAIF (Constitutional AI) avoids this but inherits AI model biases
- Debate: reward hacking — models can learn to maximize the reward model without actually improving on the underlying task

## Related Concepts
- [[pre-training-and-fine-tuning]]
- [[chain-of-thought-prompting]]
- [[reinforcement-learning]]
