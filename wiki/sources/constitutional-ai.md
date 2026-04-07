# Constitutional AI: Harmlessness from AI Feedback

Anthropic's 2022 paper introducing Constitutional AI — training harmlessness using AI-generated feedback guided by a written set of principles (constitution), rather than human labeling. Introduced RLAIF (RL from AI Feedback) as a scalable alternative to RLHF. Central to how Claude is trained.

## Key Contributions
- Two-phase training: SL-CAI (supervised) + RL-CAI (reinforcement from AI feedback)
- Critique-revision loop: model critiques its own harmful responses, revises them
- Written constitution makes AI values explicit and auditable
- RLAIF: AI-generated preferences replace expensive human labels for harmlessness

## Results
- Less harmful outputs than RLHF-only models on red-team evaluations
- Significant reduction in human labeling required
- Models can be simultaneously more helpful AND more harmless

## Related Concepts
- [[rlhf-and-rlaif]]
- [[chain-of-thought-prompting]]
- [[in-context-learning]]

## Related Entities
- [[anthropic]]
- [[dario-amodei]]

`Source: raw/constitutional-ai-anthropic.md`
