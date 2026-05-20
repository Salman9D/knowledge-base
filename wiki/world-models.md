# World Models

**Summary**: AI systems that learn an internal simulation of how the world changes in response to events and actions — enabling prediction, planning, and synthetic data generation — with WorldGPT representing the first generalist multimodal world model built on a large language model backbone.

**Sources**: `raw/papers/WorldGPT Empowering LLM as Multimodal World Model.pdf`, `Key Trends & Research Pipelines.pdf`, `2_3a_spatial_reasoning_llm_analysis.pdf`

**Last updated**: 2026-04-27

---

## What Is a World Model?

A world model is a system that can answer: **given the current state of the world and an event or action, what will the next state be?**

This is distinct from a perception model (which answers "what is the current state?") and a reasoning model (which answers "what should I do?"). A world model provides the **predictive simulation layer** between perception and decision-making.

The concept originates in cognitive science (Craik, 1943) and reinforcement learning (Sutton & Barto, Dyna architecture), where world models are used to enable planning without physically interacting with the environment — the agent "imagines" the consequences of actions using its internal model before committing to one.

In modern deep learning, world models have evolved from simple next-frame video predictors (Dreamer, PlaNet) to large-scale generalist systems that can predict transitions across arbitrary modality combinations.

## Why World Models Matter for Spatial AI

The [[spatial-ai-assistant]] vision requires more than perceiving the current state of a space. It requires:

1. **Predicting consequences**: "If I move this equipment to the left, what changes in the workflow?"
2. **Counterfactual reasoning**: "What did this room look like before the renovation?"
3. **Scenario simulation**: "If there's a fire, where will the smoke accumulate first?"
4. **Training data generation**: Creating realistic training scenarios without real-world capture

All of these are world model capabilities. The [[llm-spatial-reasoning]] analysis showed that current LLMs fail on spatial reasoning because they have no grounded model of how the physical world behaves. World models provide exactly this grounding.

## WorldGPT: The Generalist Multimodal World Model

[[WorldGPT]] (Zhejiang University, Apr 2024) is the most significant recent advance in world models for spatial AI applications. It extends the world model concept from single-modality video prediction to **any combination of modalities** — text, image, video, and audio — on a 7B LLM backbone.

### What Makes WorldGPT Different

Prior world models:
- **Dreamer / PlaNet**: World models for RL agents; learn latent state transitions; limited to image/action input
- **Genie (Google)**: Foundation world model for interactive 2D environments; image + action → next image
- **World Labs (Lecun group)**: Physical world models; proprietary; focused on physical simulation
- **Video-generation models (Sora, Kling)**: Conditional video synthesis; not designed as prediction/planning tools

WorldGPT's differentiators:
1. **Any-modality I/O**: Input and output can be any combination of text, image, video, audio
2. **LLM backbone**: Built on Vicuna-7B — inherits LLM's reasoning, instruction-following, and in-context learning
3. **Cognitive architecture**: Three-module design (knowledge retrieval, working memory, ContextReflector) mirrors human cognitive processes
4. **Dream tuning**: Can generate its own training data, creating a self-improving data flywheel

### WorldGPT Architecture Summary

```
Current state (any modality combination)
    + Knowledge retrieved from external KB
    + Working memory (recent context)
    ↓ ContextReflector (LLM-state-conditioned Q-Former)
Compressed multimodal representation
    ↓ Vicuna-7B (LoRA)
Predicted next state representation
    ↓ Modality-specific decoders
Next state (any modality)
```

See [[worldgpt]] for the full architectural detail.

## The World Model Taxonomy

Different systems occupy different positions in the world model design space:

| System | Modalities | Backbone | Planning | Open |
|--------|-----------|---------|---------|------|
| **WorldGPT** | Text/Image/Video/Audio | Vicuna-7B (LLM) | Via LLM reasoning | Planned |
| Genie 2 (Google) | Image + actions | Diffusion + Transformer | Yes (controllable) | No |
| World Labs | Image/Video | Proprietary | Physics sim | No |
| Dreamer V3 | Image + actions | CNN + Transformer | RL-based | Yes |
| JEPA (Yann LeCun) | Conceptual | — | Prediction in latent space | Research |

WorldGPT occupies the **language-grounded, multimodal** quadrant — the most flexible but also the least physically precise. For spatial AI applications requiring rich language interaction (not just robotic control), this is the right quadrant.

## Dream Tuning: World Models as Data Generators

The most strategically impactful concept in [[worldgpt]] is **dream tuning** — using a world model to generate synthetic training data for other models. See [[synthetic-training-data]] for the full analysis.

The strategic implication for 9D Technologies:

```
Step 1: Train WorldGPT-like model on available real data (clinical videos, training scenarios)
Step 2: Use trained model to generate synthetic variations:
   - "What if the patient responded differently?"
   - "What if the equipment was positioned differently?"
   - "Generate 1000 variations of this emergency scenario"
Step 3: Use synthetic variations to fine-tune task-specific models
Step 4: Task-specific models achieve ~96% of real-data performance at 1/30th the cost
```

Once the foundation world model is trained, scenario variation becomes essentially free. This is a profound shift in the economics of training simulation: the bottleneck moves from "how do we capture and annotate enough real scenarios?" to "how do we build a sufficiently good foundation world model?"

## Connection to Physical World Simulation

WorldGPT and current LLM-based world models are **statistical** world models — they predict likely next states based on learned patterns, not physical simulation. This is different from **physics-based** world models (game engines, robotics simulators) that compute next states from equations of motion.

The two approaches have complementary strengths:

| | Statistical World Model (WorldGPT) | Physics-Based Simulator |
|--|----------------------------------|------------------------|
| Fidelity | Plausible, not necessarily physical | Physically accurate |
| Coverage | Any scenario in training distribution | Only modeled phenomena |
| Language interaction | Natural ("make the room darker") | Requires API calls |
| Unknown objects | Generalizes from similar objects | Requires explicit modeling |
| Computation | Model inference | Physics simulation step |

For spatial AI assistant applications — where the goal is plausible scenario reasoning and training data generation, not engineering-grade simulation — statistical world models like WorldGPT are likely sufficient and far more flexible.

For safety-critical applications (surgical training with specific instrument forces, structural failure simulation), physics-based simulation remains necessary and statistical world models serve as a complementary layer for high-level scenario planning.

## VLA Models as World Model + Policy

The [[llm-spatial-reasoning]] page covers **Vision-Language-Action (VLA) models** — RT-2, OpenVLA, π0 — as the future path for spatially-grounded AI. VLA models implicitly incorporate a world model:

- They are trained on action sequences where each action leads to a new world state
- The model learns the world model implicitly from the (observation → action → new observation) data
- At inference, the model predicts actions based on its internal understanding of what each action will produce

WorldGPT makes this world model **explicit and queryable** — you can ask WorldGPT "what happens next if action X is taken?" rather than just asking a VLA "what action should I take?"

An emerging research direction: use WorldGPT-style explicit world models to **augment VLA training** — generate synthetic (state, action, next-state) triples for rare or dangerous scenarios that are impossible to collect in the real world.

## Implications for Imagination AI / 9D Technologies

### Near-Term (2025–2026)

1. **Scenario generation for healthcare training**: Fine-tune WorldGPT on clinical video datasets → generate synthetic patient scenario variations → use for VR training without additional real-world capture. See [[xr-simulations-training]] for the healthcare training market context.

2. **"What changed?" queries**: A world model trained on workplace/OR environments can answer "what would this environment look like if equipment X was moved to position Y?" — enabling instructors to design scenario variants from a natural language description.

3. **Prediction as safety feature**: A spatial AI assistant could use a world model to predict likely next events ("the user is approaching the edge of the workspace") and provide proactive guidance.

### Medium-Term (2026–2028)

4. **Self-improving data pipeline**: Initial real-world capture → train world model → dream-tuning generates synthetic expansions → improved model captures better real data → cycle continues.

5. **World model as evaluation harness**: Use the world model to simulate user behavior and test spatial AI assistant responses without requiring real users. Enables rapid iteration on assistant behavior.

### The Central Gap

WorldGPT's ego-centric limitation: it operates on video-level transitions, not on the streaming first-person 3D observations that XR devices produce. Combining WorldGPT's world modeling capability with [[ego-centric-3d-perception]]'s streaming 3D input pipeline is the key missing piece for a truly powerful spatial AI world model.

This is an open research problem as of April 2026. The teams closest to solving it are likely Meta Reality Labs (SceneScript + Aria data infrastructure) and Google DeepMind (Project Astra + Gemini world modeling experiments).

## Related pages

- [[worldgpt]]
- [[synthetic-training-data]]
- [[ego-centric-3d-perception]]
- [[scene-language-models]]
- [[leo]]
- [[llm-spatial-reasoning]]
- [[spatial-ai-assistant-architecture]]
- [[xr-simulations-training]]
- [[xr-trends-research-pipelines]]
