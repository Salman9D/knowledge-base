# LLM Spatial Reasoning

**Summary**: Analysis of how well current large language models reason about space, object positions, and viewpoints — with benchmark data, identified failure patterns, and the architectural path forward via Vision-Language-Action models.

**Sources**: `2_3a_spatial_reasoning_llm_analysis.pdf`

**Last updated**: 2026-04-24

---

## The Core Problem

Current LLMs were trained primarily on text and 2D images. Spatial reasoning — the ability to understand where objects are relative to each other and to the viewer — requires a fundamentally different kind of representation than language. The gap between what LLMs can articulate about space and what they can reliably reason about has direct consequences for [[spatial-ai-assistant]] design.

## Benchmark Data

| Model | Viewpoint Accuracy | Notes |
|-------|--------------------|-------|
| GPT-4o | **27.5%** | Fails basic viewpoint-change benchmarks |
| Gemini (best) | Leads among general LLMs | Still fails persistent cross-session memory |
| Claude | Explicitly limited on spatial tasks | Per internal 9D Technologies analysis |
| All models | **0%** persistent cross-session spatial memory | Universal failure across all tested models |

(Source: `2_3a_spatial_reasoning_llm_analysis.pdf`)

**Key finding**: GPT-4o achieves only 27.5% accuracy on viewpoint-change benchmarks — tasks that ask the model to reason about what an object or scene would look like from a different position. This is close to chance performance on multi-choice spatial tasks.

## Why This Matters for Spatial AI

A [[spatial-ai-assistant]] that relies solely on an LLM for spatial reasoning will:
- Fail to correctly describe relative positions after the user moves
- Lose all spatial context between sessions (memory resets to zero)
- Struggle with questions like "is the red mug still on the shelf to my left?"
- Cannot update an internal spatial model as the user walks through a space

This is not a model capability issue that will be solved by scaling alone. The failure modes are architectural.

## 6 Identified Failure Patterns

1. **Reference frame confusion**: Model loses track of whether coordinates are in world space (allocentric) vs. viewer space (egocentric). Switches between frames mid-reasoning.

2. **Occlusion handling**: Cannot correctly infer what is hidden behind other objects — or correctly update hidden-object status as viewpoint changes.

3. **Scale estimation**: Systematically wrong on distance and size judgments. Cannot ground scale from context alone.

4. **Rotation**: Fails to correctly simulate how a scene transforms when observer rotates. Mental rotation tasks break down.

5. **Temporal continuity**: Loses object position history when objects move across turns. Cannot track dynamic changes over time.

6. **Egocentric vs. allocentric switching**: Cannot reliably translate between "the cup is to my left" (egocentric) and "the cup is north of the table" (allocentric). Both representations are needed in spatial AI.

## The Persistent Memory Gap

The most strategically important finding: **every current LLM fails persistent cross-session spatial memory.** This is not a benchmark gap — it is an architectural absence.

All current commercial LLM APIs (as of April 2026):
- Receive spatial context only within the current prompt/context window
- Cannot persist object locations, room geometry, or semantic labels across sessions
- Cannot update an internal spatial model incrementally as the environment changes

This is why [[slam]] and scene graphs (see [[spatial-ai-assistant-architecture]]) are necessary as persistent memory layers — they cannot be replaced by prompt engineering alone.

## Recommended Architecture: LLM-as-Reasoning-Layer-Only

The recommended design pattern is **not** to use an LLM as the spatial understanding layer. Instead:

```
Sensor Input
    ↓
On-device SLAM + Object Detection (handles spatial grounding)
    ↓
Scene Graph (persistent world model — nodes = objects, edges = relationships)
    ↓
LLM (receives structured spatial context; handles language, planning, task execution)
    ↓
Action / Response
```

The LLM's role is reasoning, planning, and language — not spatial grounding. The spatial grounding is owned by the perception stack and scene graph. This makes the LLM function as a capable reasoning engine without requiring it to solve problems it structurally cannot solve.

## Vision-Language-Action (VLA) Models: The Future Path

The most credible path toward systems that can both understand space and act in it is **Vision-Language-Action models**, which unify perception, reasoning, and action in a single architecture.

### Key VLA Systems (2025–2026)

| Model | Organization | Parameters | Training Data | Capability |
|-------|-------------|------------|---------------|-----------|
| **RT-2** | Google DeepMind | Large | Web-scale + robot demos | Vision + language + manipulation actions |
| **OpenVLA** | Stanford/Berkeley | 7B | 970k robot demonstrations | Open-source; reproducible |
| **π0 (Pi Zero)** | Physical Intelligence | Large | Cross-embodiment fleet | Cross-robot generalization; most advanced |

VLA models are trained on robot interaction data alongside language and vision, giving them a grounded understanding of physical space that text-only LLMs lack.

**Current limitations**:
- Primarily trained for robotic manipulation, not XR spatial assistance
- Large compute requirements; not yet practical for on-device inference
- Limited to manipulation-type actions; not general spatial reasoning
- Require significant fine-tuning to transfer from robotics to XR contexts

**Strategic implication for 9D Technologies / Imagination AI**: VLA models represent the 3–5 year horizon for truly spatially-grounded AI assistants. In the near term (2025–2026), the LLM-as-reasoning-layer-only architecture with explicit SLAM and scene graph layers is the practical path.

## Recent Progress: Closing the Spatial Reasoning Gap

The 2023–2024 research wave has produced concrete evidence that the spatial reasoning gap is closeable — primarily through specialized training data, not architectural changes.

### SpatialVLM: Spatial Reasoning Is a Data Problem

[[SpatialVLM]] (Google DeepMind, 2024) demonstrates that fine-tuning a VLM on 2 billion synthetically-generated spatial QA pairs raises spatial distance estimation accuracy to **75.2%** — surpassing GPT-4V (68%). The key finding: spatial reasoning deficits are primarily a *data scarcity problem*, not an architecture problem. Standard VLM training data is rich in language and 2D semantics but contains almost no examples of metric spatial relationships.

Implication: a domain-specific spatial reasoning model can be built by generating spatial QA from SLAM outputs and scene graphs — no architectural changes needed. See [[synthetic-training-data]].

### 3D-LLM: Injecting 3D Point Clouds into LLMs

[[3D-LLM]] (UCLA/Microsoft, 2023) injects 3D point cloud representations directly into LLM token sequences using differentiable rendering (gradSLAM). It adds **3D location tokens** to the LLM vocabulary, enabling the model to output spatial positions, not just verbal descriptions. Result: +9% BLEU-1 on 3D scene QA benchmarks.

Implication: the LLM-as-reasoning-layer pattern remains correct, but 3D location tokens extend it — the LLM can now emit spatial predictions (navigation waypoints, object locations) that other system layers can act on.

### LEO and EmbodiedScan: The Ego-Centric Path

[[LEO]] demonstrates that a Vicuna-7B model with LoRA fine-tuning can perform spatially-grounded embodied task execution from ego-centric streaming input — across QA, navigation, planning, and manipulation. [[EmbodiedScan]] provides the 760+-category ego-centric dataset to train such models at scale.

These papers define the practical path from "LLMs fail at spatial reasoning" to "LLMs with the right architecture and training data succeed at embodied spatial tasks."

See [[ego-centric-3d-perception]] for the full paradigm picture.

## Strategic Implications

1. **Do not use LLMs for spatial grounding**: Route all spatial understanding through the perception stack. Feed structured spatial context (scene graph, object positions) into the LLM prompt.

2. **Persistent memory is a build problem, not a model problem**: No existing LLM API provides persistent spatial memory. This must be built and is the primary architectural gap.

3. **Gemini is the current best-of-class for spatial tasks**: If the LLM reasoning layer must be chosen, Gemini has the strongest spatial benchmark performance — and native Android XR integration is a practical advantage.

4. **Watch VLA progress closely**: π0 and future open-source VLA models will eventually provide the grounded spatial reasoning that current LLMs cannot. Plan the architecture to allow plugging in a VLA model as the reasoning layer when ready.

## Related pages

- [[spatial-ai-assistant]]
- [[spatial-ai-assistant-architecture]]
- [[slam]]
- [[spatialvlm]]
- [[3d-llm]]
- [[leo]]
- [[embodiedscan]]
- [[ego-centric-3d-perception]]
- [[synthetic-training-data]]
- [[competitive-landscape]]
- [[voice-interaction-spatial]]
