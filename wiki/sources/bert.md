# BERT: Pre-training of Deep Bidirectional Transformers

Google AI's 2018 paper introducing bidirectional Transformer pre-training. BERT shifted NLP from task-specific models to the pre-train → fine-tune paradigm, achieving SOTA on 11 benchmarks simultaneously.

## Key Contributions
- Masked Language Model (MLM): randomly mask 15% of tokens, predict from bidirectional context
- Next Sentence Prediction (NSP): pre-train on sentence-pair relationships
- [CLS] token for classification, [SEP] for sentence separation
- BERT-Base (110M params) and BERT-Large (340M params)

## Results
- GLUE: 80.5% (+7.7% over prior SOTA)
- SQuAD v1.1: 93.2 F1 (beat human performance of 91.2)

## Limitations
- Encoder-only — cannot generate text
- Fixed 512-token limit
- NSP task later found to hurt (removed in RoBERTa)

## Related Concepts
- [[pre-training-and-fine-tuning]]
- [[masked-language-model]]
- [[transformer-architecture]]
- [[encoder-decoder]]

## Related Entities
- [[jacob-devlin]]
- [[google-ai]]

`Source: raw/bert-pre-training-deep-bidirectional-transformers.md`
