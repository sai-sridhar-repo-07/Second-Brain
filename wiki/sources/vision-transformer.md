# Vision Transformer (ViT): An Image is Worth 16x16 Words

Google Research's 2020 paper applying the Transformer architecture directly to images by splitting them into 16×16 patches treated as tokens. Showed pure Transformers match/exceed CNNs at scale and enabled unified vision-language architectures (CLIP, DALL-E, GPT-4V, Claude 3).

## Key Contributions
- Split image into N patches (196 for 224×224) → embed as token sequence
- Standard Transformer encoder + [CLS] token for classification
- No convolutional inductive bias — learns image structure from data
- Outperforms CNNs with sufficient pretraining data (14M+ images)

## Results
- ViT-L/16 on ImageNet: 86.5% top-1 (with ImageNet-21k pretraining)
- Scales better than CNNs: more data + more compute always helps

## Impact
- Enabled CLIP, DALL-E, GPT-4V, Claude 3 vision — unified Transformer for vision+language
- Triggered shift from CNNs to ViT in research and production

## Related Concepts
- [[transformer-architecture]]
- [[self-attention]]
- [[transfer-learning]]

## Related Entities
- [[google-brain]]
- [[ashish-vaswani]]

`Source: raw/vision-transformer-vit.md`
