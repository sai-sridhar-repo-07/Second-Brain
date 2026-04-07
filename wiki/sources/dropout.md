# Dropout: A Simple Way to Prevent Neural Networks from Overfitting

University of Toronto's 2014 paper formalizing Dropout — randomly zeroing neuron activations during training to prevent co-adaptation and overfitting. Standard regularization technique, first used in AlexNet (2012) before this formal paper.

## Key Contributions
- Randomly zeros p fraction of neurons per forward pass (p=0.5 default)
- Inverted dropout: scale by 1/(1-p) during training, no scaling at inference
- Ensemble interpretation: approximates averaging 2^n subnetworks
- Prevents co-adaptation: neurons must learn independently useful features

## Where Applied in LLMs
- Attention weights, residual connections, embeddings (p=0.0–0.1 at scale)
- Higher dropout when fine-tuning on small datasets

## Related Concepts
- [[regularization]]
- [[dropout-regularization]]

## Related Entities
- [[geoffrey-hinton]]
- [[ilya-sutskever]]
- [[alex-krizhevsky]]

`Source: raw/dropout-regularization.md`
