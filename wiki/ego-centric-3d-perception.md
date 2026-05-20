# Ego-Centric 3D Perception

**Summary**: The shift from global, pre-built 3D scene scans to streaming, first-person 3D perception — understanding the world from the viewpoint of a moving agent receiving incomplete, incremental observations — representing the defining paradigm shift in embodied AI and XR spatial understanding.

**Sources**: `raw/papers/EmbodiedScan A Holistic Multi-Modal 3D Perception Suite Towards Embodied AI.pdf`, `raw/papers/SceneScript Reconstructing Scenes With An Autoregressive Structured Language Model.pdf`, `raw/papers/An Embodied Generalist Agent in 3D World.pdf`, `raw/papers/ConceptFusion Open-set Multimodal 3D Mapping.pdf`, `raw/papers/3D-LLM Injecting the 3D World into Large Language Models.pdf`, `Key Trends & Research Pipelines.pdf`

**Last updated**: 2026-04-27

---

## The Paradigm Shift

The first generation of 3D scene understanding research operated in **allocentric mode**: a static, global coordinate system, with full 3D scans pre-built before any reasoning began. ScanNet, ShapeNet, Matterport3D — the standard datasets — all provide complete, camera-registered 3D reconstructions of rooms as inputs.

This is not how spatial AI systems will operate in practice.

A person wearing smart glasses or an XR headset moves through a space. They see only what is in their field of view at any given moment. The scene model must be built incrementally from a streaming first-person video feed. The reference frame shifts with every head movement. The agent must reason about objects it has already passed (allocentric) while simultaneously processing what it currently sees (egocentric). It must make decisions before having full information.

This is **ego-centric 3D perception** — and it is the defining technical challenge of the papers in this ingestion batch.

## Why Ego-Centric Matters

### XR Hardware Reality

| Device | Sensor Configuration | Scene Access |
|--------|---------------------|-------------|
| Meta Quest 3 | 4 outward-facing cameras + depth | Streaming video, partial FOV |
| Apple Vision Pro | Stereo + LiDAR + IMU | Streaming, headset-mounted |
| Meta Ray-Ban glasses | Dual cameras, no depth | Single forward camera |
| Google Gemini glasses (2026) | Cameras, no depth sensor | Streaming monocular |
| Project Aria | Full multi-sensor research rig | Full ego-centric streaming |

None of these devices provides a pre-built global point cloud. Any spatial AI assistant must work with streaming ego-centric input, not pre-built scans.

### The Core Difficulties

**1. Partial observability**: The agent sees at most 120° of a room at once. Reasoning requires maintaining a model of the parts currently out of view — "where did I put the red mug?" requires remembering what is behind me.

**2. Viewpoint-dependent representations**: Visual features change dramatically as the viewpoint moves. A model that encodes the scene in an ego-centric reference frame must continuously update as the agent moves.

**3. Incremental accumulation**: Each new frame adds a little more information. The model must integrate new observations without forgetting prior ones — and resolve conflicts when new observations contradict old predictions (the "closed world assumption" breaks down).

**4. Real-time requirement**: XR assistants must respond in under 100ms (see [[spatial-ai-assistant-architecture]] latency spec). This is incompatible with full-scene re-processing on every frame. Incremental update is mandatory.

**5. Egocentric-allocentric translation**: Users ask questions in egocentric terms ("to my left") and allocentric terms ("near the door"). The system must maintain both reference frames and translate between them.

## Papers in This Paradigm

### EmbodiedScan: The Data Foundation

[[EmbodiedScan]] (Shanghai AI Lab, Dec 2023) is the infrastructure paper for ego-centric perception. Its contribution is a benchmark designed from first principles in the ego-centric paradigm:

- **5,765 scans** from three RGB-D datasets, unified under a single ego-centric annotation scheme
- **1M+ language prompts** designed to require ego-centric spatial reasoning
- **760+ object categories** — 40× the vocabulary of ScanNet, needed for real-world deployment
- **Continuous ego-centric viewpoints** — frames are organized as continuous first-person trajectories, not random independent views

The key design choice: every annotation is expressed relative to the **ego-centric frame** (relative to the camera at a specific point in the trajectory). This forces models trained on EmbodiedScan to learn ego-centric reasoning, not just static global scene understanding.

**Training-time finding**: Near-linear performance scaling with scan count. The community is not close to the data ceiling — more ego-centric data continues to improve models.

### SceneScript: Ego-Centric Reconstruction at Scale

[[SceneScript]] (Meta Reality Labs, Mar 2024) applies the scene language model approach directly to ego-centric inputs from smart glasses. The input is a streaming point cloud from Project Aria (an ego-centric multi-sensor glasses platform); the output is a structured description of the room as seen from that ego-centric trajectory.

Key ego-centric properties:
- **Streaming-compatible**: SceneScript reconstructs scenes from partial observations as they accumulate, not from a complete scan
- **Inference time 2–5 seconds**: Fast enough for near-real-time reconstruction in XR
- **Trained on ego-centric synthetic data**: Aria Synthetic Environments simulates first-person trajectories through indoor spaces — the training distribution matches deployment

SceneScript demonstrates that scene language models are not limited to batch processing — they can operate on the incomplete, viewpoint-constrained observations that ego-centric devices produce.

### LEO: Ego-Centric Embodied Agency

[[LEO]] (Zhejiang/Shanghai, 2023) takes ego-centric perception to its logical conclusion: not just understanding the scene from first-person view, but **acting in it** from first-person view.

LEO's architecture is ego-centric by design:
- **Input**: Continuous ego-centric video frames (not pre-built point cloud)
- **Viewpoint-dependent perceiver**: Explicitly encodes the agent's current viewpoint as a conditioning signal
- **Action output**: Navigation and manipulation actions defined in the agent's current reference frame
- **O-CoT training**: Reasoning chains include explicit ego-centric position references ("the object is 1.2m to my right")

LEO establishes that a generalist embodied agent — one model for QA, navigation, planning, and manipulation — can be trained with ego-centric data and deployed in streaming mode.

### ConceptFusion: Semantic Ego-Centric Mapping

[[ConceptFusion]] builds rich semantic 3D maps from ego-centric RGB-D observations. As the agent moves through a space, ConceptFusion fuses CLIP/DINO features from each frame into the growing 3D map — incrementally, frame by frame.

This is explicitly ego-centric: the agent does not need a complete scan to build the semantic map. Each new viewpoint contributes new observations that are fused into the map. By the time the agent has explored a full room, the map is both geometrically accurate and semantically queryable.

**Limitation**: ConceptFusion, as published, runs offline — feature fusion is slow enough that it cannot update the semantic map in real time during exploration. Real-time ego-centric semantic mapping remains an open engineering problem.

### 3D-LLM: Pre-Scan First, Then Query

[[3D-LLM]] operates on pre-built 3D scans — it is not ego-centric by design. It is included here because it establishes the **language interface** for 3D scene queries that ego-centric systems need to adopt.

The gap 3D-LLM leaves open is the ego-centric streaming case: as the agent is mid-exploration, with only a partial scene model, can the LLM-based query interface still provide accurate answers? This remains unresolved and is an active research direction.

## Architecture Implications for XR Deployment

An XR spatial AI assistant combining these papers would implement ego-centric 3D perception as follows:

```
Streaming frames from headset cameras
    ↓
Depth estimation (Depth Anything V2 or onboard depth sensor)
    ↓
Ego-centric SLAM (VI-SLAM: track camera pose in real time)
    ↓ ←→ (incremental)
Persistent spatial map (3DGS via SplaTAM — grows as more of space is seen)
    ↓ (parallel)
ConceptFusion feature fusion (builds semantic layer on top of geometry)
    ↓
SceneScript-style reconstruction (structured scene description when reconstruction requested)
    ↓
Scene graph (nodes = objects, edges = spatial relationships, both ego-centric + allocentric)
    ↓
LLM reasoning layer (receives scene graph as structured context)
    ↓
Response / Action
```

Each layer is incremental and streaming-compatible — the system works from the first frame and improves as more of the space is explored.

## The Ego-Centric Data Challenge

### The Annotation Bottleneck

Ego-centric annotations are harder to obtain than global scene annotations:
- Human annotators must be placed in the ego-centric viewpoint to make ego-relative spatial judgments
- Dynamic scenes (objects moving) require temporal annotation across frames
- Long-tail object categories (rare equipment, unusual objects) require domain expert annotators

EmbodiedScan's SAM-assisted annotation pipeline addresses the scale issue. Domain-specific datasets (surgical instruments, industrial equipment) remain an unsolved annotation challenge.

### The Synthetic Data Bridge

[[Synthetic-training-data]] strategies partially solve the annotation bottleneck:
- Procedural generation of ego-centric trajectories through synthetic scenes (SceneScript / Aria Synthetic Environments)
- Dream tuning from world models to generate synthetic ego-centric transitions ([[worldgpt]])
- Pipeline-derived spatial QA from SLAM outputs ([[spatialvlm]])

But EmbodiedScan's finding — **real capture beats rendering by ~6% AP** — suggests that some ego-centric perception tasks still benefit meaningfully from real-world capture data.

## Where the Field Is Heading

The 2023–2024 papers in this batch establish the ego-centric paradigm as the dominant research direction. The next challenges are:

1. **Real-time ego-centric semantic mapping**: ConceptFusion at 30 FPS on edge hardware
2. **Ego-centric open-vocabulary 3D detection**: EmbodiedScan's 760+ categories at inference time in streaming mode
3. **Incremental scene language models**: SceneScript updated per-frame without full re-inference
4. **Ego-centric persistent memory**: Cross-session, cross-device ego-centric scene models that maintain both allocentric map and egocentric access patterns

For the [[spatial-ai-assistant]] vision: these are the four open engineering problems between current research and production deployment.

## Related pages

- [[embodiedscan]]
- [[scenescript]]
- [[leo]]
- [[conceptfusion]]
- [[3d-llm]]
- [[splatam]]
- [[slam]]
- [[scene-language-models]]
- [[spatial-ai-assistant-architecture]]
- [[llm-spatial-reasoning]]
- [[xr-hardware]]
- [[xr-trends-research-pipelines]]
