# Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks

**Authors**: Patrick Lewis, Ethan Perez, Aleksandra Piktus, Fabio Petroni, Vladimir Karpukhin, Naman Goyal, Heinrich Küttler, Mike Lewis, Wen-tau Yih, Tim Rocktäschel, Sebastian Riedel, Douwe Kiela
**Institution**: Facebook AI Research (FAIR) / University College London
**Published**: 2020 (NeurIPS 2020)

---

## Overview

RAG (Retrieval-Augmented Generation) combines a parametric memory (the LLM's trained weights) with a non-parametric memory (a searchable document store) to ground language model outputs in retrieved facts. The model retrieves relevant documents from an external corpus, then conditions its generation on both the question and the retrieved documents. RAG prevents hallucination, enables up-to-date knowledge, and allows citing sources — making it one of the most widely deployed patterns in production AI systems.

---

## The Problem: LLMs Have Stale, Uncertain Knowledge

Pure language models have two fundamental limitations:
1. **Static knowledge**: Training data has a cutoff date — models don't know about recent events
2. **Hallucination**: Models confabulate facts confidently, especially for specific factual queries
3. **No attribution**: Models can't cite which source a fact came from
4. **Expensive to update**: Retraining a 175B model to add new facts costs millions of dollars

---

## The RAG Architecture

RAG has two components:

### 1. Retriever
A dense retrieval system that, given a query, retrieves the top-k most relevant documents from a corpus:
- Query is encoded into a dense vector using a bi-encoder (DPR — Dense Passage Retriever)
- All documents in the corpus are pre-encoded and stored in a vector index (FAISS)
- Similarity search finds top-k documents (k=5 in original paper)

### 2. Generator
A sequence-to-sequence model (original paper uses BART) that:
- Takes the query + retrieved documents as input
- Generates an answer conditioned on all retrieved context

### Two RAG Variants

**RAG-Sequence**: Retrieve once, use same documents for entire output
```
p(y|x) = Σ p_η(z|x) * p_θ(y|x,z)
```

**RAG-Token**: Re-retrieve at each generation step — different documents can inform different tokens
```
p(y_i|x, y_{1:i-1}) = Σ p_η(z|x) * p_θ(y_i|x,z,y_{1:i-1})
```

---

## Dense Passage Retrieval (DPR)

The retriever uses dual BERT encoders:
- Question encoder: encodes query q into vector q_e
- Passage encoder: encodes each passage p into vector p_e
- Similarity: dot product q_e · p_e

Trained with in-batch negatives (treat other passages in the same batch as negatives). Much better than BM25 (TF-IDF based) for open-domain QA.

---

## Results

| Task | Closed-book LM | RAG |
|------|----------------|-----|
| Natural Questions | 44.5% | 44.5% |
| TriviaQA | 47.4% | 56.8% |
| WebQuestions | 41.7% | 45.5% |
| Jeopardy question gen (ROUGE-L) | 14.7 | 17.9 |
| MS-MARCO BLEU | 26.9 | 28.1 |

RAG outperforms closed-book GPT models and specialized extractive QA systems.

---

## Modern RAG Patterns (Post-2020)

The original paper used fixed corpora. Modern RAG has evolved significantly:

### Naive RAG
1. Split documents into chunks
2. Embed chunks with an embedding model
3. Store in vector database (Pinecone, Weaviate, Chroma, pgvector)
4. At query time: embed query, find top-k similar chunks, inject into prompt
5. LLM generates answer from retrieved context

### Advanced RAG Techniques
- **HyDE** (Gao et al., 2022): Generate a hypothetical answer, use that to retrieve — better than using raw query
- **Self-RAG** (Asai et al., 2023): Model decides when to retrieve, reflects on retrieved content quality
- **RAPTOR** (Sarthi et al., 2024): Hierarchical summarization tree for long documents
- **GraphRAG** (Microsoft, 2024): Build knowledge graph from documents, retrieve via graph traversal
- **Reranking**: Use a cross-encoder to rerank initial retrievals before passing to LLM

---

## RAG vs Fine-tuning

| Use Case | RAG | Fine-tuning |
|----------|-----|-------------|
| Frequently changing data | Better | Impractical |
| Domain-specific style/tone | Limited | Better |
| Specific factual knowledge | Better | Possible but expensive |
| Source attribution | Built-in | Not available |
| No training data needed | Yes | No |
| Hallucination reduction | Strong | Moderate |

For most production use cases, RAG is preferred for knowledge-intensive tasks; fine-tuning is preferred for style/format/behavior adaptation.

---

## Key Terms

- **RAG**: Retrieval-Augmented Generation — combining retrieval with generation
- **Dense retrieval**: Using neural network embeddings to find similar documents
- **Vector database**: Stores document embeddings for efficient similarity search
- **DPR**: Dense Passage Retriever — the dual-encoder retrieval model
- **Chunk**: A segment of a document (typically 100-500 tokens) stored as a retrieval unit
- **Embedding**: Dense vector representation of text
- **Top-k**: Retrieve the k most similar documents (k=5 is common default)
- **Hallucination**: LLM generating factually incorrect but confident-sounding text
- **Grounding**: Connecting LLM outputs to verified external sources

---

## Authors

- **Patrick Lewis** — Facebook AI Research / UCL; lead author; later at Cohere
- **Ethan Perez** — Facebook AI Research; also contributed to Constitutional AI direction
- **Douwe Kiela** — Facebook AI Research; NLP researcher; later founded Contextual AI

---

## Citation

Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., ... & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. *Advances in Neural Information Processing Systems*, 33, 9459–9474.
