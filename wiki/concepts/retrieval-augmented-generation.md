# Retrieval-Augmented Generation (RAG)

RAG combines a retrieval system (finds relevant documents from an external corpus) with a generative LLM (produces an answer conditioned on the retrieved context). It grounds model outputs in verified external knowledge, reducing hallucination and enabling up-to-date responses.

## How Sources Explain This
- **[[rag]]**: Original paper uses Dense Passage Retrieval (DPR) to retrieve top-k documents, then BART to generate answers. The model retrieves documents matching the query by dense vector similarity, then generates conditioned on both query + retrieved documents.
- **[[word2vec]]**: The fundamental operation in RAG retrieval — text to dense vector — traces back to Word2Vec's insight that distributed representations capture semantic similarity.

## How It Works (Modern)
1. Documents → chunks → embed → store in vector database
2. Query → embed → similarity search → top-k chunks
3. LLM generates answer conditioned on: system prompt + retrieved chunks + user query

## Contradictions or Variations
- RAG vs fine-tuning: RAG better for frequently changing data; fine-tuning better for style/format/behavior
- GraphRAG (Microsoft): builds knowledge graph from documents — better for multi-hop reasoning than naive chunk retrieval
- Self-RAG: model decides when to retrieve — more selective than always retrieving

## Related Concepts
- [[vector-embeddings]]
- [[in-context-learning]]
- [[pre-training-and-fine-tuning]]
