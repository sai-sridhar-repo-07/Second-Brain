# Constitutional AI: Harmlessness from AI Feedback

**Authors**: Yuntao Bai, Saurav Kadavath, Sandipan Kundu, Amanda Askell, Jackson Kernion, Andy Jones, Anna Chen, Anna Goldie, Azalia Mirhoseini, Cameron McKinnon, Carol Chen, Catherine Olsson, Christopher Olah, Danny Hernandez, Dawn Drain, Deep Ganguli, Eli Tran-Johnson, Ethan Perez, Jamie Kerr, Jared Mueller, Jeff Ladish, Joshua Landau, Kamal Ndousse, Kamile Lukosuite, Liane Lovitt, Michael Sellitto, Nelson Elhage, Nicholas Schiefer, Noemi Mercado, Nova DasSarma, Robert Lasenby, Robin Larson, Sam Ringer, Scott Johnston, Shauna Kravec, Sheer El Showk, Stanislav Fort, Tamera Lanham, Timothy Telleen-Lawton, Tom Conerly, Tom Henighan, Tristan Hume, Samuel R. Bowman, Zac Hatfield-Dodds, Ben Mann, Dario Amodei, Nicholas Joseph, Sam McCandlish, Tom Brown, Jared Kaplan
**Institution**: Anthropic
**Published**: 2022 (arXiv)

---

## Overview

Constitutional AI (CAI) introduces a method for training AI systems to be harmless using AI-generated feedback rather than human labeling — called RLAIF (Reinforcement Learning from AI Feedback). A set of principles (a "constitution") guides the AI to critique and revise its own responses for harmfulness. This dramatically reduces the human labeling burden for safety training and produces models that are both helpful and harmless. CAI is central to how Claude is trained.

---

## The Problem: RLHF at Scale for Safety

RLHF (Reinforcement Learning from Human Feedback) requires humans to label which responses are better — helpful but extremely expensive and slow at scale, especially for safety-relevant (harmful content) comparisons. Human labelers must view potentially harmful content, creating psychological and logistical burdens.

---

## Constitutional AI: Two-Phase Training

### Phase 1: SL-CAI (Supervised Learning from AI feedback)

1. Start with a helpful-only model (no harmlessness training)
2. Generate responses to harmful prompts (red-team prompts)
3. Have the model **critique** its own response against each constitutional principle
4. Have the model **revise** its response based on the critique
5. Repeat critique-revision up to 16 times
6. Use the final revised responses to fine-tune the model via supervised learning

### Phase 2: RL-CAI (Reinforcement Learning from AI feedback)

1. Generate pairs of responses to prompts
2. Have a feedback model (trained on human harmlessness preferences) evaluate which response is better — using the constitution as guidance
3. Use these AI-generated preferences to train a **preference model** (PM)
4. Use RL (PPO) with the PM as the reward signal — no human labels required

---

## The Constitution

A set of principles the AI is instructed to use when critiquing its own outputs. Examples:

- "Choose the response that is least likely to contain harmful or unethical content"
- "Choose the response that is most supportive of human autonomy and individual freedoms"
- "Which response is least likely to be used to harm or manipulate a vulnerable person?"
- "Choose the response that a thoughtful, senior Anthropic employee would consider optimal"

The constitution is explicit and human-readable — it makes the AI's values transparent and auditable in a way that reward model training does not.

---

## Key Innovation: Chain-of-Thought Critique

The model is prompted to:
1. **Identify** the harmful aspect of its response
2. **Explain** why it violates the principle
3. **Rewrite** the response to comply

This chain-of-thought critique produces better revisions than single-step correction. The reasoning traces also serve as training data for more interpretable models.

---

## Results

- Models trained with CAI show less harmful outputs than RLHF-only models on red-team evaluations
- Constitutional models can be both more helpful AND more harmless — reducing the perceived tension between the two
- Human evaluators rate CAI models as more trustworthy
- Significant reduction in human labeling required for harmlessness training

---

## RLAIF vs RLHF

| Property | RLHF | RLAIF (CAI) |
|----------|------|-------------|
| Feedback source | Human labelers | AI model |
| Cost | High (human time) | Low (compute) |
| Scale | Limited | Unlimited |
| Consistency | Variable | More consistent |
| Transparency | Opaque (implicit in human choices) | Explicit (written principles) |
| Bias | Human biases | AI biases from training |

---

## Impact on Claude

Constitutional AI is a core part of how Claude (Anthropic's model) is trained:
- Claude is trained to be helpful, harmless, and honest (HHH)
- The Constitutional AI process enables large-scale harmlessness training
- The "thoughtful Anthropic employee" heuristic in the constitution maps to Claude's guidelines
- Successive Claude models (Claude 1, 2, 3, Sonnet, Opus) all use CAI-derived training

---

## Broader Significance

1. **Transparency**: Making AI values explicit and auditable via a written constitution
2. **Scalability**: AI-generated feedback can scale to billions of examples
3. **Alignment research**: A practical method bridging AI safety theory and production training
4. **Industry adoption**: Influenced Google's alignment work and the broader RLAIF research direction

---

## Key Terms

- **Constitutional AI (CAI)**: Training harmlessness using AI critique guided by a written constitution
- **RLAIF**: Reinforcement Learning from AI Feedback — using AI-generated preference labels
- **RLHF**: Reinforcement Learning from Human Feedback — prior dominant alignment method
- **Constitution**: Set of natural-language principles guiding the AI's self-critique
- **Red-team prompts**: Prompts designed to elicit harmful responses — used to stress-test safety
- **HHH**: Helpful, Harmless, Honest — Anthropic's stated alignment framework
- **PPO**: Proximal Policy Optimization — the RL algorithm used in RLHF/RLAIF

---

## Key Institution

- **Anthropic** — AI safety company; founded 2021 by Dario Amodei, Daniela Amodei, and others who left OpenAI

---

## Citation

Bai, Y., et al. (2022). Constitutional AI: Harmlessness from AI feedback. *arXiv preprint arXiv:2212.08073*.
