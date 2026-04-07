# Vector Embeddings

A vector embedding is a dense, low-dimensional numerical representation of discrete objects (words, sentences, images, documents). Objects with similar meaning or function have similar vectors — measurable via cosine similarity or dot product. Embeddings are the bridge between symbolic data and neural network computation.

## How Sources Explain This
- **[[word2vec]]**: First practical large-scale word embeddings. Trained by predicting surrounding context (skip-gram) or target from context (CBOW). Word arithmetic works: king - man + woman ≈ queen. Foundation of all modern embeddings.
- **[[bert]]**: Contextual embeddings — same word has different vectors in different contexts ("bank" in finance vs. river). [CLS] token embedding represents the whole sentence.
- **[[rag]]**: RAG uses sentence/passage embeddings for retrieval. Queries and documents are embedded into the same space; cosine similarity finds relevant documents.
- **[[vision-transformer]]**: Image patches are linearly projected into embedding space — same concept as word embeddings, applied to image regions.

## Contradictions or Variations
- Static embeddings (Word2Vec): one vector per word regardless of context
- Contextual embeddings (BERT, LLMs): vector depends on surrounding context — richer but requires full model pass
- For retrieval (RAG), sentence-level embeddings (Sentence-BERT, OpenAI ada-002) are used, not per-token

## Related Concepts
- [[retrieval-augmented-generation]]
- [[pre-training-and-fine-tuning]]
- [[self-attention]]
