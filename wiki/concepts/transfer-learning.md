# Transfer Learning

Transfer learning is the practice of using a model trained on one task as the starting point for a different (but related) task. In deep learning, it typically means using a model pre-trained on a large dataset and adapting it to a downstream task with less data and compute.

## How Sources Explain This
- **[[alexnet]]**: AlexNet features trained on ImageNet could be transferred to other vision tasks — early demonstration of transfer learning's power in deep learning.
- **[[resnet]]**: ResNet weights pre-trained on ImageNet are universally used as backbone for detection, segmentation, and other vision tasks.
- **[[bert]]**: BERT formalized the pre-train → fine-tune paradigm for NLP. One pre-trained model → SOTA on 11 different tasks with small task-specific fine-tuning.
- **[[vision-transformer]]**: ViT scales better than CNNs with more pre-training data — the more powerful the pre-training, the more valuable the transfer.

## Contradictions or Variations
- Fine-tuning (update all weights) vs PEFT/LoRA (update small adapters) vs in-context learning (no updates)
- Domain mismatch can hurt: pre-training on general web text may not transfer well to medical/legal domains without domain-specific pre-training

## Related Concepts
- [[pre-training-and-fine-tuning]]
- [[parameter-efficient-fine-tuning]]
- [[in-context-learning]]
