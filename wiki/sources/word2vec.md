# Word2Vec: Efficient Estimation of Word Representations in Vector Space

Google's 2013 paper introducing Word2Vec — learning dense word vector representations from text. Words with similar meanings cluster together in vector space; semantic relationships are encoded as directions. Foundation of all modern text embeddings and RAG systems.

## Key Contributions
- CBOW: predict target word from context; Skip-gram: predict context from target word
- Negative sampling: efficient training without full vocabulary softmax
- Word arithmetic: king - man + woman ≈ queen
- Distributional hypothesis: meaning defined by context

## Legacy
- Direct path to: GloVe → FastText → ELMo → BERT → Sentence Transformers
- Modern RAG uses the same concept: text → dense vector → cosine similarity search

## Related Concepts
- [[vector-embeddings]]
- [[retrieval-augmented-generation]]
- [[pre-training-and-fine-tuning]]

## Related Entities
- [[tomas-mikolov]]
- [[google-brain]]

`Source: raw/word2vec-embeddings.md`
