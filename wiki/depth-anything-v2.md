# Depth Anything V2

**Summary**: Yang et al. (HKU / ByteDance, 2024) build a monocular depth estimation foundation model by training on synthetic data first, using the result to pseudo-label real photos, then distilling into smaller student models — achieving 97.1% δ₁ accuracy versus Marigold's 86.8% with significantly faster inference.

**Sources**: `raw/papers/Depth Anything V2.pdf`

**Last updated**: 2026-04-27

---

## Overview

Depth Anything V2 is a **monocular depth estimation model**: given a single RGB image (no depth sensor, no stereo pair, no SLAM), predict accurate per-pixel depth. This is one of the hardest problems in 3D vision because depth from a single image is geometrically underconstrained — the model must use learned priors about scene structure.

The paper's primary contribution is a **training pipeline** that uses synthetic data to bootstrap labeled real-world data, solving the annotation bottleneck that has historically limited monocular depth models.

## The Annotation Bottleneck Problem

High-quality depth ground truth for real photos requires:
- LiDAR scanners (expensive, outdoor-only at range)
- Structured light sensors (limited range, indoor-only)
- Stereo rigs with precise calibration

All are impractical at the scale needed for a strong foundation model. The standard alternative — using Internet photos with SLAM-estimated pseudo-labels — produces noisy, inconsistent ground truth.

Depth Anything V2 breaks this bottleneck with a three-stage pipeline.

## Three-Stage Training Pipeline

### Stage 1: Train Teacher on Synthetic Data

- **Data**: Large-scale photorealistic synthetic datasets (DA-2K synthetic subset, Hypersim, Virtual KITTI, etc.)
- **Ground truth**: Exact depth from the renderer — perfect, noise-free labels
- **Diversity**: Wide range of indoor/outdoor scenes, lighting conditions, object types
- **Result**: A strong teacher model with reliable depth estimation from synthetic scenes

Synthetic data solves the label quality problem but introduces a domain gap — the model sees perfect CG renders, not real photos.

### Stage 2: Pseudo-Label Real Photos

- **Input**: 62 million unlabeled real photos (web-crawled, diverse)
- **Process**: Run the Stage 1 synthetic-trained teacher on every photo → generate pseudo-depth labels
- **Filtering**: Quality filtering removes frames where teacher confidence is low
- **Result**: 62M real images with (noisy but useful) pseudo-depth labels

The key insight: the synthetic teacher, despite the domain gap, produces pseudo-labels that are more consistent and higher quality than SLAM-based pseudo-labels on the same images. Synthetic training instills strong structural priors that transfer.

### Stage 3: Train Student on Pseudo-Labeled Real Data

- **Data**: 62M real photos with pseudo-labels from Stage 2
- **Architecture variants**: Multiple student sizes — ViT-Small (~24M params) through ViT-Large (~300M params)
- **Training objective**: Distill the teacher's predictions as training signal (scale-invariant loss)
- **Result**: Students inherit the teacher's accuracy on synthetics while learning the photorealistic appearance distribution of real photos

## Key Results

| Model | δ₁ (higher = better) | Inference speed |
|-------|----------------------|-----------------|
| **Depth Anything V2 (Large)** | **97.1%** | ~3 FPS on CPU |
| Depth Anything V1 | 92.6% | Similar |
| Marigold (diffusion-based) | 86.8% | 10–30 sec/image |
| ZoeDepth | 91.2% | ~5 FPS |

δ₁ measures the fraction of pixels where the ratio between predicted and true depth is within 1.25× — the standard benchmark for depth accuracy.

The 97.1% vs 86.8% gap over Marigold (a strong diffusion-based competitor) is substantial, and Depth Anything V2 is orders of magnitude faster than diffusion-based depth models.

## Edge Deployment Variants

| Variant | Params | Target hardware |
|---------|--------|----------------|
| ViT-Small | ~24M | Edge GPU, mobile |
| ViT-Base | ~86M | Mid-range GPU |
| ViT-Large | ~307M | Server inference |

The Small variant is competitive with ViT-Large models from prior generations — the synthetic data pipeline compensates for reduced model capacity.

## Connection to Synthetic Data Strategy

Depth Anything V2 is the clearest example in this paper set of the **synthetic-to-real curriculum** pattern:

```
Synthetic (perfect labels, domain gap)
    ↓ Train teacher
Real unlabeled (no labels, realistic)
    ↓ Pseudo-label via teacher
Real pseudo-labeled (noisy labels, realistic)
    ↓ Train student
Strong model: accurate + realistic
```

This pattern appears across the full paper set. See [[synthetic-training-data]] for the unified analysis including WorldGPT's dream tuning, SpatialVLM's map-derived QA, and SceneScript's Aria Synthetic Environments.

## Implications for XR and Spatial AI

Monocular depth estimation is critical for:

1. **Devices without depth sensors**: Smart glasses (Meta Ray-Ban, Google Gemini glasses) have no LiDAR or structured light — monocular depth from Depth Anything V2 provides the depth channel needed for SLAM and scene understanding
2. **Supplementing sparse sensors**: Vision Pro has LiDAR but limited FOV; Depth Anything fills in depth for the full camera field
3. **Historical frame analysis**: Analyzing recorded video from non-depth-enabled cameras with post-hoc depth estimation

For [[ego-centric-3d-perception]] specifically: a real-time version of Depth Anything V2 Small running on a headset's neural accelerator could replace or supplement the depth sensor for semantic scene reconstruction.

**Key limitation**: Monocular depth estimates are relative, not metric. Without a scale reference (a known object size, a depth anchor from SLAM), the model cannot give absolute distances. For a [[spatial-ai-assistant]] that needs to say "the fire extinguisher is 2.1 meters to your right," metric anchoring is required.

## Related pages

- [[splatam]]
- [[slam]]
- [[synthetic-training-data]]
- [[ego-centric-3d-perception]]
- [[spatialvlm]]
- [[xr-hardware]]
- [[xr-trends-research-pipelines]]
