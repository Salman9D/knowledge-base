# SplaTAM

**Summary**: Keetha et al. (CMU, 2024) introduce the first dense SLAM system using 3D Gaussian Splatting as the scene representation, achieving photorealistic real-time reconstruction with 0.6cm trajectory accuracy — significantly better than prior dense SLAM methods.

**Sources**: `raw/papers/SplaTAM Splat Track and Map 3D Gaussians for Dense RGB-D SLAM.pdf`

**Last updated**: 2026-04-27

---

## Overview

SplaTAM (**Splat**, **T**rack **a**nd **M**ap) addresses a long-standing tension in SLAM: geometric representations (point clouds, meshes) are accurate but visually coarse; neural representations (NeRF) are photorealistic but slow. 3D Gaussian Splatting (3DGS) offers a third path — photorealistic rendering at high FPS, with a representation that is also directly manipulable.

SplaTAM is the first system to close the loop: it uses 3DGS not just for rendering but as the **persistent map representation** that SLAM updates in real time.

## 3D Gaussian Splatting Primer

A 3D Gaussian Splat represents a scene as a collection of ellipsoidal Gaussians, each with:
- **Position** (mean): where in 3D space
- **Covariance** (shape): orientation and size of the ellipsoid
- **Color** (spherical harmonics): view-dependent appearance
- **Opacity**: transparency

Rendering: project Gaussians into the image plane, alpha-composite in depth order. This is fully differentiable and runs at 30+ FPS on consumer GPUs.

The key property for SLAM: **Gaussians are explicit, editable objects** — unlike NeRF's implicit network weights. You can add, move, or remove individual Gaussians as the map updates.

## SplaTAM Architecture

### Three-Stage Pipeline

**Stage 1: Camera Tracking**
Given a new RGB-D frame, optimize the camera pose (rotation + translation) to best explain the observed depth and color under the current Gaussian map. Uses photometric loss + depth loss over the rendered image.

**Stage 2: Gaussian Densification**
Where the current map fails to explain new observations (high rendering error), new Gaussians are added. SplaTAM uses a **silhouette-guided densification** heuristic: regions where the rendered silhouette mask deviates from the observed depth mask trigger new Gaussian initialization.

**Stage 3: Map Update**
Existing Gaussians are updated (position, color, opacity) by gradient descent on the photometric and depth losses over a sliding window of recent keyframes.

### Key Design Choices

- **RGB-D only** (no IMU, no loop closure yet in v1): simplifies the pipeline
- **Unified representation**: the same Gaussian map used for rendering is the same map used for localization — no separate tracking/mapping threads
- **Keyframe selection**: new keyframes added when camera moves sufficiently or when reconstruction error exceeds threshold

## Results

| Metric | SplaTAM | iMAP | NICE-SLAM | Point-SLAM | MonoGS |
|--------|---------|------|-----------|-----------|--------|
| ATE RMSE (cm) | **0.6** | 5.33 | 1.69 | 0.58 | 0.64 |
| Render FPS | **400** | ~3 | ~1 | ~10 | ~20 |
| Map quality | Photorealistic | Coarse | Structured | Point | Gaussian |

At 400 FPS rendering and 0.6cm ATE RMSE (comparable to Point-SLAM, better than all neural radiance methods), SplaTAM establishes 3DGS as the superior representation for dense SLAM.

**Evaluation datasets**: Replica (synthetic), TUM RGB-D (real), ScanNet (real indoor).

## Why This Matters for Persistent Spatial Memory

The [[slam]] page notes that persistent spatial memory is the central gap for [[spatial-ai-assistant]] systems. SplaTAM changes the calculus on what that memory can store:

| Property | Point Cloud SLAM | 3DGS SplaTAM |
|----------|-----------------|-------------|
| Geometric accuracy | High | High (0.6cm ATE) |
| Visual fidelity | Low | Photorealistic |
| Edit support | Limited | Yes (per-Gaussian) |
| Change detection | Geometric diff | Visual + geometric diff |
| Render speed | Fast | 400 FPS |

A persistent spatial memory layer built on SplaTAM can detect **visual changes** — "the whiteboard has new content since yesterday" — not just geometric changes. This is directly useful for XR training scenarios where the state of a physical environment (surgical setup, emergency scene) changes between sessions.

## Connection to GaussianEditor

SplaTAM handles **capture** (building the 3DGS map from live sensor data). [[gaussianeditor]] handles **editing** (modifying the 3DGS map after capture using text prompts). Together they form a pipeline:

```
Live RGB-D frames
    ↓ SplaTAM
3DGS persistent map
    ↓ GaussianEditor (text-driven)
Modified 3DGS scene
    ↓ Re-render
Updated spatial view
```

This pipeline is directly relevant to 9D Technologies use cases: capture a real training environment, edit it to add/remove elements, re-render for VR training.

## Current Limitations

- **No loop closure** in the original SplaTAM v1 — drift accumulates in large environments
- **No IMU integration** — less robust to fast motion than visual-inertial SLAM
- **Static scenes only** — dynamic objects (people, vehicles) corrupt tracking (see SuperDynaSLAM in [[slam]])
- **Memory footprint** — 3DGS maps are larger than sparse point cloud maps; large environments require compression or selective storage

## Related pages

- [[slam]]
- [[gaussianeditor]]
- [[ego-centric-3d-perception]]
- [[spatial-ai-assistant-architecture]]
- [[conceptfusion]]
- [[xr-trends-research-pipelines]]
