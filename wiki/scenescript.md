# SceneScript

**Summary**: Avetisyan et al. (Meta Reality Labs / Project Aria, Mar 2024) reconstruct 3D scenes as text sequences of structured commands using an autoregressive language model — achieving F1@5cm of 0.903 versus 0.139 for the prior state of the art, with 2–5 second inference that streams directly to VR headsets.

**Sources**: `raw/papers/SceneScript Reconstructing Scenes With An Autoregressive Structured Language Model.pdf`

**Last updated**: 2026-04-27

---

## Overview

SceneScript is the most architecturally distinctive paper in this ingestion batch. It approaches scene reconstruction by asking: **what if we treated a 3D scene as a text document?**

Instead of predicting meshes, voxels, or Gaussian splats, SceneScript outputs a sequence of **structured language commands** that describe the scene. These commands are then executed to reconstruct the geometry. The model is a standard autoregressive transformer — the kind used for language generation — trained on 100K synthetic scenes.

The result is a system that is simultaneously more accurate than geometric reconstruction methods, extensible without retraining, and fast enough to stream to a VR headset in real time.

See [[scene-language-models]] for the broader concept this paper instantiates.

## The Scene Language

SceneScript defines a structured command language for encoding architectural scenes:

```
make_wall(id, a_x, a_y, a_z, b_x, b_y, b_z, height)
make_door(id, wall0_id, wall1_id, position_x, position_y, position_z, width, height)
make_window(id, wall0_id, wall1_id, position_x, position_y, position_z, width, height)
make_bbox(id, class, position_x, position_y, position_z, angle_z, scale_x, scale_y, scale_z)
make_prim(bbox_id, prim_num, class, center_x, center_y, center_z, angle_x, angle_y, angle_z, scale_x, scale_y, scale_z)
```

An entire room is represented as an ordered sequence of these commands:
1. First, structural elements (walls, doors, windows)
2. Then, bounding boxes for each detected object (`make_bbox`)
3. Finally, primitive-level geometry for complex objects (`make_prim`)

This text sequence is a **complete, unambiguous specification** of the scene — it can be parsed and rendered by any standard 3D engine.

### Why Language Sequences Work for 3D Scenes

- **Compositional**: Complex scenes are composed of primitives — the language is naturally compositional
- **Hierarchical**: `make_bbox` (object) → `make_prim` (sub-part) captures object-to-part hierarchy
- **Relational**: `make_door(id, wall0_id, ...)` explicitly encodes which wall the door belongs to — relationships are first-class
- **Discrete + continuous**: Class labels are discrete tokens; spatial coordinates are continuous values, quantized to bins
- **Autoregressive ordering**: Generate walls first (constrain room layout), then objects (conditioned on walls), then parts (conditioned on objects)

## Architecture

### Input

SceneScript processes **point clouds and/or RGB images** from Project Aria smart glasses:
- **Points-only mode**: Sparse depth point cloud from SLAM
- **Lifted features mode**: 2D image features (ViT-derived) lifted into 3D by projecting along depth rays
- **Image-only mode**: No explicit depth; purely visual features

### Model

A standard **transformer encoder-decoder**:
- **Encoder**: Processes the 3D point cloud (or lifted image features) as a set of 3D tokens
- **Decoder**: Autoregressive generation of the command sequence, token by token
- **Tokenization**: Spatial coordinates are quantized into 512 discrete bins per axis; class labels are vocabulary tokens

The model architecture is deliberately unremarkable — no special 3D operators, no graph networks. The contribution is the language representation and training data, not the architecture.

### Training Data: Aria Synthetic Environments

Trained on **100,000 synthetic indoor scenes** from the Aria Synthetic Environments dataset (also publicly released by Meta Reality Labs):

- Procedurally generated room layouts
- Diverse furniture configurations
- Rendered with physically-based lighting
- Ground truth command sequences generated from scene graph specifications

The 100K synthetic scenes are sufficient for strong generalization to real environments — no real-scene fine-tuning was required. This validates the [[synthetic-training-data]] paradigm at the scene reconstruction level.

## Results

### Core Benchmark (Layout Estimation)

| Model | F1@5cm (Lifted Features) | F1@5cm (Points Only) | F1@5cm (Image Only) |
|-------|-------------------------|----------------------|---------------------|
| **SceneScript** | **0.903** | 0.848 | 0.661 |
| RoomFormer | 0.139 | — | — |

The gap is not incremental — 0.903 vs 0.139 is a 6.5× improvement. RoomFormer is the prior state of the art for structured room reconstruction.

### Inference Characteristics

- **Inference time**: 2–5 seconds for a full scene reconstruction
- **Streaming**: Can reconstruct incrementally as new observations arrive; streams directly to an Aria VR headset
- **Extensibility**: Adding a new command type (e.g., `make_stair`) requires only generating more training examples — no architectural changes

### Cross-Modal Results

The performance hierarchy (Lifted Features > Points Only > Image Only) validates the value of fusing depth and appearance — but the image-only result (0.661) is still strong, showing the language model can infer reasonable room layouts from appearance alone.

## Extensibility: The Key Strategic Property

Traditional reconstruction systems are brittle: adding a new object category requires retraining a new detection head. SceneScript's extensibility is qualitatively different:

**Adding a new command type (e.g., `make_electrical_outlet`)**:
1. Define the new command and its parameter schema
2. Generate training examples showing that command in context
3. Fine-tune (or continue training) the existing autoregressive model

The model doesn't need to be redesigned — it's already a sequence model that can accommodate new token types. This is the same way new words are added to a language model's vocabulary.

For 9D Technologies, this means:
- Start with walls/doors/windows/boxes for general environments
- Add healthcare-specific commands (`make_medical_equipment`, `make_patient_bed`) for hospital training scenarios
- Add industrial commands for 9D Technologies' industrial training use cases
- Each extension is a data problem, not an architecture problem

## Connection to Project Aria

SceneScript is built on Meta's **Project Aria** platform:
- **Project Aria**: Research smart glasses with IMU, stereo cameras, and eye tracking
- **Aria Synthetic Environments**: 100K synthetic indoor scenes for training (publicly released)
- The system's output streams to a VR headset in 2–5 seconds — this is a production-targeting demo, not just a benchmark

Project Aria's public release of Aria Synthetic Environments is a significant open-science contribution: any research group can now train SceneScript-style models without building their own synthetic scene pipeline.

## Related pages

- [[scene-language-models]]
- [[ego-centric-3d-perception]]
- [[embodiedscan]]
- [[splatam]]
- [[synthetic-training-data]]
- [[spatial-ai-assistant-architecture]]
- [[xr-hardware]]
- [[xr-trends-research-pipelines]]
