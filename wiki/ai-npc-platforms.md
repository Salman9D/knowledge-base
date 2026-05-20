# AI NPC Platforms

**Summary**: Real-time conversational AI platforms (Convai, Inworld AI) that power AI-driven non-player characters in XR environments — the runtime engine for adaptive training scenarios and intelligent spatial agents.

**Sources**: `AR_VR_Software_Services_GenAI_Avatar_Animation_Report_1.1_.docx.pdf`, `Spatial_AI_Assistant_High-Level_Architecture_2026-04-21.md`

**Last updated**: 2026-04-24

---

## What AI NPC Platforms Do

AI NPC platforms provide the conversation and behavior layer that makes virtual characters in XR feel responsive and intelligent. Unlike scripted dialogue systems, they allow characters to respond naturally to freeform voice or text input, adapt their behavior, and maintain contextual memory within a session.

For XR training specifically, AI NPCs enable:
- **Adaptive scenario branching**: Scenarios that evolve based on how the learner responds
- **Freeform conversation practice**: Trainees practice patient communication, customer service, or clinical interviews with characters who behave realistically
- **Real-time feedback**: NPCs can break character to coach the learner, then resume the scenario
- **Infinite variation**: No two training runs are identical — key for skill generalization

## Key Platforms

| Platform | Focus | Voice Support | Memory | Integration |
|----------|-------|--------------|--------|-------------|
| **Convai** | Game/XR NPCs | Yes (real-time) | Session-level | Unity, Unreal, REST API |
| **Inworld AI** | Enterprise/game NPCs | Yes (real-time) | Persistent character memory | Unity, Unreal, REST API |

### Convai

- Specializes in real-time conversational AI for game and XR characters
- End-to-end pipeline: speech recognition → LLM reasoning → TTS → lip sync
- Low latency optimized for interactive XR; supports custom character personalities
- Available via API and Unity/Unreal SDK
- Referenced in `Spatial_AI_Assistant_High-Level_Architecture_2026-04-21.md` as the prototype-phase memory/reasoning backend for Quest 3 builds

### Inworld AI

- Enterprise-grade NPC platform with persistent character memory (remembers prior interactions)
- Supports "goals and motivations" system — characters behave purposefully, not just responsively
- Safety layer for enterprise/healthcare use cases (filters inappropriate content)
- Used by Unity and game studios; increasingly adopted for enterprise simulation
- Acquired by Google (2024) — future integration with Gemini native possible

## Strategic Position for 9D Technologies

Both platforms are available via API today and slot directly into the [[spatial-ai-assistant-architecture]] Reasoning & Planning layer (Layer 4) for prototype builds.

**Recommended path** (from `Spatial_AI_Assistant_High-Level_Architecture_2026-04-21.md`):
- **Prototype phase**: Quest 3 + Unity → Convai or Inworld for NPC reasoning → GPT-4o for complex scenario logic
- **Enterprise phase**: Custom fine-tuned model replacing the third-party NPC platform, trained on domain-specific scenarios

**Key differentiation**: Neither Convai nor Inworld AI includes spatial awareness — they operate on text/voice only and have no knowledge of where the learner is in 3D space, what they're looking at, or how they're moving. This is the gap that [[spatial-ai-assistant]] fills: adding spatial context (from [[slam]] and [[arkit-scene-understanding]]/[[meta-scene-api]]) to the NPC reasoning pipeline.

## Competitive Risk

Inworld AI's acquisition by Google means it may become a native capability of Android XR / Gemini. If Google integrates Inworld deeply into the Android XR platform, third-party NPC platforms lose distribution leverage. This reinforces the case for 9D Technologies owning the spatial context layer (not easily replicated by platform NPC integrations) rather than competing on conversational AI alone.

## Related pages

- [[genai-animation]]
- [[xr-simulations-training]]
- [[spatial-ai-assistant]]
- [[spatial-ai-assistant-architecture]]
- [[xr-platforms]]
