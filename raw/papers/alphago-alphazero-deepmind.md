# AlphaGo / AlphaZero: Mastering Games with Deep Reinforcement Learning

**Key Papers**:
- AlphaGo: Mastering the game of Go with deep neural networks and tree search (Silver et al., Nature 2016)
- AlphaGo Zero: Mastering the game of Go without human knowledge (Silver et al., Nature 2017)
- AlphaZero: A general reinforcement learning algorithm that masters chess, shogi, and Go (Silver et al., Science 2018)

**Institution**: DeepMind (Google DeepMind)

---

## Overview

AlphaGo was the first AI to defeat a professional human Go player (and later world champion Lee Sedol). Go was considered AI's hardest challenge — more complex than chess, with a game tree of 10^170 possible positions (vs 10^47 for chess). AlphaGo Zero then learned to play Go from scratch with no human data, solely through self-play, reaching superhuman performance in 3 days. AlphaZero generalized this to chess and shogi. These systems demonstrated that deep reinforcement learning combined with search could achieve superhuman performance on complex strategic tasks.

---

## Why Go Was Hard for AI

Chess was solved (IBM Deep Blue, 1997) using handcrafted evaluation functions + tree search. Go resisted this approach:
- **Branching factor**: ~250 moves per position (vs ~35 in chess)
- **Position evaluation**: Extremely difficult to evaluate "who's winning" in a Go position
- **Depth**: Games last ~200 moves
- No good handcrafted evaluation function existed

---

## AlphaGo (2016): The First Version

Uses three components:

### 1. Policy Network (SL)
- 13-layer CNN trained on 30 million expert human moves (supervised learning)
- Outputs a probability distribution over legal moves
- Used to: guide tree search, initialize RL policy

### 2. Policy Network (RL)
- Initialized from SL policy network
- Improved via self-play reinforcement learning (policy gradient)
- Wins 80% of games against SL policy network

### 3. Value Network
- Predicts probability of winning from a given board position
- Trained on positions from RL self-play games
- Used to: evaluate positions without full rollout

### 4. Monte Carlo Tree Search (MCTS)
- Combines policy network (to guide search) + value network (to evaluate leaves)
- Explores millions of possible continuations
- Selects the move with highest expected win rate

**Result**: 5-0 victory over Fan Hui (European champion, 2015); 4-1 victory over Lee Sedol (world champion, 2016)

---

## AlphaGo Zero (2017): No Human Data

AlphaGo Zero learns entirely from self-play, starting from random play:

- **No human data**: No expert games used
- **Single neural network**: Combines policy and value into one network
- **Self-play only**: Generates all training data by playing against itself
- **Residual architecture**: Uses ResNet instead of CNN
- **3 days of training**: Achieves superhuman performance (beats original AlphaGo 100-0)

### Why Removing Human Data Helped
Human games constrain the AI to human strategies. Without this constraint, AlphaGo Zero discovered:
- Novel openings not seen in human play
- More efficient strategies that human players had never found in thousands of years of Go history

---

## AlphaZero (2018): General Algorithm

Generalizes to any two-player game with perfect information:
- Learned chess from scratch: defeated Stockfish (world's best chess engine) after 9 hours
- Learned shogi from scratch: defeated Elmo (world's best shogi engine) after 2 hours
- Learned Go from scratch: better than AlphaGo Zero

Single algorithm, no game-specific knowledge except rules. Demonstrates a general approach to mastering strategic games.

---

## Technical Insights Relevant to Modern AI

### Self-Play and RLHF
AlphaGo Zero's self-play loop is structurally similar to RLHF:
- Generate outputs (games)
- Evaluate outputs (win/loss)
- Train to improve (policy gradient)
The difference: evaluation is objective (win/loss) vs subjective (human preference)

### Search + Neural Network
The combination of a learned policy/value network with Monte Carlo Tree Search is a general pattern:
- Network prunes the search space (which moves to explore)
- Search corrects for network errors (verifying promising moves)
- Modern AI reasoning systems use similar patterns (e.g., tree-of-thoughts, process reward models)

### Emergent Strategies
AlphaGo Zero discovered Go strategies not known to human players — strong evidence that data-free self-play can discover knowledge beyond the training distribution.

---

## Impact on AI Research

1. Proved deep RL can master complex strategic tasks
2. Demonstrated self-play as a scalable training paradigm
3. Influenced reasoning research: AlphaCode (code competition), AlphaFold (protein folding)
4. AlphaFold (2020): Applied similar ideas to protein structure prediction — solved a 50-year biology problem

---

## Key Terms

- **Monte Carlo Tree Search (MCTS)**: Search algorithm using random rollouts to evaluate moves
- **Policy network**: Neural network outputting move probabilities
- **Value network**: Neural network estimating win probability from a position
- **Self-play**: Training by having the model play against itself
- **Reinforcement learning**: Learning from rewards (win/loss) rather than labeled data
- **Policy gradient**: RL algorithm that directly optimizes the policy using gradient ascent on expected reward

---

## Key Institution

- **DeepMind**: London-based AI research lab acquired by Google in 2014; merged with Google Brain to form Google DeepMind in 2023

## Key Researchers

- **David Silver** — DeepMind; lead researcher on all AlphaGo/AlphaZero papers
- **Demis Hassabis** — Co-founder and CEO of DeepMind; Turing Award 2024

---

## Citations

Silver, D., et al. (2016). Mastering the game of Go with deep neural networks and tree search. *Nature*, 529(7587), 484–489.

Silver, D., et al. (2017). Mastering the game of Go without human knowledge. *Nature*, 550(7676), 354–359.

Silver, D., et al. (2018). A general reinforcement learning algorithm that masters chess, shogi, and Go through self-play. *Science*, 362(6419), 1140–1144.
