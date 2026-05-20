# Voice Interaction for Spatial AI

**Summary**: Analysis of voice pipeline architectures for spatial AI assistants — covering generation-by-generation latency comparison, the critical <600ms threshold for immersive XR, recommended stack components, and production readiness assessments for emotion detection, voice cloning, and lip sync.

**Sources**: `2_3b_voice_interaction_spatial_context.pdf`

**Last updated**: 2026-04-24

---

## Why Voice Is Critical for Spatial AI

In an XR context, the user's hands are often occupied and a screen may not exist. Voice is frequently the only natural interaction channel. But voice in XR has a harder requirement than voice on a phone: **latency must be imperceptible**, because any delay in AR/VR breaks the sense of presence and causes cognitive jarring.

## Voice Pipeline Generations

### Gen 1: Text-Only LLM (Baseline)
- Architecture: typed text → LLM → text output
- TTFT (time-to-first-token): varies; not voice-capable
- **Not applicable for voice-first spatial AI**

### Gen 1.5: Cascaded ASR → LLM → TTS
- Architecture: microphone → ASR (Whisper) → LLM → TTS → speaker
- TTFT: **~2500ms** (sum of ASR, LLM inference, TTS)
- Common tools: Whisper + GPT-4o + ElevenLabs
- **Problem**: 2.5s delay is humanly perceptible and breaks XR presence

### Gen 2: Native Speech-to-Speech (S2S)
- Architecture: microphone → native S2S model → speaker (end-to-end)
- TTFT: **200-300ms**
- The model receives audio directly and generates audio output without intermediate text conversion
- **This is the required architecture for immersive spatial AI**

## Latency Thresholds

| Threshold | Meaning |
|-----------|---------|
| **<200ms** | Ideal; below human perception threshold for conversational voice |
| **<600ms** | **Required** for immersive spatial AI — above this, presence breaks |
| **600–1500ms** | Acceptable for non-immersive workflows (smart glasses, background tasks) |
| **>1500ms** | **Failure condition** — users disengage, experience is broken |

(Source: `2_3b_voice_interaction_spatial_context.pdf`)

## Native S2S Model Comparison

| Model | TTFT | Cost | Notes |
|-------|------|------|-------|
| **OpenAI Realtime API** | ~280ms | $0.08/min | Best balance; recommended for production |
| **Gemini Live** | ~280ms | Competitive | Strong spatial context; native Android XR integration |
| **Moshi** (Kyutai) | ~250ms | Self-hosted | Open-source; 18GB VRAM; GPU required |
| **Persona** (Moshi + voice cloning) | ~280ms | Self-hosted | Adds voice cloning to Moshi; best open-source option |
| **ElevenLabs Conversational AI** | Variable | Per-minute | Excellent voice quality but latency degrades with tool calls |

**Recommended**: OpenAI Realtime API ($0.08/min) for cloud deployments. Moshi/Persona for self-hosted setups where data sovereignty or cost at scale matters.

## Critical ElevenLabs Finding

When using ElevenLabs Conversational AI with tool calls (function calls to external systems):

- **1-2 tool calls**: latency stays within acceptable range (~400-600ms)
- **3+ tool calls per turn**: latency spikes to **800-1200ms** — above the 600ms threshold

**Implication**: If using ElevenLabs, keep the agent lean. Decompose complex multi-tool flows into separate turns rather than single complex tool chains. Consider OpenAI Realtime API for tool-heavy use cases.

## Scene Context Injection Architectures

Spatial context (what objects are in the room, where the user is looking, recent spatial events) must reach the voice model. Three approaches:

### 1. System Prompt Injection (Cascaded only)
- Serialize scene graph to JSON; inject into LLM system prompt
- Works with any cascaded LLM
- Limitation: re-serialization overhead; not usable with native S2S models directly

### 2. Hybrid Dual-Channel (Persona/Moshi architecture)
- Dedicated scene-context channel alongside the audio stream
- Audio channel: voice interaction
- Context channel: continuous structured spatial state updates
- **Recommended for native S2S + rich spatial context**

### 3. WavRAG (Voice-Augmented Retrieval)
- Retrieves relevant spatial memories as audio embeddings
- Matches voice queries to spatial memory store without ASR intermediate step
- Early-stage; not yet production-ready

## Voice Cloning: Sesame CSM 1B

For spatial AI assistants that require a branded or persona voice (e.g., a consistent voice identity for a training assistant):

**Recommended**: **Sesame CSM 1B** (Character Speech Model)
- Fastest inference on Google Colab T4 GPU
- Production-quality voice cloning from short reference audio (~30 seconds)
- Commercial-friendly licensing
- Lower compute requirement vs. XTTS, StyleTTS2

**Second option**: **Qwen3TTS**
- Runs on CPU (no GPU required)
- Slightly lower quality than Sesame CSM 1B but more accessible deployment

**Not recommended for production**: OpenVoice, XTTS v2 (licensing/quality tradeoffs)

## Lip Sync: Salsa

For XR contexts where an avatar or virtual assistant character requires lip sync with generated speech:

**Recommended**: **Salsa**
- Near-zero additional latency (on-device inference)
- Commercial license covers 7 phoneme blend shapes
- Designed specifically for real-time XR avatar use
- Integrates with Unity and Unreal Engine

**Not recommended**: OVRLipSync (latency), SadTalker (video-only, not real-time)

## Emotion Detection: Not Production-Ready

A common request for spatial AI assistants is detecting the user's emotional state from voice to adapt responses. **As of April 2026, this is not production-ready** with any general-purpose audio model.

**Why**:
- State-of-the-art audio emotion classifiers achieve ~65-70% accuracy on clean lab recordings
- In real XR environments (background noise, microphone variation, non-native accents), accuracy drops to ~50-55%
- Models exhibit strong demographic bias (gender, dialect, age)
- No standardized emotion taxonomy across models makes results incomparable

**Practical guidance**: Do not include emotion detection in the initial product architecture. Design the system to be emotion-aware through explicit user signals (feedback, correction, pacing) rather than implicit audio inference.

## Recommended Stack (2026)

| Component | Recommended Tool | Notes |
|-----------|-----------------|-------|
| **Voice pipeline** | OpenAI Realtime API | Best TTFT + tool call reliability |
| **Fallback / self-hosted** | Moshi + Persona | 18GB VRAM requirement |
| **Voice cloning** | Sesame CSM 1B | Fastest on T4; commercial license |
| **Lip sync** | Salsa | Near-zero latency; XR-native |
| **Scene context injection** | Hybrid dual-channel | For S2S with rich spatial state |
| **Voice retrieval** | WavRAG | Future-state; not yet production |
| **Emotion detection** | Skip for v1 | Not production-ready |

## Implications for 9D Technologies / Imagination AI

1. **Target <600ms end-to-end**: From user utterance to first audio response. This requires native S2S (Gen 2 pipeline) — cascaded architecture cannot reliably hit this threshold.

2. **Budget tool call latency**: Each tool call adds ~200-400ms. With ElevenLabs, hitting 3+ calls exceeds the threshold. Design agent flows to minimize sequential tool chains.

3. **Voice identity matters for training XR**: A consistent voice persona improves user trust and recall in training applications. Sesame CSM 1B gives 9D Technologies the ability to deploy a consistent branded voice at low compute cost.

4. **Lip sync is a presence multiplier**: For avatar-based training scenarios, adding Salsa lip sync dramatically improves perceived intelligence even without changing the underlying voice model.

## Related pages

- [[spatial-ai-assistant]]
- [[spatial-ai-assistant-architecture]]
- [[llm-spatial-reasoning]]
- [[ai-npc-platforms]]
- [[xr-hardware]]
