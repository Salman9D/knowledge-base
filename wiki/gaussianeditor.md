# GaussianEditor

**Summary**: Chen et al. (ETH Zurich / BIT, 2023) enable text-driven editing of 3D scenes represented as Gaussian Splats, using a combination of semantic Gaussian tracing and a novel Hierarchical Gaussian Splatting (HGS) stabilization method, completing in 5–10 minutes per edit.

**Sources**: `raw/papers/GaussianEditor Swift and Controllable 3D Editing based on Gaussian Splatting.pdf`

**Last updated**: 2026-04-27

---

## Overview

GaussianEditor is the **editing counterpart** to [[splatam]]. Where SplaTAM captures a scene as a 3D Gaussian Splat map, GaussianEditor modifies that map using natural language prompts — "make the wall blue," "remove the chair," "add a window." Together they form a complete pipeline for capturing, persisting, and intentionally modifying 3D environments.

The paper solves two hard problems in 3DGS editing:
1. **Localization**: Which Gaussians belong to the target object/region?
2. **Stability**: How to prevent neighboring Gaussians from being corrupted during editing?

## Technical Contributions

### 1. Gaussian Semantic Tracing

Existing 3DGS scenes have no concept of object identity — each Gaussian is independent, and objects are only implied by spatial proximity. GaussianEditor assigns **semantic IDs** to Gaussians:

1. **User specifies target**: text prompt ("the chair") or segmentation mask
2. **2D segmentation**: Run Grounded SAM (GroundingDINO + SAM) on rendered views to get 2D masks of the target
3. **3D propagation**: Project 2D masks into 3D using the camera model to tag which Gaussians correspond to the target region
4. **Iterative refinement**: Re-render from multiple viewpoints, re-run segmentation, accumulate IDs — handles the view-dependence problem

Result: every Gaussian in the scene carries a `semantic_id` indicating what object (if any) it belongs to. Editing operations are then applied only to the tagged Gaussians.

### 2. Hierarchical Gaussian Splatting (HGS)

During editing, a standard 3DGS optimizer will propagate changes beyond the target region — editing a chair slightly degrades the floor behind it, for example. HGS prevents this:

- **Anchor Gaussians**: Gaussians not tagged to the edit target are frozen with strong regularization anchors
- **Edit Gaussians**: Tagged Gaussians are free to change position, color, opacity, and shape
- **Hierarchy**: The editing process uses a coarse-to-fine scheme, starting with large positional moves and refining to detailed appearance changes

This two-tier system lets the optimizer focus editing energy on the target while preserving the surrounding scene geometry.

### 3. 2D Diffusion as Edit Signal

Once the target Gaussians are isolated, the edit guidance comes from a **2D diffusion model** (InstructPix2Pix or similar instruction-following diffusion):

1. Render the current 3DGS scene from a viewpoint
2. Apply the text instruction to the 2D rendered image via diffusion editing
3. Use the edited 2D image as a supervision signal for the 3D Gaussian update
4. Repeat from many viewpoints, accumulating consistent 3D updates

This leverages the full power of 2D generative models (trained on massive 2D datasets) to guide 3D edits — without needing 3D training data for the editing process itself.

## Results

| Metric | GaussianEditor | NeRF-based editors (Instruct-NeRF2NeRF) |
|--------|---------------|----------------------------------------|
| Edit time | **5–10 minutes** | 45–90 minutes |
| Localization control | High (Gaussian semantic tracing) | Low (global optimization) |
| Neighboring region preservation | High (HGS anchors) | Low |
| Scene fidelity | Photorealistic (3DGS) | Lower quality |

The 5–10× speedup over NeRF-based editing comes from the explicit Gaussian representation — updates are local and parallelizable rather than a global network refit.

## Supported Edit Types

| Edit Type | Example |
|-----------|---------|
| Appearance change | "Make the chair red" |
| Object removal | "Remove the table" |
| Style transfer | "Make the room look medieval" |
| Object replacement | "Replace the lamp with a modern one" |
| Texture modification | "Add graffiti to the wall" |

## Integration with SplaTAM

The natural pipeline:

```
SplaTAM (capture + persistent map)
    ↓ 3DGS scene file
GaussianEditor (text-driven modification)
    ↓ Modified 3DGS scene
Re-render for VR/AR headset
```

For 9D Technologies' training scenarios:
- Capture a real OR, emergency room, or industrial site with SplaTAM
- Use GaussianEditor to add/remove equipment, change configurations, introduce hazards
- Render the modified environment for training scenarios in VR
- Iterate in 5–10 minutes per modification — viable for instructors to prepare scenarios

## Current Limitations

- **Not real-time**: 5–10 minutes per edit is practical for content creation, not interactive editing
- **2D diffusion artifacts**: multi-view consistency of diffusion edits is imperfect — visible seams can appear
- **Deletion stability**: removing objects leaves gaps that must be inpainted; quality varies
- **Large structural changes**: adding entirely new rooms or changing global geometry is not supported

## Related pages

- [[splatam]]
- [[slam]]
- [[scenescript]]
- [[synthetic-training-data]]
- [[spatial-ai-assistant-architecture]]
- [[xr-simulations-training]]
- [[xr-trends-research-pipelines]]
