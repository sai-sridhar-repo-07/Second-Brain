# Reinforcement Learning

Reinforcement learning (RL) is a training paradigm where an agent learns to take actions that maximize a cumulative reward signal from an environment. Unlike supervised learning (learn from labeled examples), RL learns from consequences of actions.

## How Sources Explain This
- **[[alphago-alphazero]]**: RL via self-play — the game outcome (win/loss) is the reward. AlphaGo's policy gradient training and AlphaZero's MCTS-guided RL are among the most successful RL applications.
- **[[constitutional-ai]]**: RLHF/RLAIF uses RL (PPO) with a learned reward model as the environment. The reward model scores outputs; PPO optimizes the LLM to produce higher-scoring responses.

## RL in LLM Training
- PPO (Proximal Policy Optimization): the RL algorithm used in RLHF — prevents the policy from changing too fast
- Reward model: a separate model trained on human (RLHF) or AI (RLAIF) preferences
- KL divergence penalty: prevents the fine-tuned model from diverging too far from the pre-trained base

## Contradictions or Variations
- Classic RL (games, robotics): objective reward from environment
- RLHF: subjective reward from human preferences — more complex, potentially gameable
- DPO (Direct Preference Optimization, 2023): bypasses RL entirely, optimizes preference directly — simpler and often better than PPO for LLM alignment

## Related Concepts
- [[rlhf-and-rlaif]]
- [[pre-training-and-fine-tuning]]
