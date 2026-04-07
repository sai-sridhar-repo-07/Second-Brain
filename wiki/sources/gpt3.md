# GPT-3: Language Models are Few-Shot Learners

OpenAI's 2020 paper introducing a 175B parameter decoder-only Transformer that demonstrated in-context learning — performing tasks from prompt examples without any gradient updates. Kickstarted the modern LLM era.

## Key Contributions
- In-context learning: zero-shot, one-shot, few-shot without fine-tuning
- Demonstrated emergent capabilities at scale (arithmetic, analogical reasoning)
- Showed performance scales smoothly with model size
- First major LLM released via commercial API

## Results
- TriviaQA: 71.2% one-shot (competitive with fine-tuned models)
- News article generation indistinguishable from human 52% of the time
- Near-SOTA on many SuperGLUE tasks without fine-tuning

## Limitations
- Context window limited to 2,048 tokens
- No gradient updates — few-shot still behind fine-tuned models on many tasks
- Hallucination, inconsistency, and bias from internet training data

## Related Concepts
- [[in-context-learning]]
- [[few-shot-prompting]]
- [[scaling-laws]]
- [[transformer-architecture]]
- [[encoder-decoder]]

## Related Entities
- [[openai]]
- [[ilya-sutskever]]
- [[dario-amodei]]
- [[jared-kaplan]]

`Source: raw/gpt3-language-models-few-shot-learners.md`
