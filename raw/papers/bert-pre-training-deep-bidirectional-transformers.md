# BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding

**Authors**: Jacob Devlin, Ming-Wei Chang, Kenton Lee, Kristina Toutanova
**Institution**: Google AI Language
**Published**: 2018 (NeurIPS 2018 Workshop, full paper NAACL 2019)

---

## Overview

BERT (Bidirectional Encoder Representations from Transformers) introduced a new paradigm for NLP: pre-train a deep bidirectional Transformer on massive unlabeled text, then fine-tune it on specific downstream tasks. It achieved state-of-the-art on 11 NLP benchmarks and fundamentally changed how NLP models are built. Before BERT, models were mostly trained from scratch on task-specific data. After BERT, the field shifted to pre-train then fine-tune.

---

## The Core Problem BERT Solved

Prior language models were **unidirectional** — they read text left-to-right (or right-to-left). This limits representation quality because each token's representation only includes context from one direction.

- GPT (2018): left-to-right Transformer decoder — works well for generation, poor for understanding
- ELMo: concatenates separate left-to-right and right-to-left LSTMs — shallow bidirectionality

BERT's insight: use a **masked language model** objective to train a truly bidirectional Transformer. Every token sees context from both left and right simultaneously.

---

## Pre-training Tasks

### 1. Masked Language Model (MLM)
- Randomly mask 15% of input tokens
- Model must predict the original token from context
- Of the 15%: 80% replaced with [MASK], 10% replaced with random word, 10% left unchanged
- This prevents the model from simply "seeing" the answer and forces use of bidirectional context

### 2. Next Sentence Prediction (NSP)
- Given two sentences A and B, predict whether B follows A in the original text
- 50% of pairs are real consecutive sentences, 50% are random
- Teaches the model sentence-level relationships — important for tasks like question answering and inference

---

## Architecture

- Based on the Transformer encoder (from "Attention Is All You Need")
- **BERT-Base**: 12 layers, 768 hidden dimensions, 12 attention heads, 110M parameters
- **BERT-Large**: 24 layers, 1024 hidden dimensions, 16 attention heads, 340M parameters
- Input representation: token embeddings + segment embeddings + positional embeddings
- Special tokens: [CLS] at start (classification token), [SEP] between sentences

---

## Fine-tuning

After pre-training, BERT is fine-tuned on specific tasks by adding a small task-specific output layer:

- **Classification** (sentiment, spam): Use [CLS] token representation → linear layer
- **Token classification** (NER, POS tagging): Use each token's representation → linear layer
- **Question answering** (SQuAD): Predict start and end positions of answer span
- **Sentence pair tasks** (entailment, similarity): Feed both sentences with [SEP]

Fine-tuning is cheap — only a few epochs needed. The heavy lifting is done during pre-training.

---

## Results

- **GLUE benchmark**: 80.5% (7.7% improvement over prior SOTA)
- **SQuAD v1.1**: 93.2 F1 (surpassed human performance of 91.2)
- **SQuAD v2.0**: 83.1 F1
- **SWAG**: 86.3% accuracy
- Achieved SOTA on 11 NLP tasks simultaneously

---

## Why BERT Was Revolutionary

1. **Transfer learning came to NLP**: Like ImageNet pre-training for vision, BERT provided a general-purpose language representation
2. **Bidirectionality at scale**: First model to effectively train bidirectional deep Transformers
3. **Democratized NLP**: Anyone could download BERT and fine-tune on their task with limited data and compute
4. **Pre-train once, fine-tune everywhere**: Shifted NLP from task-specific models to foundation models

---

## Limitations

- **Encoder-only**: Cannot generate text — not suitable for language generation tasks
- **[MASK] token mismatch**: Masking during pre-training creates a mismatch with downstream tasks (no [MASK] tokens at inference)
- **NSP task criticized**: Later work (RoBERTa) showed NSP hurts rather than helps — removed in successors
- **Fixed sequence length**: Limited to 512 tokens
- **Quadratic attention**: O(n²) complexity limits context window

---

## Successors and Impact

- **RoBERTa** (Facebook, 2019): Removed NSP, trained longer with more data — stronger BERT
- **ALBERT** (Google, 2019): Parameter-efficient BERT with factorized embeddings
- **DistilBERT** (HuggingFace, 2019): 40% smaller, 60% faster, retains 97% of performance
- **DeBERTa** (Microsoft, 2020): Disentangled attention, better positional encoding
- **Domain-specific BERTs**: BioBERT (biomedical), LegalBERT, FinBERT, CodeBERT

---

## Key Terms

- **MLM (Masked Language Model)**: Pre-training objective where random tokens are masked and predicted
- **NSP (Next Sentence Prediction)**: Pre-training objective predicting sentence order
- **[CLS] token**: Special classification token whose representation is used for sentence-level tasks
- **[SEP] token**: Separator token between sentence pairs
- **Fine-tuning**: Adapting a pre-trained model to a specific downstream task
- **Transfer learning**: Using knowledge from one task to improve performance on another

---

## Authors

- **Jacob Devlin** — Google AI, lead author
- **Ming-Wei Chang** — Google AI
- **Kenton Lee** — Google AI
- **Kristina Toutanova** — Google AI

---

## Citation

Devlin, J., Chang, M. W., Lee, K., & Toutanova, K. (2018). BERT: Pre-training of deep bidirectional transformers for language understanding. *arXiv preprint arXiv:1810.04805*.
