# ConceptFusion

**Summary**: Jatavallabhula et al. (MIT/CMU, 2023) build open-set 3D maps queryable by any modality — text, image, audio, or click — without task-specific training, achieving >40% mIoU over prior semantic mapping methods.

**Sources**: `raw/papers/ConceptFusion Open-set Multimodal 3D Mapping.pdf`

**Last updated**: 2026-04-27

---

## Overview

ConceptFusion answers a critical question for [[spatial-ai-assistant]] systems: how do you build a 3D map of a real environment that a language model can query in natural language — without retraining for every new environment?

The answer: fuse **pixel-level foundation model features** (CLIP, DINO) into a 3D point cloud map during construction, so that the semantic meaning of every 3D point is encoded at map-build time. The result is a scene that the agent can query at inference time using any modality — zero-shot.

## Architecture

### Building the Semantic 3D Map

ConceptFusion extends **standard RGB-D SLAM** (or NeRF/3DGS as the geometry backbone) with a feature fusion pipeline:

1. **Geometry first**: Build a standard geometric map from RGB-D frames (point cloud or mesh)
2. **CLIP features per pixel**: For each frame, run CLIP to get per-pixel semantic embeddings
3. **DINO features per pixel**: Run DINO (self-supervised ViT) for local, object-part-level features
4. **SAM masks**: Use Segment Anything to get clean object boundaries for each frame
5. **Fusion into 3D**: Project per-pixel features into the 3D map; accumulate and average features at each 3D point across all observed views

The result: a 3D point cloud where every point carries a multi-model semantic embedding vector (CLIP + DINO + region-level features).

### Querying the Map

Once the map is built, ConceptFusion supports **any-modality queries** at inference time without additional training:

| Query Type | Example | Method |
|-----------|---------|--------|
| Text | "Where is the coffee mug?" | Cosine similarity between CLIP text embedding and point CLIP features |
| Image crop | Photo of a specific object | CLIP image embedding → cosine similarity to map |
| Audio | Sound clip of running water | AudioCLIP embedding → cosine similarity |
| Click | User clicks on a rendered view | Project click ray into 3D → use DINO local features to find similar regions |

All queries return a **relevance heatmap** over the 3D scene — the points most semantically similar to the query are highlighted.

## Key Results

| Method | mIoU | Notes |
|--------|------|-------|
| ConceptFusion | **>40% better** | Zero-shot, no task-specific training |
| LSeg | Baseline | Task-specific language-segmentation model |
| OpenSeg | Baseline | Open-vocabulary 3D segmentation |

The key comparison is zero-shot (ConceptFusion) vs. trained-for-task (LSeg, OpenSeg). ConceptFusion wins by >40% mIoU while requiring no environment-specific or task-specific training — a qualitative shift in how semantic 3D maps can be built.

## The "Open-Set" Property

"Open-set" means the system can recognize and localize any concept a foundation model understands — not just the categories it was trained on. This is critical for real-world XR deployment where:

- New objects appear without notice (user brings new device to workspace)
- Domain-specific objects are not in any training set (specialized surgical instrument, industrial component)
- Natural language queries are unpredictable ("where did I put the thing that scans barcodes?")

ConceptFusion handles all of these because its semantic understanding comes from CLIP/DINO (trained on web scale), not from a fixed class taxonomy.

## Connection to Ego-Centric Perception

ConceptFusion, as published, operates on pre-built point cloud maps. The **ego-centric extension** — building and querying the semantic 3D map from a streaming first-person video feed — is the direction that [[embodiedscan]] and [[leo]] push. See [[ego-centric-3d-perception]] for the unified picture.

For real-time XR deployment, the question becomes: can ConceptFusion-style feature fusion run at interactive rates on an embedded device? The CLIP/DINO inference per frame is the compute bottleneck; distilled/quantized variants are an active research direction.

## Implications for Spatial AI Assistant

ConceptFusion is a near-complete answer to the semantic layer of a spatial AI assistant's perception stack:

```
RGB-D SLAM (geometry)  +  ConceptFusion (semantics)
    ↓
Persistent spatial map: every point has position + meaning
    ↓
Any-modality query: "show me everything made of glass"
    ↓
Localized 3D region highlighted in AR overlay
```

For 9D Technologies' healthcare training use case: a ConceptFusion map of an OR would allow trainees to query "where is the electrosurgical unit?" or search by image of an instrument they don't know the name of.

**Integration path with SplaTAM**: SplaTAM provides the photorealistic 3DGS geometry; ConceptFusion's feature fusion could be applied to the 3DGS map rather than a point cloud. This combination is not in either paper but is an obvious next step.

## Relationship to Other Open-Source Models

| Model | Role | Notes |
|-------|------|-------|
| [[open-source-scene-understanding]] (SAM, GroundingDINO, YOLO-World) | Object detection/segmentation | ConceptFusion uses SAM as a component |
| ConceptFusion | Semantic 3D mapping | Uses CLIP + DINO + SAM together |
| [[splatam]] | Geometric 3D mapping | Complements ConceptFusion's semantics with photorealistic geometry |

## Related pages

- [[slam]]
- [[splatam]]
- [[embodiedscan]]
- [[ego-centric-3d-perception]]
- [[open-source-scene-understanding]]
- [[spatial-ai-assistant-architecture]]
- [[xr-trends-research-pipelines]]
