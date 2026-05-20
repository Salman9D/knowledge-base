# 3D-LLM

**Summary**: Hong et al. (UCLA/Microsoft, 2023) introduce a method to inject 3D point cloud representations into large language models, enabling grounded 3D scene understanding across QA, task planning, and navigation.

**Sources**: `raw/papers/3D-LLM Injecting the 3D World into Large Language Models.pdf`

**Last updated**: 2026-04-27

---

## Overview

3D-LLM asks a direct question: can we give LLMs genuine 3D spatial understanding without retraining from scratch? The answer is yes — by using **differentiable rendering** to lift 2D features into 3D and injecting those 3D representations into a frozen language model's embedding space.

The paper establishes both a method and a dataset, and demonstrates that LLMs can be grounded in 3D scenes for a range of tasks that require understanding spatial relationships, object properties, and actionable paths through space.

## The Core Method

### 3D Feature Extraction via gradSLAM

The pipeline begins with RGB-D data and uses **gradSLAM** — a differentiable variant of SLAM — to reconstruct a point cloud with gradient flow. This enables end-to-end learning through the 3D reconstruction.

Key steps:
1. Multi-view RGB-D frames → gradSLAM reconstruction → 3D point cloud
2. 2D features (from CLIP, BLIP-2) are lifted to 3D via point cloud pooling
3. A **3D encoder** converts the point cloud + features into a sequence of tokens
4. These 3D tokens are injected alongside text tokens into the LLM

### 3D Location Tokens

A key innovation: **3D location tokens** are added to the LLM vocabulary. These encode XYZ positions in the scene and can be predicted as outputs — meaning the model can respond to "where is the coffee mug?" by generating a location token, not just a verbal description.

This makes the model actionable for navigation and manipulation planning.

### Supported Tasks

| Task Category | Examples |
|---------------|----------|
| 3D QA | "What color is the chair near the window?" |
| 3D Captioning | Describe the objects in this scene |
| Task Planning | "I need to water the plant — what steps should I take?" |
| Embodied Reasoning | "Which path leads to the exit?" |
| Navigation | Grounded waypoint prediction |

## Dataset: 300K 3D-Language Pairs

A major contribution is the dataset construction pipeline for generating 3D-language pairs at scale:

1. **Source scenes**: ScanNet (RGB-D indoor scans), HM3D and MP3D (synthetic environments)
2. **ChatGPT-powered generation**: Feed scene metadata → GPT-3.5 generates contextually appropriate questions and answers
3. **Scale**: ~300,000 QA pairs across thousands of 3D scenes
4. **Diversity**: QA pairs cover spatial, semantic, navigational, and planning categories

This dataset (3D-LLM-Instruction) was released publicly and has become a benchmark for subsequent 3D-language work.

## Key Results

| Metric | 3D-LLM | Prior Baseline | Improvement |
|--------|--------|---------------|-------------|
| ScanQA BLEU-1 | +9% | Best prior | Significant |
| SQA3D (3D spatial QA) | State of the art (at publication) | — | — |
| Scan2Cap (captioning) | Competitive | — | — |
| 3D task planning | Qualitatively superior | No prior quantitative baseline | — |

The +9% BLEU-1 improvement on ScanQA represents a substantial jump in grounded 3D language understanding.

## Connection to Ego-Centric 3D Perception

3D-LLM operates on pre-built, camera-registered 3D scene reconstructions — it requires a full scene scan to be available. This is different from the **ego-centric, streaming** approach where the model must reason about incomplete 3D data as it accumulates in real time.

The gap between batch-mode 3D-LLM and streaming ego-centric inference is the key challenge for XR deployment. Papers like [[embodiedscan]] (live ego-centric scanning) and [[leo]] (embodied generalist agent) push toward the streaming direction. See [[ego-centric-3d-perception]] for the full landscape.

## Architecture Comparison with LEO

| | 3D-LLM | [[leo]] |
|--|--------|-------|
| **3D input** | Point cloud (pre-built) | Streamed ego-centric views |
| **LLM base** | BLIP-2/OPT or Flamingo variants | Vicuna-7B |
| **Task scope** | Scene QA, captioning, planning | Full embodied task execution |
| **3D encoding** | 3D location tokens via gradSLAM | Viewpoint-dependent perceiver |
| **Action output** | Text/location tokens | Executable actions in embodied env |

3D-LLM establishes the grounding framework; LEO extends it to full embodied agency.

## Implications for Spatial AI Assistant

3D-LLM demonstrates that the [[spatial-ai-assistant-architecture]] recommendation — LLM receives structured spatial context from the scene graph layer — is achievable with existing VLMs. Specifically:

- **3D tokens as context injection** is a proven pattern for grounding LLMs in space
- **ChatGPT-powered dataset generation** provides a template for building domain-specific 3D-language datasets for healthcare or industrial training scenarios
- The 3D location token idea directly informs how a spatial AI assistant could respond with navigation waypoints, not just verbal descriptions

## Related pages

- [[llm-spatial-reasoning]]
- [[spatialvlm]]
- [[leo]]
- [[embodiedscan]]
- [[ego-centric-3d-perception]]
- [[slam]]
- [[spatial-ai-assistant-architecture]]
- [[xr-trends-research-pipelines]]
