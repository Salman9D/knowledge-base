# EmbodiedScan

**Summary**: Wang et al. (Shanghai AI Lab, Dec 2023) introduce a large-scale multi-modal ego-centric 3D perception dataset and benchmark with 5K+ scans, 1M language prompts, 160K 3D bounding boxes, and 760+ object categories — establishing the data infrastructure for the next generation of embodied spatial AI.

**Sources**: `raw/papers/EmbodiedScan A Holistic Multi-Modal 3D Perception Suite Towards Embodied AI.pdf`

**Last updated**: 2026-04-27

---

## Overview

EmbodiedScan is a **dataset and benchmark** paper — its contribution is infrastructure, not a novel model. But infrastructure is often the bottleneck, and EmbodiedScan removes a critical one: there was no large-scale, ego-centric, language-annotated 3D perception benchmark for training the kind of embodied AI models that [[leo]], [[3d-llm]], and spatial AI assistants need.

The paper also introduces the **Embodied Perceptron** baseline model, which establishes performance numbers to beat.

## Dataset Statistics

| Property | EmbodiedScan | ScanNet (prior standard) |
|----------|-------------|--------------------------|
| Indoor scans | 5,765 | 1,513 |
| RGB-D views | 1,000,000+ | ~2.5M (total frames) |
| Language prompts | 1,000,000+ | Limited |
| 3D bounding boxes (oriented) | 160,000+ | ~250K (axis-aligned) |
| Object categories | **760+** | **18** |
| Ego-centric viewpoints | Yes (continuous) | Per-frame, not ego-centric |
| Multi-modal | RGB + Depth + Language | RGB + Depth only |

The 760+ category count versus ScanNet's 18 is the headline number: EmbodiedScan represents a 40× expansion in semantic vocabulary, enabling models to learn "long-tail" object recognition that sparse commercial category lists miss.

## Data Collection and Annotation

### Source Datasets

EmbodiedScan aggregates and extends three existing RGB-D indoor scan sources:
- **ScanNet** (1,513 scans) — the current standard benchmark
- **3RScan** (1,482 scans) — re-scans of the same scenes over time
- **HM3D** (2,770 scans) — large-scale Habitat-Matterport dataset

Rather than recollecting data, the team develops a unified annotation pipeline that elevates all three datasets to EmbodiedScan's richer annotation format.

### SAM-Assisted Annotation Pipeline

Manual annotation of 160K+ 3D bounding boxes across 760+ categories would be impractical. The team uses **Segment Anything Model (SAM)** to accelerate:

1. SAM generates 2D segmentation masks across all RGB frames
2. Masks are projected into 3D using depth and camera calibration
3. 3D object instances are assembled from multi-view 2D masks
4. Human annotators verify and label — but the segmentation workspace is already done

SAM reduces annotation time by an estimated 5–8× compared to manual 3D box drawing from scratch.

### Language Prompts

The 1M language prompts cover:
- **Object grounding**: "Find the wooden table next to the window" → 3D box
- **Spatial QA**: "Is the chair to the left or right of the desk?"
- **Navigation description**: "Walk toward the door, which is behind the sofa"
- **Object description**: "Describe the objects in front of you"

Language prompts are generated via a combination of template-based generation and GPT-4 rewriting for natural language diversity.

## Embodied Perceptron: The Baseline Model

The paper introduces Embodied Perceptron as a multi-modal baseline that processes:
- **Ego-centric RGB frames** (sequential, first-person viewpoint)
- **Depth maps** from each frame
- **Language queries**

Architecture:
- Image encoder: ViT-based visual backbone
- Depth encoder: lightweight depth feature extractor
- Cross-modal fusion: multi-head attention over image + depth + language tokens
- 3D detection head: predicts oriented 3D bounding boxes in the ego-centric reference frame

The Embodied Perceptron establishes baseline numbers on EmbodiedScan's benchmark tasks.

## Key Experimental Findings

### Real Capture Beats Rendering

The most practically significant result: models trained on **real RGB-D captures** outperform models trained on **rendered synthetic frames** from the same scenes by ~**6% AP** (average precision).

This is a significant finding because rendering is cheap and controllable — if it matched real capture in training value, the pipeline to large-scale training data would be much simpler. The 6% gap means real data remains important, and the community needs real scanning infrastructure like EmbodiedScan.

**Caveat from cross-paper analysis**: This appears to contradict [[depth-anything-v2]] and [[worldgpt]]'s finding that synthetic data is sufficient. The reconciliation: EmbodiedScan's gap is about *photorealistic appearance* (real textures, real lighting) — categories where synthetic rendering still falls short. SpatialVLM and WorldGPT use synthetic data for *relational and semantic* properties (positions, states, transitions) where the domain gap is smaller.

### Linear Scaling with Scan Count

Model performance scales near-linearly with the number of training scans. There is no evidence of saturation at 5K scans — EmbodiedScan is not yet the ceiling. This means more real-world scanning data will continue to improve embodied perception models.

### Long-Tail Categories Require Full Dataset

Models trained on the full 760+-category vocabulary significantly outperform models trained on filtered common-category subsets — confirming that the long tail is important, not just a labeling exercise.

## Benchmark Tasks

EmbodiedScan defines three primary benchmark tracks:

| Task | Input | Output | Metric |
|------|-------|--------|--------|
| 3D Visual Grounding | Language + ego-centric scan | 3D oriented bounding box | AP@25/50 |
| 3D Dense Captioning | Ego-centric scan | Text descriptions of visible objects | METEOR, CIDEr |
| Multi-Target Grounding | Language (multiple objects) | Multiple 3D boxes | Group AP |

## Implications for Spatial AI

EmbodiedScan is the training data foundation that practitioners need to build the next generation of ego-centric spatial AI models:

1. **Vocabulary gap closed**: Prior models trained on ScanNet's 18 categories fail in the wild (everything outside those 18 categories is invisible). EmbodiedScan's 760+ categories approaches real-world deployment richness.

2. **Ego-centric benchmark is the right framing**: Spatial AI assistants receive streaming ego-centric input, not pre-built scans. EmbodiedScan's streaming viewpoint design matches deployment reality.

3. **SAM-assisted annotation is replicable**: For 9D Technologies building domain-specific datasets (surgical equipment, industrial environments), the SAM-accelerated annotation pipeline can be applied to custom RGB-D captures.

4. **Scaling signal**: The near-linear scaling result means that investment in real-world data capture (scanning clinical environments, training spaces) has predictable returns.

## Related pages

- [[ego-centric-3d-perception]]
- [[leo]]
- [[3d-llm]]
- [[conceptfusion]]
- [[scenescript]]
- [[slam]]
- [[synthetic-training-data]]
- [[xr-trends-research-pipelines]]
