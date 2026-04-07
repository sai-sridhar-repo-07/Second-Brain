# GPT-3: Language Models are Few-Shot Learners

**Authors**: Tom B. Brown, Benjamin Mann, Nick Ryder, Melanie Subbiah, Jared Kaplan, Prafulla Dhariwal, Arvind Neelakantan, Pranav Shyam, Girish Sastry, Amanda Askell, Sandhini Agarwal, Ariel Herbert-Voss, Gretchen Krueger, Tom Henighan, Rewon Child, Aditya Ramesh, Daniel M. Ziegler, Jeffrey Wu, Clemens Winter, Christopher Hesse, Mark Chen, Eric Sigler, Mateusz Litwin, Scott Gray, Benjamin Chess, Jack Clark, Christopher Berner, Sam McCandlish, Alec Radford, Ilya Sutskever, Dario Amodei
**Institution**: OpenAI
**Published**: 2020 (NeurIPS 2020)

---

## Overview

GPT-3 is a 175 billion parameter autoregressive language model that demonstrated remarkable few-shot and zero-shot capabilities across a wide range of NLP tasks — without any gradient updates or fine-tuning. It showed that scaling a decoder-only Transformer to unprecedented size unlocks emergent capabilities: the model can perform tasks simply by reading a few examples in its context window. GPT-3 kickstarted the modern LLM era and the race to scale.

---

## The Core Insight: In-Context Learning

Before GPT-3, the dominant paradigm was pre-train → fine-tune. GPT-3 introduced a new paradigm: **in-context learning** — the model adapts to a task based purely on examples provided in the prompt, with no weight updates.

Three modes demonstrated:
- **Zero-shot**: No examples, just a task description — "Translate English to French: cheese =>"
- **One-shot**: One example provided before the query
- **Few-shot**: Several examples (up to the context window limit) provided before the query

The key finding: performance scales smoothly with the number of in-context examples, and larger models benefit more from them.

---

## Architecture

GPT-3 is a **decoder-only Transformer** (autoregressive), building on GPT-2:

- **175 billion parameters** — 100x larger than GPT-2
- 96 layers
- 96 attention heads
- 12,288 hidden dimensions
- Context window: 2,048 tokens
- Uses alternating dense and locally banded sparse attention layers
- Trained on 300 billion tokens from Common Crawl, WebText2, Books1, Books2, Wikipedia

### Model Variants Tested
The paper trained 8 model sizes from 125M to 175B parameters to study scaling behavior:
- Ada (350M), Babbage (1.3B), Curie (6.7B), Davinci (175B)

---

## Training Data

- **Common Crawl** (filtered): 410B tokens, weighted at 60%
- **WebText2** (Reddit links): 19B tokens
- **Books1 + Books2**: 67B tokens
- **Wikipedia**: 3B tokens
- Total training mix: ~300B tokens

Data quality filtering was critical — raw Common Crawl is noisy. They filtered using a classifier trained to distinguish high-quality text from low-quality.

---

## Key Results

- **SuperGLUE**: Near SOTA on several tasks with few-shot, no fine-tuning
- **TriviaQA**: 71.2% (one-shot), competitive with fine-tuned models
- **Translation**: Competitive on English→French, English→German
- **Arithmetic**: Surprising ability to do 2-3 digit addition/subtraction
- **SAT analogies**: 65.2% (few-shot) vs 57% human average
- **News article generation**: Humans could only distinguish GPT-3 articles from real 52% of the time

---

## Emergent Capabilities

GPT-3 demonstrated abilities not seen in smaller models:
- Multi-step arithmetic
- Code generation (rudimentary)
- Answering questions about its own outputs
- Analogical reasoning
- Simple commonsense reasoning

These were described as **emergent** — appearing suddenly at scale, not present in smaller versions. This finding drove subsequent scaling research.

---

## Limitations

- **No gradient updates**: Few-shot is still far below fine-tuned performance on many tasks
- **Context window bottleneck**: Limited to 2,048 tokens — constrains how many examples can be provided
- **Inconsistency**: Outputs can be inconsistent, hallucinate facts, or contradict themselves
- **Bias**: Trained on internet data, inherits biases around gender, race, religion
- **No grounding**: No access to external knowledge, can't look things up
- **Expensive**: 175B parameters require significant inference compute

---

## Why GPT-3 Changed Everything

1. **Proved scaling works**: Showed that raw compute + data + scale = emergent capability
2. **Made fine-tuning optional**: Few-shot prompting became a viable alternative for many tasks
3. **Launched the API era**: OpenAI released GPT-3 via API — first time a major LLM was commercialized
4. **Inspired GPT-4, Claude, PaLM, LLaMA**: Every subsequent LLM was built in response to GPT-3
5. **Introduced "prompt engineering"**: Practitioners discovered that phrasing prompts carefully dramatically affected output quality

---

## Path Forward: What GPT-3 Led To

- **InstructGPT / RLHF (2022)**: Fine-tuning GPT-3 with human feedback — much more useful
- **ChatGPT (2022)**: InstructGPT optimized for conversation
- **GPT-4 (2023)**: Multimodal, stronger reasoning
- **Constitutional AI / Claude**: Anthropic's alignment-focused alternative
- **Scaling laws paper**: Formalized the relationship between compute, data, and performance

---

## Key Authors

- **Tom Brown** — Lead author, OpenAI
- **Jared Kaplan** — Co-author, later co-authored Scaling Laws paper
- **Ilya Sutskever** — Co-founder and Chief Scientist, OpenAI
- **Dario Amodei** — VP of Research at OpenAI during GPT-3; later co-founded Anthropic
- **Alec Radford** — OpenAI researcher, also lead on GPT-1, GPT-2, CLIP

---

## Citation

Brown, T. B., Mann, B., Ryder, N., et al. (2020). Language models are few-shot learners. *Advances in Neural Information Processing Systems*, 33, 1877–1901.
