# Knowledge Base Index

Last Updated: 2026-04-07

## Sources
- [[attention-is-all-you-need]] - 2017 paper introducing the Transformer architecture
- [[bert]] - 2018 bidirectional pre-training; the pre-train → fine-tune paradigm
- [[gpt3]] - 2020 175B model; introduced in-context / few-shot learning
- [[resnet]] - 2015 residual connections; enabled very deep networks
- [[alexnet]] - 2012 deep CNN that started the deep learning revolution
- [[diffusion-models]] - 2020 DDPM; foundation of Stable Diffusion and all modern image generation
- [[adam-optimizer]] - 2014 adaptive optimizer; standard for all LLM training (AdamW)
- [[batch-normalization]] - 2015 normalizing CNN layer inputs; accelerated training
- [[dropout]] - 2014 regularization via random neuron zeroing
- [[layer-normalization]] - 2016 per-sample feature normalization; standard in Transformers
- [[lora]] - 2021 low-rank adapters for efficient fine-tuning; dominant PEFT method
- [[constitutional-ai]] - 2022 Anthropic; RLAIF for harmlessness; how Claude is trained
- [[chain-of-thought]] - 2022 step-by-step reasoning in prompts; foundation of modern prompting
- [[rag]] - 2020 retrieval + generation; most deployed production AI pattern
- [[mixture-of-experts]] - 2022 sparse activation; trillion-parameter models at constant compute
- [[flash-attention]] - 2022 IO-aware attention; 2-4× faster, enables long context windows
- [[word2vec]] - 2013 dense word vectors; foundation of all modern embeddings
- [[gan]] - 2014 adversarial generative model; superseded by diffusion for image generation
- [[alphago-alphazero]] - 2016-2018 superhuman game play via RL + self-play
- [[vision-transformer]] - 2020 Transformer applied to images; enabled CLIP, GPT-4V, Claude vision
- [[scaling-laws]] - 2020 power laws for LLM training; Chinchilla revised to 20 tokens/param

## Entities
- [[ashish-vaswani]] - Lead author of the Transformer paper
- [[noam-shazeer]] - Co-inventor of Transformer; co-founded Character.AI
- [[aidan-gomez]] - Transformer co-author; co-founded Cohere
- [[google-brain]] - Lab behind Transformers, BERT precursors, Batch Norm
- [[jacob-devlin]] - Lead author of BERT
- [[google-ai]] - Google AI Language; created BERT and T5
- [[ilya-sutskever]] - AlexNet co-author; OpenAI co-founder
- [[dario-amodei]] - GPT-3 co-author; co-founded Anthropic (CEO)
- [[openai]] - Created GPT-3, GPT-4, ChatGPT, Scaling Laws
- [[anthropic]] - Created Claude; introduced Constitutional AI / RLAIF
- [[jared-kaplan]] - Scaling Laws lead author; co-founded Anthropic
- [[geoffrey-hinton]] - Godfather of Deep Learning; AlexNet, Dropout, LayerNorm
- [[alex-krizhevsky]] - AlexNet creator; named the network
- [[kaiming-he]] - ResNet creator; residual connections
- [[microsoft-research]] - Created ResNet (2015) and LoRA (2021)
- [[jonathan-ho]] - DDPM lead author; classifier-free guidance
- [[uc-berkeley]] - BAIR lab; home of DDPM and RL research
- [[diederik-kingma]] - Co-invented Adam optimizer and VAEs
- [[jimmy-ba]] - Co-authored Adam and Layer Normalization
- [[deepmind]] - Created AlphaGo, AlphaFold, Gemini; Chinchilla laws
- [[demis-hassabis]] - DeepMind CEO; Turing Award 2024
- [[tri-dao]] - FlashAttention creator; Stanford PhD
- [[stanford-university]] - Academic home of FlashAttention
- [[tomas-mikolov]] - Word2Vec creator
- [[facebook-ai-research]] - Created RAG, RoBERTa, LLaMA
- [[ian-goodfellow]] - GAN inventor
- [[yoshua-bengio]] - Godfather of Deep Learning; Turing Award 2018
- [[jason-wei]] - Chain-of-Thought lead author
- [[christian-szegedy]] - Batch Norm co-author; GoogLeNet architect

## Concepts
- [[self-attention]] - Tokens attending to all other tokens directly
- [[multi-head-attention]] - Parallel attention across multiple learned subspaces
- [[transformer-architecture]] - Full architecture built on attention only
- [[positional-encoding]] - Injecting token order into attention-based models
- [[encoder-decoder]] - Input encoder + autoregressive output decoder pattern
- [[pre-training-and-fine-tuning]] - Train large on general data, adapt to specific task
- [[in-context-learning]] - Task adaptation via prompt examples, no weight updates
- [[scaling-laws]] - Power laws relating loss to parameters, data, compute
- [[retrieval-augmented-generation]] - Grounding LLM generation in retrieved documents
- [[rlhf-and-rlaif]] - Training alignment from human or AI preference feedback
- [[parameter-efficient-fine-tuning]] - Fine-tuning with small trainable adapters (LoRA, QLoRA)
- [[normalization-techniques]] - BatchNorm, LayerNorm, RMSNorm comparison
- [[residual-connections]] - Skip connections enabling deep network training
- [[vector-embeddings]] - Dense representations for semantic similarity and retrieval
- [[generative-models]] - GANs, diffusion, autoregressive models compared
- [[transfer-learning]] - Using pre-trained features for new tasks
- [[reinforcement-learning]] - Learning from reward signals; self-play; RLHF
- [[optimization-algorithms]] - Adam, AdamW, SGD — optimizer comparison

## Synthesis
*No synthesis pages created yet*

## Statistics
- Total Sources: 21
- Total Entities: 29
- Total Concepts: 18
- Total Synthesis Pages: 0
