# Mixture of Experts for Transformers

Google Brain's Switch Transformers (2022) and GShard (2021) papers introducing sparse MoE Transformer layers — replacing dense feed-forward layers with N expert networks, activating only top-k per token. Enables trillion-parameter models at constant compute cost. Used in GPT-4 (rumored), Mixtral, Grok.

## Key Contributions
- Replace FFN with N experts + router; each token activates only k=1–2 experts
- Switch Transformer: Top-1 routing — simplest and most efficient
- Load balancing loss prevents routing collapse (all tokens to same expert)
- Expert capacity: limits tokens per expert to handle overflow
- 1.6T parameter Switch Transformer at T5-XXL compute budget

## Results
- 7× speedup vs T5-XXL (11B dense) at same compute
- Scaling: more experts always helps up to 2,048 experts

## Related Concepts
- [[sparse-activation]]
- [[transformer-architecture]]
- [[scaling-laws]]

## Related Entities
- [[google-brain]]
- [[noam-shazeer]]

`Source: raw/mixture-of-experts.md`
