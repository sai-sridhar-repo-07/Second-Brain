# AlphaGo / AlphaZero: Mastering Games with Deep Reinforcement Learning

DeepMind's landmark papers (2016–2018) defeating world champions at Go, chess, and shogi using deep RL + Monte Carlo Tree Search. AlphaGo Zero learned entirely from self-play with no human data — discovering novel strategies humans had never found.

## Key Contributions
- AlphaGo (2016): Policy network + Value network + MCTS — beat Lee Sedol 4-1
- AlphaGo Zero (2017): Self-play only, no human data, single ResNet — beat AlphaGo 100-0 in 3 days
- AlphaZero (2018): Generalized to chess/shogi — one algorithm, no domain knowledge except rules
- Self-play discovered Go strategies unknown to humans after thousands of years

## Relevance to Modern AI
- Self-play loop structurally similar to RLHF (generate → evaluate → improve)
- Search + neural network pattern: model prunes search space, search corrects model errors
- Led to AlphaFold (protein folding) and AlphaCode (programming)

## Related Concepts
- [[reinforcement-learning]]
- [[rlhf-and-rlaif]]

## Related Entities
- [[deepmind]]
- [[demis-hassabis]]

`Source: raw/alphago-alphazero-deepmind.md`
