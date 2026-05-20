# Scene Language Models

**Summary**: A new class of AI system that represents, reconstructs, and reasons about 3D scenes using the same autoregressive sequence-generation machinery as language models — treating spatial structure as a structured language, not as geometric data.

**Sources**: `raw/papers/SceneScript Reconstructing Scenes With An Autoregressive Structured Language Model.pdf`, `raw/papers/3D-LLM Injecting the 3D World into Large Language Models.pdf`, `raw/papers/An Embodied Generalist Agent in 3D World.pdf`, `Key Trends & Research Pipelines.pdf`

**Last updated**: 2026-04-27

---

## The Core Idea

For decades, 3D scene understanding has been treated as a **geometry problem**: reconstruct meshes, predict voxel labels, regress bounding box coordinates. The dominant architectures — CNNs, 3D convolutions, PointNets — are all built to process spatial signals as numerical arrays.

Scene language models propose an alternative: **represent scenes as sequences**. Sequence models — transformers, autoregressive generators — are arguably the most powerful learning architecture today. Why not apply them to 3D scenes?

The insight is that 3D scenes have **compositional, hierarchical, relational structure** that is more naturally expressed in a language-like representation than in a geometric one:
- A room is composed of walls, doors, windows, and objects
- Objects are composed of parts
- Parts have spatial relationships to each other and to the room
- These relationships can be expressed as text commands, graph traversals, or natural language

Once a scene is expressed as a sequence, the full power of transformer architectures — attention over tokens, autoregressive generation, few-shot prompting, in-context learning — becomes applicable to 3D spatial reasoning.

## SceneScript: The Foundational Demonstration

[[SceneScript]] (Meta Reality Labs, Mar 2024) is the clearest and most practically successful demonstration of the scene language model concept to date.

### What SceneScript Does

SceneScript takes a 3D point cloud (from smart glasses or depth camera) and generates a **program** that reconstructs the scene:

```
make_wall(id=0, a_x=0.0, a_y=0.0, a_z=0.0, b_x=4.2, b_y=0.0, b_z=0.0, height=2.4)
make_wall(id=1, a_x=4.2, a_y=0.0, a_z=0.0, b_x=4.2, b_y=3.6, b_z=0.0, height=2.4)
make_door(id=2, wall0_id=0, wall1_id=1, position_x=2.1, position_y=0.0, position_z=0.0, width=0.9, height=2.1)
make_bbox(id=3, class=chair, position_x=1.5, position_y=1.8, position_z=0.0, angle_z=45, scale_x=0.5, scale_y=0.5, scale_z=0.9)
make_prim(bbox_id=3, prim_num=0, class=seat, center_x=1.5, center_y=1.8, center_z=0.45, ...)
```

This is not pseudocode — it is the literal output of a transformer decoder, generated token-by-token exactly like a language model generates text.

### Why SceneScript Performance Is Extraordinary

| Method | F1@5cm |
|--------|--------|
| SceneScript (lifted features) | **0.903** |
| SceneScript (points only) | 0.848 |
| SceneScript (image only) | 0.661 |
| RoomFormer (prior best geometric method) | 0.139 |

The 0.903 vs 0.139 gap — 6.5× improvement — is not incremental progress. It suggests that the scene language approach is qualitatively superior for **structured scene reconstruction** compared to direct geometric regression.

The intuition: learning to **generate** a structured description of a scene (autoregressive, compositional) forces the model to develop strong priors about scene composition, room layouts, and spatial relationships. Direct geometric regression (predict bounding box → refine) lacks this compositional prior.

### Extensibility: The Killer Property

Adding a new object type or structural element to a geometric reconstruction model typically requires:
- Redesigning the detection head
- Rebalancing the training objective
- Retraining (or at minimum, fine-tuning)

Adding a new command type to SceneScript requires:
1. Define the new command and parameters
2. Generate training examples using the new command
3. Fine-tune the existing sequence model

The model architecture stays constant. This is the same reason it's easy to teach a language model new vocabulary — the architecture doesn't care about the vocabulary, only the sequence distribution.

For a spatial AI assistant deployed across diverse environments (OR, factory floor, office, classroom), this extensibility means a single architecture can be specialized to each domain with only data changes.

## The Broader Landscape

SceneScript is the most prominent current instance, but the scene language model idea connects to a family of related work:

### Spatial Tokens in LLMs

[[3D-LLM]] introduces **3D location tokens** — explicit spatial position tokens added to an LLM's vocabulary. The model can then both *consume* 3D spatial context and *produce* spatial predictions (e.g., "the object is at position [token: 1.5m, 2.1m, 0.8m]").

This extends the language model interface in the other direction: rather than converting scenes to structured language programs (SceneScript), it converts language models into spatial predictors.

### Embodied Language Agents

[[LEO]] uses language models with 3D-aware encoders to generate **action sequences** from scene descriptions. The output is a program for navigating and interacting with the 3D world — again, scenes converted to sequences, but here the sequences are actions rather than descriptions.

### Spatial VQA as Scene Language

[[SpatialVLM]] converts metric spatial relationships between objects into natural language QA pairs. The model learns that "how far is X from Y?" → "approximately 2.3 meters" by training on 2B spatial QA pairs derived from map data. This is the scene language model applied to *spatial querying* rather than *scene reconstruction*.

### Unified View

| System | Input | Output Sequence | Language Type |
|--------|-------|----------------|---------------|
| SceneScript | Point cloud / images | Structured commands (`make_wall`, `make_bbox`) | Domain-specific language (DSL) |
| 3D-LLM | 3D point cloud | Location tokens + text | Augmented natural language |
| LEO | Ego-centric video | Action primitives | Action language |
| SpatialVLM | Image | Metric QA text | Natural language |

## Why Scene Language Models Are Strategically Important

### 1. They Unify Perception and Reasoning

Traditional spatial AI pipelines have a hard boundary: perception (geometric, visual) feeds into reasoning (language, logic). Scene language models dissolve this boundary — the same transformer architecture handles both.

This matters for [[spatial-ai-assistant-architecture]]: a scene language model can take sensor input and directly output a structured scene description that is also a valid prompt for downstream reasoning. No hand-designed format conversion needed.

### 2. They Leverage the Full LLM Ecosystem

Scene language models inherit every capability of the language model ecosystem:
- **Few-shot prompting**: Show 2–3 example scenes → model adapts to a new scene type
- **Instruction following**: "Describe only the furniture" → selectively generate `make_bbox` tokens for furniture categories
- **Chain-of-thought**: Generate a step-by-step "thought process" about scene structure before generating the final commands
- **In-context learning**: No fine-tuning needed for new tasks; just change the context/prompt

### 3. They Handle Uncertainty Naturally

Language models produce probability distributions over tokens. A scene language model's uncertainty about a room layout is naturally expressed as probability distributions over spatial command parameters — "there's probably a wall here, but I'm uncertain about its exact length." Geometric methods require ad-hoc uncertainty representations.

### 4. They Are Inherently Composable with LLMs

A scene language model's output — a text program — can be directly consumed by any language model for downstream tasks: "given this room description, generate a safety inspection checklist," or "given this layout, plan the optimal path to the exit." No format conversion, no adapter — it's already text.

## Limitations and Open Problems

### Current Scope: Structured Environments

SceneScript works well for indoor architectural environments with clear primitives (walls, doors, windows, boxes). Extension to unstructured outdoor environments, deformable objects, or fine-grained part-level geometry is not demonstrated.

### Hallucination Risk

Like all language models, scene language models can hallucinate — generating plausible-sounding commands for objects that don't exist, or incorrect spatial positions. For applications where scene accuracy is safety-critical (surgical environment setup, emergency response), hallucination detection and verification is essential.

### Real-Time Streaming

SceneScript's 2–5 second inference makes it suitable for batch scene reconstruction, not real-time streaming updates. For an XR assistant that must update its scene model 30 times per second, a faster (potentially non-autoregressive) variant is needed.

### Scale vs. Coverage Trade-off

SceneScript encodes scenes as commands — rich and structured, but with a fixed vocabulary of primitive shapes and object categories. [[ConceptFusion]]'s approach — encoding every point with full CLIP semantic features — gives richer semantic coverage at the cost of losing the compositional structure that makes scene language models extensible.

The ideal system would combine both: a scene language model for structure, ConceptFusion-style feature maps for semantics.

## Implications for Imagination AI / 9D Technologies

1. **Scene language is the right abstraction for a Spatial AI Assistant** — it bridges the gap between raw sensor data and LLM reasoning without requiring a hand-designed intermediate representation.

2. **Extensibility via command vocabulary** — 9D Technologies can define domain-specific command vocabularies for healthcare (`make_patient_bed`, `make_defibrillator`) or industrial (`make_conveyor_belt`, `make_safety_zone`) and extend SceneScript-style models without architectural changes.

3. **Aria Synthetic Environments is publicly available** — Meta released the 100K scene training dataset. 9D Technologies can use it directly, or augment it with domain-specific synthetic scenes to fine-tune a specialized scene language model.

4. **Direct integration with LLM pipeline** — The structured command output of a scene language model can be directly included in an LLM context window as a "scene description." No adapter, no format conversion, no information loss.

## Related pages

- [[scenescript]]
- [[3d-llm]]
- [[leo]]
- [[spatialvlm]]
- [[ego-centric-3d-perception]]
- [[spatial-ai-assistant-architecture]]
- [[slam]]
- [[conceptfusion]]
- [[xr-trends-research-pipelines]]
