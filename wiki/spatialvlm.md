# SpatialVLM

**Summary**: Google DeepMind paper demonstrating that spatial reasoning in vision-language models is primarily a data problem, solved by generating 2 billion synthetic spatial QA pairs from web-scale map data rather than changing model architecture.

**Sources**: `raw/papers/SpatialVLM Endowing Vision-Language Models with Spatial Reasoning Capabilities.pdf`

**Last updated**: 2026-04-27

---

## Overview

SpatialVLM (Chen et al., Google DeepMind, 2024) is a vision-language model fine-tuned specifically for quantitative spatial reasoning — tasks like "how far is the chair from the table?" or "which object is closer to the left wall?" The core contribution is the training pipeline, not the model architecture.

The central thesis: **spatial reasoning is a data scarcity problem, not an architecture problem**. Standard VLM training datasets contain abundant language and 2D semantic understanding, but almost no examples of precise metric spatial relationships between objects. SpatialVLM constructs this data synthetically at scale.

## Synthetic Spatial VQA Pipeline

The data generation pipeline is the paper's primary contribution:

1. **Source**: Web-scale map data (Google Maps satellite imagery with known metric ground truth)
2. **Object detection**: Identify objects and their metric positions
3. **QA generation**: Automatically generate spatial questions at three levels:
   - **Qualitative** ("is the chair to the left or right of the table?")
   - **Quantitative metric** ("how many meters from the chair to the desk?")
   - **Comparative** ("which is closer: the door or the window?")
4. **Scale**: 2 billion spatial VQA pairs total

The synthetic pipeline avoids the central bottleneck of spatial datasets: human annotation of 3D spatial relationships is slow, expensive, and error-prone. By anchoring to map data with known coordinates, ground truth is derived automatically.

## Key Results

| Task | SpatialVLM | GPT-4V | Baseline VLM |
|------|-----------|--------|-------------|
| Spatial distance estimation | **75.2%** | 68% | ~40% |
| Qualitative spatial QA | Outperforms | — | Significant margin |
| Chain-of-thought spatial reasoning | Enabled | Limited | Not applicable |

The model also enables **chain-of-thought spatial reasoning** — multi-step spatial inference that smaller or less-trained models cannot perform.

## Training Setup

- Base model: 2B parameter VLM (not publicly named in full detail)
- Fine-tuning: Standard instruction tuning on synthetic spatial QA pairs
- No architecture changes required — pure data-driven improvement

## Connection to Broader Synthetic Data Theme

SpatialVLM is one of four papers in this ingestion batch that demonstrate the synthetic data unlock pattern:

| Paper | Synthetic Data Source | Performance Gap Closed |
|-------|----------------------|----------------------|
| **SpatialVLM** | Web-scale map data → 2B spatial QA pairs | 75.2% vs GPT-4V 68% on spatial distance |
| [[depth-anything-v2]] | Synthetic renderer → pseudo-label real data | 97.1% vs Marigold 86.8% δ₁ |
| [[scenescript]] | Aria Synthetic Environments (100K scenes) | F1 0.903 vs 0.139 for RoomFormer |
| [[worldgpt]] | Dream tuning (WorldGPT self-generation) | Synthetic ≈ real at 30× lower cost |

See [[synthetic-training-data]] for the full cross-paper analysis of this pattern.

## Implications for Imagination AI / 9D Technologies

SpatialVLM is a direct template for filling the spatial reasoning gap identified in [[llm-spatial-reasoning]]:

1. **The gap is fillable via data, not novel architecture** — 9D Technologies could fine-tune an open VLM on a domain-specific spatial QA dataset (XR scenes, surgical environments, training scenarios) without waiting for architectural breakthroughs.

2. **XR-specific spatial QA data is generatable** — Using SLAM outputs, scene graphs, and known metrics from Quest 3 or Vision Pro, a similar pipeline could generate XR-specific spatial training data.

3. **Chain-of-thought spatial reasoning** — Once fine-tuned, the model can reason over multiple spatial relationships in sequence, enabling the "what is near me that I haven't seen recently" class of queries that a [[spatial-ai-assistant]] needs.

**Caveat**: SpatialVLM is a 2D → metric reasoning model; it doesn't directly solve 3D ego-centric perception. For 3D understanding, see [[3d-llm]] and [[embodiedscan]]. See also [[ego-centric-3d-perception]] for the broader paradigm.

## Related pages

- [[llm-spatial-reasoning]]
- [[3d-llm]]
- [[synthetic-training-data]]
- [[ego-centric-3d-perception]]
- [[spatial-ai-assistant]]
- [[xr-trends-research-pipelines]]
