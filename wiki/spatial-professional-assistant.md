# Spatial Professional Assistant

**Summary**: A real-time, persistent productivity tool designed for corporate environments, delivering contextual "profiler" metadata about co-workers and interactions via AR HUD or audio whisper.

**Sources**: `Spatial_AI_Assistant_High-Level_Architecture_2026-04-21.md`, `XR_Productivity_Market_Report_1.4_2025-2026.docx.pdf`, `2_3b_voice_interaction_spatial_context.pdf`, `Key Trends & Research Pipelines.pdf`

**Last updated**: 2026-04-28

---

The **Spatial Professional Assistant (SPA)**—internally referred to as the "Office ctOS"—is an ambient intelligence layer that eliminates "information asymmetry" in the workplace. It transforms the office into a queryable database where people and locations surface their relevant metadata in real time.

## Core Features

### 1. The Profiler HUD
Inspired by the "ctOS" concept from the *Watch Dogs* franchise, this feature provides a heads-up display (HUD) for every person in the user's field of view.
- **Identity Overlay**: Floating name, role, and department.
- **Interaction History**: Summary of the last meeting or email exchange.
- **Social Graph**: Links to shared projects or mutual connections.
- **Availability State**: Real-time status (e.g., "In a meeting," "Focus time ends in 10m").

### 2. Office Recall
A persistent memory layer that allows users to query the physical state of the office over time.
- **Object Retrieval**: "Where did I leave my laptop bag?"
- **Historical Presence**: "Who was using this conference room at 2 PM?"
- **Resource Tracking**: Real-time location of shared prototypes or equipment.

### 3. Ambient Briefing
An audio-first feature for smart glasses (like Meta Ray-Ban AI) that "whispers" context as you approach a person.
- **Example**: *"You're approaching Sarah from Marketing. You owe her a follow-up on the Q3 budget proposal from yesterday's 4 PM email."*

## Technical Foundations

The SPA relies on several emerging research paradigms:
- **[[splatam]]**: For photorealistic, dense 3D mapping of the office that persists across days.
- **[[leo]]**: For ego-centric streaming perception that understands "who is doing what" in real time.
- **[[scenescript]]**: To represent the office as a structured language model for easy querying.
- **[[voice-interaction-spatial]]**: For the low-latency (<600ms) audio whisper pipeline.

## Strategic Moat: Persistent Memory
Current competitors like Google Astra or Apple Scene Understanding are "session-bound"—they forget the world the moment the app closes. The SPA's primary advantage is **Persistent Spatial Memory**, which treats the office as a permanent, shared digital twin (source: [[spatial-ai-assistant-architecture]]).

## Market Strategy

### Primary Verticals
1. **High-Churn Large Enterprises**: Reducing the "onboarding friction" of learning thousands of faces and roles.
2. **Sales & Account Management**: "Superpower" tools for networking events and high-stakes client meetings.
3. **Healthcare/Clinical Labs**: Tracking shared equipment and personnel in high-stress, mobile environments (source: [[healthcare-xr]]).

### Privacy & Ethics
To be viable in an enterprise, the SPA must employ a **"Permission-Based Visibility"** model:
- Users only see data for co-workers who have opted-in.
- Non-consenting individuals are visually "masked" or semantically ignored.
- All biometric profiling is performed **on-device** to prevent centralized surveillance (source: [[9d-technologies-strategic-brief]]).

## Related pages

- [[spatial-ai-assistant]]
- [[spatial-ai-assistant-architecture]]
- [[xr-productivity]]
- [[ego-centric-3d-perception]]
- [[llm-spatial-reasoning]]
- [[9d-technologies-strategic-brief]]
