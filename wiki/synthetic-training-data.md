# Synthetic Training Data

**Summary**: A cross-paper pattern in which synthetically-generated training data — from renderers, world models, map pipelines, or other models — achieves near-parity with real annotated data while dramatically reducing cost and enabling coverage of scenarios that real data cannot provide.

**Sources**: `raw/papers/WorldGPT Empowering LLM as Multimodal World Model.pdf`, `raw/papers/Depth Anything V2.pdf`, `raw/papers/SpatialVLM Endowing Vision-Language Models with Spatial Reasoning Capabilities.pdf`, `raw/papers/SceneScript Reconstructing Scenes With An Autoregressive Structured Language Model.pdf`, `raw/papers/An Embodied Generalist Agent in 3D World.pdf`

**Last updated**: 2026-04-27

---

## The Core Thesis

Real annotated training data is the primary bottleneck for most modern AI systems. Human annotation is expensive, slow, inconsistent, and physically constrained — you cannot annotate scenarios that don't exist yet, hazardous environments that are unsafe to film, or rare events that occur too infrequently to capture at scale.

The papers ingested in this batch collectively demonstrate a pattern that is becoming a primary strategy in applied ML research:

**Synthetic data, generated at low cost, is approaching parity with real annotated data — and in some cases exceeds it.**

This is not a single trick but a family of techniques, each appropriate to different problem types.

## The Four Techniques

### Technique 1: Renderer-Generated Ground Truth (Depth Anything V2)

**Problem**: Monocular depth estimation requires pixel-perfect depth ground truth for training. LiDAR-scanned real data is expensive and limited in scale.

**Synthetic solution**: Train the teacher model entirely on **photorealistic synthetic renders** where depth is trivially exact (provided by the renderer). Use this teacher to generate pseudo-labels for 62M real unlabeled photos. Train students on pseudo-labeled real data.

**Result**: 97.1% δ₁ — outperforms all prior methods including Marigold (86.8%) trained on real data.

**The synthetic-to-real bridge**: The synthetic teacher's structural priors (learned from perfect CG renders) transfer reliably to real photos because the relationship between object structure and depth is physics-based, not domain-specific. A table casts the same depth pattern in a synthetic render and a real photo.

**Key limitation**: Works when the relevant property (depth profile, object composition) is domain-invariant. Fails when appearance matters more than structure (e.g., fine-grained texture recognition in new material categories).

### Technique 2: Pipeline-Generated Relational Labels (SpatialVLM)

**Problem**: Spatial reasoning QA requires metric labels ("how far is X from Y?"). No human-annotated dataset contains spatial QA at the scale needed for training strong spatial reasoning.

**Synthetic solution**: Use **web-scale map data** (Google Maps satellite imagery with known metric coordinates) to automatically derive spatial relationships and generate 2 billion QA pairs. No human annotation required — ground truth is computed directly from the geometry of the map.

**Result**: 75.2% spatial distance estimation accuracy vs GPT-4V's 68% — better than the best commercial model, trained only on synthetically-derived QA.

**The key insight**: Spatial QA labels are a **deterministic function** of metric positions. If you know where two objects are in 3D space, you can generate arbitrarily many spatial questions and answers about them. Real-world data with known coordinates (maps, robotics logs, synthetic scenes) can generate these labels without any human labeling.

**Generalization**: Any relational property that can be computed from a scene's geometry or semantics — not just depth, but "which direction is X from Y?", "is X above or below Z?", "how many objects are within 2 meters of the camera?" — can be used to generate training labels automatically.

### Technique 3: Designed Synthetic Environments (SceneScript)

**Problem**: Training a scene reconstruction model requires thousands of diverse indoor scenes with ground-truth layout annotations. Such annotated real datasets don't exist at scale.

**Synthetic solution**: Use **procedurally-generated synthetic indoor scenes** (Aria Synthetic Environments: 100K scenes) where layout ground truth is trivially known from the scene generator. Train the SceneScript model entirely on synthetic data, no real-scene fine-tuning.

**Result**: F1@5cm of 0.903 — 6.5× improvement over prior state of the art (RoomFormer at 0.139). Generalizes to real environments without any real-scene training.

**Why this works for scene reconstruction**: Structural properties of indoor environments (walls are vertical, doors are in walls, furniture has characteristic scale ratios) are governed by architectural norms that transfer from synthetic to real. The model learns compositional rules, not photorealistic appearance.

**Aria Synthetic Environments availability**: Meta publicly released this 100K-scene dataset. Any team can train SceneScript-style models using it — no investment in real-scene annotation required.

**Scale**: 100K diverse scenes is sufficient for strong generalization. The training data pipeline is procedural — generating another 1M scenes is a matter of compute, not annotation labor.

### Technique 4: Dream Tuning — AI-Generated Training Data (WorldGPT)

**Problem**: Fine-tuning multimodal models on new tasks requires large amounts of task-specific labeled examples. Collecting real multimodal data (video + audio + text + action labels) for specialized domains is prohibitively expensive.

**Synthetic solution**: Train a world model (WorldGPT) on available real multimodal data. Then use WorldGPT to **generate synthetic training examples** for the new task — the world model "dreams" plausible scenario transitions that the student model uses as training data.

**Result**: WorldGPT-synthetic training data achieves within 4% of real data performance on Visual Understanding and Embodied Planning tasks, and **outperforms** real data on Audio-Visual QA. Cost reduction: **30×**.

| Task | Real data training | Dream tuning | Gap |
|------|-------------------|-------------|-----|
| Visual Understanding | 36.3 | 34.8 | -4% |
| Embodied Planning | 40.5 | 38.8 | -4% |
| Audio-Visual QA | 47.5 | **48.5** | +2% |

**Why dream tuning can outperform real data**: Real-world multimodal datasets have coverage gaps — rare audio-visual combinations, unusual scenario transitions, domain-specific events. A world model can generate synthetic examples that fill these gaps uniformly, without the frequency biases of real-world data collection.

**The key requirement**: Dream tuning requires an existing capable world model to generate the synthetic data. It is a **second-order technique** — it compounds the return on investment in the initial world model, rather than replacing it. You still need to train WorldGPT on real data first.

**The compounding dynamic**: As more real data is used to train better world models, those world models generate better synthetic data, which trains better task-specific models. The return on each real data example increases as world models improve.

### Technique 5: O-CoT Data Augmentation (LEO)

**Problem**: Training an embodied agent requires examples of spatially-grounded reasoning — reasoning chains that explicitly reference 3D positions. No existing dataset has this.

**Synthetic solution**: Take existing embodied task datasets (which have task descriptions but not spatially-grounded reasoning). Extract 3D positions from scene annotations. Use GPT-3.5 to generate **Object-grounded Chain-of-Thought** (O-CoT) reasoning chains that reference the extracted positions.

**Result**: O-CoT training data significantly improves LEO's performance on embodied spatial tasks compared to training without position-grounded reasoning chains.

**The pattern**: Augment existing data with computed properties (positions, relationships) and use a capable LLM to generate richer training labels that incorporate those properties. No new real data needed.

## Cross-Paper Comparison

| Paper | Technique | Data Type | Cost Reduction | Performance vs Real |
|-------|-----------|-----------|---------------|---------------------|
| [[depth-anything-v2]] | Renderer GT + pseudo-labeling | Depth maps | ~10–50× | Exceeds (97.1% vs 86.8%) |
| [[spatialvlm]] | Pipeline-derived labels | Spatial QA pairs | ~100× | Exceeds (75.2% vs 68%) |
| [[scenescript]] | Procedural scene generation | Room layouts | ~20× | 6.5× improvement over prior |
| [[worldgpt]] | Dream tuning | Multimodal transitions | **30×** | Within 4%; beats on AVQA |
| [[leo]] | LLM-augmented CoT | Reasoning chains | ~5× | Meaningful improvement |

## The Shared Pattern

Despite the different domains, all five techniques share the same structure:

```
Real data (expensive, limited)
    ↓ Used to:
        - Train a teacher model
        - Calibrate a procedural generator
        - Ground a QA generation pipeline
        - Train a world model
Synthetic data (cheap, scalable, controllable)
    ↓ Used to:
Train production model
    ↓
Performance ≈ or > real-data-trained model
```

The key is that **the synthetic data captures the properties the model needs to learn** — not all properties, but the ones that matter for the target task. Depth profiling, spatial relationships, room structure, state transitions. These are all deterministic or model-able from first principles.

## The Remaining Role of Real Data

Despite the synthetic data success stories, real data is not obsolete:

1. **[[embodiedscan]]'s finding**: Real capture beats rendering by ~6% AP on fine-grained 3D object detection. Photorealistic appearance details that distinguish visually similar objects still benefit from real-world capture.

2. **Initial teacher/world model**: Every synthetic data technique requires a capable model trained on real data to bootstrap. SpatialVLM's pipeline is anchored in real map coordinates. WorldGPT's teacher is trained on 11M real videos.

3. **Distribution edge cases**: Real-world data captures distribution tails (unusual lighting, edge-case object configurations) that procedural generators may miss.

4. **Evaluation**: Synthetic-trained models should be validated on real-world benchmarks — the EmbodiedScan comparison provides exactly this validation infrastructure.

**Synthesis**: Real data provides the structural priors; synthetic data provides the scale. The optimal strategy is to use real data to build strong foundation models, then use synthetic data for task-specific fine-tuning and scale-out.

## Implications for Imagination AI / 9D Technologies

### Immediate Opportunities

1. **Spatial QA for XR domains**: Following SpatialVLM's approach — use SLAM outputs and scene graphs from real XR sessions to automatically generate spatial QA pairs. Build a domain-specific spatial reasoning dataset without annotation cost.

2. **Surgical / industrial scene generation**: Following SceneScript / Aria Synthetic Environments — build a procedural generator for clinical or industrial environments. 10K scenes is sufficient (SceneScript trained on 100K; 10K would likely be sufficient for a narrower domain). Cost: engineering time for the procedural generator, not annotation labor.

3. **Dream tuning for vertical fine-tuning**: Once a foundation world model is available (via fine-tuning [[worldgpt]] or similar), use dream tuning to generate unlimited domain-specific training data for healthcare simulation or industrial training scenarios.

4. **O-CoT for spatial reasoning chains**: Extract 3D positions from Quest 3 or Vision Pro scene graphs → use GPT-4 to generate O-CoT style reasoning chains → use as fine-tuning data for the spatial AI assistant's reasoning module.

### Strategic Implication

The real competitive moat in spatial AI is no longer **data collection** — synthetic data strategies have largely solved the quantity problem. The moat is:
1. **The initial real-world capture** (enough to train the first-generation model)
2. **Domain-specific scene generators** (the procedural assets that define the synthetic environment)
3. **The fine-tuning pipeline** (efficiently adapting foundation models to specific verticals)

## Related pages

- [[worldgpt]]
- [[depth-anything-v2]]
- [[spatialvlm]]
- [[scenescript]]
- [[leo]]
- [[embodiedscan]]
- [[scene-language-models]]
- [[world-models]]
- [[xr-simulations-training]]
- [[xr-trends-research-pipelines]]
