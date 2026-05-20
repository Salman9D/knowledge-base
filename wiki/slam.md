# SLAM

**Summary**: Explains Simultaneous Localization and Mapping (SLAM) as the foundational technology for spatial understanding in XR, covering how it works, key variants, and its role in enabling a Spatial AI Assistant.

**Sources**: `AR_VR_Hardware_Market_Analysis_Spatial_Mapping_Technologies_Report_1.1_.docx.pdf`, `Spatial_AI_Assistant_Report_2.1.docx.pdf`, `Scene_Understanding_Object_Recognition_Landscape_2026-04-21.md`, `Durrant-Whyte_Bailey_SLAM-tutorial-I.pdf`, `s41598-026-46629-0_reference.pdf`, `Key Trends & Research Pipelines.pdf` (9D Technologies AI Research)

**Last updated**: 2026-04-24

---

## What Is SLAM?

SLAM — Simultaneous Localization and Mapping — is the computational problem of building a map of an unknown environment while simultaneously tracking the device's location within that map.

For XR, SLAM answers two questions at once:
1. **Where am I?** (localization)
2. **What does the space look like?** (mapping)

Both questions must be solved simultaneously because each depends on the other — you need a map to localize, and you need to know your position to build an accurate map.

## Why SLAM Matters for Spatial AI

SLAM is the foundational technology that makes the following possible:

- **Persistent spatial memory**: Remembering where objects are across sessions requires a stable map of the environment. Without SLAM, every session starts with a blank spatial slate.
- **Accurate AR overlay**: Placing virtual objects in the physical world requires knowing exactly where surfaces, walls, and objects are.
- **Real-time spatial reasoning**: A [[spatial-ai-assistant]] must continuously track both the environment and its own position to provide contextually relevant assistance.
- **Multi-device collaboration**: Shared spatial experiences (collaborative AR) require all devices to agree on the same spatial map.

## How SLAM Works

### The Basic Loop

1. **Sensor input**: Camera(s) capture frames; IMU measures acceleration and rotation; depth sensors (LiDAR, structured light) measure distances
2. **Feature extraction**: Identify distinctive visual features (corners, edges, textures) in each frame
3. **Data association**: Match features between frames to track motion
4. **Pose estimation**: Calculate how the device has moved since the last frame
5. **Map update**: Add new observations to the spatial map; correct previous estimates using the new data
6. **Loop closure**: When the device returns to a previously mapped area, recognize it and correct accumulated drift

### The Drift Problem

SLAM systems accumulate small errors over time. Each pose estimate has a tiny error, and these errors compound — causing the map to "drift" from reality. Loop closure (recognizing previously seen places) is the primary mechanism for correcting drift.

## Algorithmic Foundations

The canonical academic treatment of SLAM is Durrant-Whyte & Bailey (IEEE, 2006), which defines the problem in probabilistic form and describes the two primary solution classes. (source: `Durrant-Whyte_Bailey_SLAM-tutorial-I.pdf`)

### Probabilistic Formulation

SLAM requires computing the joint posterior distribution:

**P(x_k, m | Z₀:k, U₀:k, x₀)**

— the probability over robot pose `x_k` and full landmark map `m`, given all observations `Z₀:k` and control inputs `U₀:k` up to time k. The algorithm runs as a recursive two-step loop: **time-update** (predict next state from motion model) and **measurement-update** (correct using Bayes' theorem given new observations).

**Key insight — convergence**: The correlations between landmark estimates grow monotonically as more observations are made. This means the relative position between any two landmarks always becomes more accurate over time, regardless of robot motion. The map converges; it does not random-walk. This was the conceptual breakthrough that made SLAM tractable.

### EKF-SLAM

Extended Kalman Filter SLAM maintains a joint mean and covariance over the robot pose and all landmark positions.

- **Strengths**: Well-understood, convergence guaranteed in linear Gaussian case
- **Weaknesses**: Computation scales quadratically with number of landmarks; fragile to incorrect data association (wrong landmark matches); linearisation errors can cause inconsistency in highly non-linear systems
- **Loop closure**: When the robot revisits a known area, EKF-SLAM can recognize landmarks and correct accumulated drift — but the "loop closure" data association problem is particularly hard

### FastSLAM (Rao-Blackwellised Particle Filter)

FastSLAM factors the SLAM state into a vehicle trajectory (sampled via particle filter) and per-landmark Gaussians (computed analytically given each trajectory). Because landmarks are independent given the trajectory, each particle carries its own map — giving **linear complexity** in the number of landmarks.

- **FastSLAM 1.0**: Uses the motion model as the proposal distribution
- **FastSLAM 2.0**: Incorporates current observations into the proposal — locally optimal, far more efficient
- **Weakness**: Statistical degeneration over time as particle diversity is lost through resampling; cannot "forget the past"

### Open-Source SLAM Implementations

The tutorial documents several open reference implementations:

| Implementation | Language | Notes |
|----------------|----------|-------|
| Tim Bailey's simulator | MATLAB | EKF-SLAM, UKF-SLAM, FastSLAM 1.0 & 2.0 |
| Andrew Davison's Scene | C++ | Real-time single-camera SLAM |
| Mark Paskin's library | Java | Kalman filter, information filter, thin junction tree |
| Dirk Hähnel's FastSLAM | C | Grid-based |

Public benchmark datasets: Victoria Park (outdoor, GPS ground truth), Radish repository (indoor), IJRR archive.

## SLAM Variants

### Visual SLAM (vSLAM)
- Uses only cameras (monocular, stereo, or RGB-D)
- Most common in XR headsets due to low cost and power
- Examples: ORB-SLAM3, LSD-SLAM, Meta's scene understanding in Quest 3
- Limitation: scale ambiguity in monocular systems; struggles in textureless or highly dynamic environments

### LiDAR SLAM
- Uses laser point clouds for mapping
- Higher accuracy and range than visual SLAM
- Used in: autonomous vehicles, industrial robotics, Apple Vision Pro (short-range)
- Limitation: expensive hardware; power-hungry

### Inertial-Visual SLAM (VI-SLAM)
- Fuses camera data with IMU (accelerometer + gyroscope)
- More robust to motion blur and texture-poor environments
- Standard in modern XR headsets (Quest 3, HoloLens 2, Vision Pro all use VI-SLAM variants)

### Dense vs. Sparse SLAM
- **Sparse SLAM**: Tracks a set of keypoints; fast, low memory; sufficient for localization
- **Dense SLAM**: Builds a full 3D reconstruction (mesh or point cloud); slower but enables surface-aware AR; needed for realistic occlusion and physics

## SLAM in Current XR Hardware

| Device | SLAM Approach | Mapping Quality | Loop Closure |
|--------|--------------|-----------------|--------------|
| Meta Quest 3 | 4-camera VI-SLAM | Room-scale, good | Yes |
| Apple Vision Pro | LiDAR + stereo VI-SLAM | Excellent, mesh-level | Yes |
| HoloLens 2 | Depth sensor + VI-SLAM | Room-scale, accurate | Yes |
| Magic Leap 2 | Custom depth sensor + VI-SLAM | Room-scale | Yes |
| Pico 4 | 4-camera VI-SLAM | Room-scale | Yes |

## Persistent Spatial Maps: The Missing Piece

Current SLAM implementations in commercial XR headsets generally do **not** persist spatial maps across sessions. Each time you put on a Quest 3 or Vision Pro:
- The device re-maps the room from scratch
- Objects placed in virtual space may drift or disappear
- The spatial AI assistant has no memory of what was in the room before

This is the key technical gap that Imagination AI is positioned to solve. Building a **persistent spatial memory layer** on top of SLAM — one that:
- Saves maps between sessions
- Updates incrementally rather than re-mapping from scratch
- Associates semantic meaning (this is a desk, this is a coffee mug) with mapped geometry
- Shares spatial maps across devices in the same space

This layer is analogous to what GPS did for navigation: it didn't replace the underlying positioning technology, it created a persistent, shareable coordinate system on top of it.

**Why this cannot be replaced by LLMs**: Current LLMs (including GPT-4o at 27.5% viewpoint accuracy) fundamentally cannot perform reliable spatial reasoning, and all current LLMs have zero persistent cross-session spatial memory. The persistent spatial memory layer must be built in the SLAM + scene graph stack — it cannot be prompt-engineered. See [[llm-spatial-reasoning]] for full benchmark data and failure pattern analysis.

## Open Standards and Interoperability

- **OpenXR** (Khronos Group): Cross-platform runtime API; 13+ vendors; standardizes controller input, rendering, and basic spatial anchors — but not persistent spatial memory
- **Spatial anchors**: Microsoft Azure Spatial Anchors, ARKit World Tracking, ARCore Cloud Anchors — proprietary attempts at persistence; not interoperable
- **OpenVDB / USD**: File format standards for 3D spatial data (Pixar USD is becoming the standard for spatial scene description)

The lack of an open standard for persistent spatial maps is both a market gap and a strategic opportunity.

## Deep Learning SLAM: Handling Dynamic Environments

Traditional feature-based SLAM systems (including ORB-SLAM3) assume a **static world**. In practice, AR/VR environments contain moving people and objects — pedestrians, vehicles, hands — whose motion corrupts pose estimation by introducing false geometric constraints. This is one of the hardest open problems in production SLAM. (source: `s41598-026-46629-0_reference.pdf`, Cui et al., *Scientific Reports*, 2026)

### The Dynamic Object Problem

When a moving object occupies a large portion of the camera's field of view:
- RANSAC (the standard outlier rejection method) fails — moving features outnumber static ones
- Pose estimates drift significantly
- Loop closure becomes unreliable

### SuperDynaSLAM (2026)

Cui et al. propose **SuperDynaSLAM**, a visual-inertial SLAM built on ORB-SLAM3 with two key upgrades:

**1. SuperPoint feature extractor** (replaces ORB)
- Deep learning-based, self-supervised via Homographic Adaptation
- More robust under violent motion and varying illumination
- Spatially uniform distribution of keypoints — better tracking stability
- Feature points classified into semantic classes (background / vehicle / pedestrian) using Mask R-CNN; matching only within same class to prevent cross-class errors

**2. Two-stage dynamic feature point detection**
- Stage 1 (semantic): Mask R-CNN generates initial mask of all *movable* objects
- Stage 2 (geometric): IMU measurements compute the expected epipolar line for each feature point; feature points that deviate beyond an adaptive threshold belong to *actually moving* objects
- Result: final mask contains only currently-moving objects; their feature points are removed before pose estimation

**Performance vs. ORB-SLAM3** (across EuRoC, VIODE, OpenLORIS-Scene datasets):
- Consistently lower absolute trajectory error (ATE), especially in high-dynamic scenes
- In Seq. city_day_3_high (many moving vehicles): 14.42% improvement in localization accuracy
- 95% confidence intervals consistently narrower — more stable across runs

**Key tradeoffs**:
- Runs at **2–3 FPS** vs. ORB-SLAM3's 25–30 FPS — not yet real-time; SuperPoint + Mask R-CNN dominate compute
- Limited to object categories recognized by pre-trained Mask R-CNN — shopping carts, unusual objects bypass the filter
- Future directions: Segment Anything Model (SAM) for open-world segmentation; LiDAR fusion; lightweight perception networks

**Strategic implication for Imagination AI / 9D Technologies**: Any spatial AI assistant deployed in real-world XR must handle dynamic environments. The SuperDynaSLAM approach — semantic + geometric fusion — is the current state of the art, but the 2–3 FPS limitation means a production system would need lighter-weight alternatives (e.g., mobile-optimized SuperPoint, YOLOv8 instead of Mask R-CNN) or edge-cloud split inference.

## 3D Gaussian Splatting: A New Representation for Persistent Spatial Maps

Traditional SLAM builds geometric maps — point clouds, meshes, voxel grids. An emerging alternative is **3D Gaussian Splatting (3DGS)**, which represents scenes as a collection of 3D Gaussians that can be rendered photorealistically in real-time. (source: `Key Trends & Research Pipelines.pdf`)

### Why 3DGS Matters for Spatial AI

| Property | Traditional SLAM Map | 3DGS Map |
|----------|---------------------|---------|
| Representation | Points/mesh/voxels | 3D Gaussians |
| Visual fidelity | Low (geometric) | Photorealistic |
| Render speed | Fast | 30fps on iPhone 15 |
| Edit/update | Incremental | GaussianEditor supports text-driven edits |
| Map size | Small | Larger (but compressible) |

**[[splatam|SplaTAM]]** (CMU, 2024) is the key paper: it combines SLAM with 3DGS, enabling real-time dense reconstruction of a scene as photorealistic Gaussian splats. This is the first system to deliver both SLAM accuracy *and* photorealistic output at real-time speeds (0.6cm ATE RMSE, 400 FPS rendering).

**Practical implication**: A persistent spatial memory layer built on 3DGS doesn't just know *where* objects are — it captures exactly *how they look*. For a Spatial AI Assistant, this means the system can visually recognize changes in the environment ("the whiteboard has new content since yesterday") rather than just detecting geometric differences. It also enables rendering the remembered environment for context even when the user isn't physically present.

**Current limitation**: 3DGS maps are larger than point cloud maps; editing (adding/removing objects post-capture) is only partially solved. [[gaussianeditor|GaussianEditor]] enables text-driven scene editing in 5–10 minutes per edit, but is not yet real-time.

## Semantic 3D Mapping: ConceptFusion

Beyond 3DGS geometry, persistent spatial maps need **semantic meaning** attached to every point — not just "where is this surface?" but "what is this object?" [[ConceptFusion]] (MIT/CMU, 2023) provides exactly this layer by fusing CLIP and DINO features into the 3D map during construction. The result: every 3D point carries a semantic embedding, making the map queryable by text, image, audio, or click — zero-shot, without task-specific training.

ConceptFusion + SplaTAM represents the full stack: SplaTAM provides photorealistic geometry, ConceptFusion provides open-vocabulary semantics. Combined, the persistent spatial memory layer not only captures how a scene looks but what everything in it means.

See [[ego-centric-3d-perception]] for the streaming ego-centric variant, and [[scene-language-models]] for an alternative approach that encodes scene structure as language.

## Scene Understanding & Object Recognition

Beyond geometric SLAM, modern spatial AI requires semantic understanding of what's in the environment. This extends SLAM from "where" to "what" (source: `Scene_Understanding_Object_Recognition_Landscape_2026-04-21.md`):

### Platform Capabilities

| Platform | Capability | Key Feature |
|----------|------------|-------------|
| **Apple ARKit** | Scene Understanding | Detects surfaces, estimates lighting, tracks body motion; indoor-focused |
| **Meta Scene API** | Persistent scene models | OS-persisted across apps, shared spatial understanding |
| **Google Scene Semantics** | Pixel-level labeling | Real-time semantic segmentation via Hexagon DSP |
| **Open-source** | SAM, GroundingDINO, YOLO-World | Zero-shot segmentation and open-world detection |

### Semantic Layer vs. Geometric SLAM

- **Geometric SLAM**: Answers "where is the device?" and "what is the geometry of this room?"
- **Scene Understanding**: Answers "what is this object?" and "what is this surface used for?"

The strategic opportunity: combining persistent spatial memory with semantic understanding creates the foundation for a truly intelligent spatial assistant that remembers not just where objects are, but what they are and their context.

## Related pages

- [[spatial-ai-assistant]]
- [[llm-spatial-reasoning]]
- [[spatial-ai-assistant-architecture]]
- [[splatam]]
- [[conceptfusion]]
- [[gaussianeditor]]
- [[ego-centric-3d-perception]]
- [[scene-language-models]]
- [[xr-hardware]]
- [[xr-platforms]]
- [[digital-twins]]
- [[arkit-scene-understanding]]
- [[meta-scene-api]]
- [[google-scene-semantics]]
- [[open-source-scene-understanding]]
