# Word2Vec: Efficient Estimation of Word Representations in Vector Space

**Authors**: Tomas Mikolov, Kai Chen, Greg Corrado, Jeffrey Dean
**Institution**: Google
**Published**: 2013 (ICLR 2013)

---

## Overview

Word2Vec introduced efficient neural methods for learning dense vector representations of words (word embeddings) from large text corpora. Words with similar meanings end up with similar vector representations, and the vectors capture semantic relationships through arithmetic: "king" - "man" + "woman" ≈ "queen". Word2Vec is the foundational work for all modern text embeddings and is the precursor to contextual embeddings (BERT, sentence transformers) used in RAG and semantic search today.

---

## The Core Idea: Words as Vectors

Before Word2Vec, words were represented as one-hot vectors — extremely sparse, with no semantic information. A vocabulary of 100k words = 100k-dimensional vectors with one 1 and 99,999 zeros.

Word2Vec learns dense, low-dimensional vectors (50-300 dimensions) where:
- Similar words are nearby in vector space
- Semantic relationships are encoded as directions

Famous examples:
```
vec("king") - vec("man") + vec("woman") ≈ vec("queen")
vec("Paris") - vec("France") + vec("Italy") ≈ vec("Rome")
vec("bigger") - vec("big") + vec("small") ≈ vec("smaller")
```

---

## Two Architectures

### CBOW (Continuous Bag of Words)
Predict the target word from surrounding context words:
```
[w_{t-2}, w_{t-1}, w_{t+1}, w_{t+2}] → predict w_t
```
- Faster to train
- Slightly better for frequent words

### Skip-gram
Predict surrounding context words from the target word:
```
w_t → predict [w_{t-2}, w_{t-1}, w_{t+1}, w_{t+2}]
```
- Better for rare words
- More commonly cited

### Negative Sampling
Training with full softmax over 100k vocabulary is expensive. Negative sampling trains by:
- Making the embedding of the target word similar to its context (positive pair)
- Making it dissimilar from k randomly sampled "negative" words (k=5-20)
- Simple binary classification instead of 100k-way softmax

---

## Why Embeddings Work

The **distributional hypothesis**: words that appear in similar contexts have similar meanings (Firth, 1957: "You shall know a word by the company it keeps").

Word2Vec operationalizes this: if "cat" and "dog" frequently appear near the same words ("pet", "feed", "vet"), their vectors become similar.

---

## Impact and Legacy

### Direct Applications (2013-2018)
- NLP benchmarks improved across the board by initializing with pretrained Word2Vec
- Semantic search: find documents similar to a query using vector similarity
- Recommendation systems: model user preferences as vectors

### Path to Modern Embeddings
Word2Vec → GloVe → FastText → ELMo → BERT → Sentence Transformers

| Model | Year | Key Improvement |
|-------|------|-----------------|
| Word2Vec | 2013 | Dense word vectors |
| GloVe | 2014 | Global co-occurrence statistics |
| FastText | 2016 | Subword embeddings (handles rare words) |
| ELMo | 2018 | Contextual word embeddings (same word, different vectors in different contexts) |
| BERT | 2018 | Full bidirectional contextual embeddings |
| Sentence-BERT | 2019 | Sentence-level embeddings for semantic similarity |

### Modern RAG Connection
Every RAG system uses embeddings descended from Word2Vec's insight:
- Text chunks → dense vectors → stored in vector database
- Query → dense vector → cosine similarity search
- The fundamental operation is the same; the embeddings are just richer (contextual)

---

## Key Terms

- **Word embedding**: Dense vector representation of a word
- **Semantic similarity**: Words with similar meanings have similar vectors (high cosine similarity)
- **Cosine similarity**: Dot product of normalized vectors — measures angle between vectors
- **Distributional hypothesis**: Word meaning is defined by usage context
- **Negative sampling**: Training trick to avoid expensive full vocabulary softmax
- **Subword**: Word pieces (e.g., "running" = "run" + "##ning") — used in BERT tokenizers

---

## Authors

- **Tomas Mikolov** — Google Brain; lead author; later Facebook AI Research, then Meta AI
- **Jeffrey Dean** — Google; co-inventor of MapReduce and TensorFlow; senior author

---

## Citation

Mikolov, T., Chen, K., Corrado, G., & Dean, J. (2013). Efficient estimation of word representations in vector space. *arXiv preprint arXiv:1301.3781*.
