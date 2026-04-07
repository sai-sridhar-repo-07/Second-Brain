# AlexNet: ImageNet Classification with Deep Convolutional Neural Networks

University of Toronto's 2012 paper that started the deep learning revolution. Won ImageNet 2012 by an 11-point margin, proving deep CNNs could scale, and triggered the shift from hand-crafted features to learned representations.

## Key Contributions
- First major CNN trained on GPUs (2× GTX 580)
- ReLU activations — non-saturating, 6× faster than tanh
- Dropout for regularization in fully connected layers
- Data augmentation (random crops, horizontal flips, PCA color)
- 5 conv + 3 FC layers, ~60M parameters

## Results
- ILSVRC 2012: 15.3% top-5 error vs 26.2% (2nd place) — unprecedented margin
- Triggered a decade of rapid architecture improvements

## Related Concepts
- [[convolutional-neural-networks]]
- [[transfer-learning]]
- [[dropout-regularization]]

## Related Entities
- [[geoffrey-hinton]]
- [[ilya-sutskever]]
- [[alex-krizhevsky]]

`Source: raw/alexnet-imagenet-classification.md`
