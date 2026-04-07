# Retrieval-Augmented Generation (RAG)

Facebook AI Research's 2020 paper combining dense retrieval with language model generation — grounding LLM outputs in retrieved external documents. Prevents hallucination, enables up-to-date knowledge, and allows citations. Most widely deployed production AI pattern.

## Key Contributions
- Retrieve top-k relevant documents via Dense Passage Retrieval (DPR) → generate answer conditioned on documents
- RAG-Sequence vs RAG-Token: retrieve once vs re-retrieve per token
- DPR: dual BERT encoders — outperforms BM25 (TF-IDF) for open-domain QA
- Non-parametric knowledge: update retrieval corpus without retraining

## Results
- TriviaQA: 56.8% (vs 47.4% closed-book)
- Outperforms fine-tuned QA systems on open-domain benchmarks

## Modern Extensions
- HyDE: generate hypothetical answer, use it to retrieve
- GraphRAG: knowledge graph for retrieval
- Self-RAG: model decides when to retrieve

## Related Concepts
- [[retrieval-augmented-generation]]
- [[vector-embeddings]]
- [[in-context-learning]]

## Related Entities
- [[facebook-ai-research]]

`Source: raw/rag-retrieval-augmented-generation.md`
