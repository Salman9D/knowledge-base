# Wiki Log

Append-only record of all wiki operations.

---

## 2026-04-15 — Initial wiki build

**Operation**: Full wiki creation from scratch

**Sources ingested (23 total)**:
- `ARVR_XR_Market_Combined.md`
- `ARVR_XR_Market_2024.md`
- `ARVR_XR_Market_2025.md`
- `ARVR_XR_Market_2026-2030_Projection.md`
- `XR_Competitive_Landscape_Matrix.md`
- `XR_Competitive_Landscape_Major_Players.md`
- `Spatial_AI_Assistant_Report_2.1.docx.pdf`
- `XR_Productivity_Market_Report_1.4_2025-2026.docx.pdf`
- `XR_Simulations_Strategic_Intelligence_Report_1.4_2024-2030.pdf`
- `Competitive Landscape for Spatial AI Assistants.pdf`
- `AR_VR_Hardware_Market_Analysis_Spatial_Mapping_Technologies_Report_1.1_.docx.pdf`
- `AR_VR_Software_Services_GenAI_Avatar_Animation_Report_1.1_.docx.pdf`
- `Major players across Hardware, Softwares and AI.pdf`
- `VR GAMES 2026.pdf`
- `AR IN HEALTHCARE.pdf`
- `Global Spatial Computing Market Analysis (2024–2030).pdf`
- `10 best examples and use cases of augmented reality in healthcare.pdf`
- `VR simulations for medical students and HCPs_ learning in a 3D world.pdf`
- `s12909-024-06402-1.pdf` (Minouei et al., BMC Medical Education 2024)
- `ijerph-19-00464.pdf` (Vianez et al., IJERPH 2022)
- `sustainability-16-08520-v2.pdf` (Sung et al., Sustainability 2024)
- `s12909-025-07402-5.pdf` (Hammouda et al., BMC Medical Education 2025)
- `AR_VR_XR_Market_Combined.md` (same as first, deduplicated)

**Pages created**:
- `wiki/index.md` — master table of contents
- `wiki/log.md` — this file
- `wiki/spatial-ai-assistant.md`
- `wiki/market-size-overview.md`
- `wiki/competitive-landscape.md`
- `wiki/xr-hardware.md`
- `wiki/xr-platforms.md`
- `wiki/xr-productivity.md`
- `wiki/xr-simulations-training.md`
- `wiki/healthcare-xr.md`
- `wiki/vr-healthcare-evidence.md`
- `wiki/vr-gaming.md`
- `wiki/digital-twins.md`
- `wiki/genai-animation.md`
- `wiki/slam.md`

**Summary**: Full initial ingestion of 23 source documents spanning market research reports, competitive analyses, clinical studies, and technology assessments. Created 15 wiki pages covering all major themes.

---

## 2026-04-15 — Strategic Brief Compilation

**Operation**: Created synthesis document `wiki/9d-technologies-strategic-brief.md`

**Pages modified**:
- `wiki/9d-technologies-strategic-brief.md` — created (new)
- `wiki/index.md` — added "Strategic Briefs" section with link to brief
- `wiki/log.md` — this entry

**Summary**: Compiled all 15 wiki pages and 23 source documents into a single cohesive strategic brief for 9D Technologies. Document includes: executive summary, 5 key market insights, competitive landscape with threat ratings, opportunity matrix (6 verticals × 4 dimensions), phased 18-month roadmap, and a risk register. Primary recommendation: healthcare clinical skills training as lead vertical, AI NPC prototype as immediate next action.

---

## 2026-04-21 — New Source Ingestion

**Operation**: Ingested new source document

**Sources ingested (1 total)**:
- `Spatial_AI_Assistants_Landscape_2026-04-21.md`

**Pages modified**:
- `wiki/spatial-ai-assistant.md` — added 2026 landscape section with updated player table and new gaps
- `wiki/competitive-landscape.md` — added Rabbit, Humane AI Pin, and AskUI profiles

**Pages created**:
- `wiki/google-gemini-smart-glasses.md` — new product entry for Google Gemini glasses
- `wiki/meta-rayban-ai-glasses.md` — new product entry for Meta Ray-Ban AI glasses
- `wiki/index.md` — added new pages to table of contents

**Summary**: Added April 2026 spatial AI assistant landscape covering 7 major players (Google, Apple, Meta, Rabbit, Humane, AskUI, Emerging). Confirmed original whitespace thesis and added new gap analysis around form factor tradeoffs and privacy concerns.

---

## 2026-04-21 — Scene Understanding Source Ingestion

**Operation**: Ingested new source document

**Sources ingested (1 total)**:
- `Scene_Understanding_Object_Recognition_Landscape_2026-04-21.md`

**Pages modified**:
- `wiki/slam.md` — added Scene Understanding & Object Recognition section
- `wiki/index.md` — added new pages to table of contents

**Pages created**:
- `wiki/arkit-scene-understanding.md` — Apple ARKit capabilities
- `wiki/meta-scene-api.md` — Meta Scene API for persistent spatial models
- `wiki/google-scene-semantics.md` — Google Scene Semantics pixel-level labeling
- `wiki/open-source-scene-understanding.md` — SAM, GroundingDINO, YOLO-World models

**Summary**: Added scene understanding and object recognition landscape covering platform APIs (ARKit, Meta Scene API, Google Scene Semantics) and open-source models. Extended SLAM page with semantic layer comparison. Total wiki now has 21 pages.

---

## 2026-04-21 — Architecture Source Ingestion

**Operation**: Ingested new source document

**Sources ingested (1 total)**:
- `Spatial_AI_Assistant_High-Level_Architecture_2026-04-21.md`

**Pages modified**:
- `wiki/spatial-ai-assistant.md` — replaced Technical Architecture section with 7-layer architecture and Mermaid diagram
- `wiki/index.md` — added architecture page to Core Strategic Pages

**Pages created**:
- `wiki/spatial-ai-assistant-architecture.md` — dedicated page with full 7-layer architecture, component details, on-device vs cloud deployment table, data flow, and build recommendations for Imagination AI and 9D Technologies

**Summary**: Added comprehensive architecture blueprint for Spatial AI Assistant. Architecture includes: Environment Perception, Spatial Memory, Multimodal Interaction, Reasoning & Planning, Action & Execution, AR Overlay, and Security Framework. Includes explicit on-device vs cloud deployment breakdown. Total wiki now has 22 pages.

This ingestion completes the "why, what, how" package: problem definition (whitespace), market validation (training market), and technical architecture (build path).

---

## 2026-04-24 — New Source Ingestion (3 files)

**Operation**: Ingested three new source documents

**Sources ingested**:
- `Durrant-Whyte_Bailey_SLAM-tutorial-I.pdf` — Foundational IEEE SLAM tutorial (Durrant-Whyte & Bailey)
- `What does virtual reality and the metaverse mean for training.pdf` — PwC VR soft skills training efficacy study (2020/2022)
- `s41598-026-46629-0_reference.pdf` — Cui et al. 2026, SuperDynaSLAM, *Scientific Reports* (Article in Press)

**Pages modified**:
- `wiki/slam.md` — Added "Algorithmic Foundations" section (EKF-SLAM, FastSLAM, probabilistic formulation from Durrant-Whyte tutorial) and "Deep Learning SLAM: Handling Dynamic Environments" section (SuperDynaSLAM architecture, results, strategic implications)
- `wiki/xr-simulations-training.md` — Added "VR vs. Traditional Training: PwC Efficacy Data" section with headline outcome stats (4x speed, 275% confidence, 3.75x emotional connection), cost curve breakpoints, and adoption context

**Pages created**: None (all content integrated into existing pages)

**Summary**: Added algorithmic depth to the SLAM page (now covers probabilistic formulation, EKF-SLAM, FastSLAM, and 2026 deep learning SLAM for dynamic environments). Strengthened the XR training page with the strongest independently published VR efficacy dataset. Total wiki remains 22 pages.

---

## 2026-04-24 — Wiki Lint Pass

**Operation**: Full lint audit and fix of all 22 wiki pages

**Issues fixed (9 total)**:

1. **Broken table** — `wiki/spatial-ai-assistant-architecture.md`: Restored 3-column structure in On-Device vs. Cloud table; "Spatial Memory &" and "Reasoning &" rows had missing `|` separators
2. **YAML frontmatter removed** — `wiki/9d-technologies-strategic-brief.md`: Stripped non-standard `---/title:/type:/tags:` block; page now opens with standard `# heading`
3. **Stale source count updated** — `wiki/9d-technologies-strategic-brief.md`: "23" → "26" ingested sources (two occurrences); Last updated → 2026-04-24; PwC VR Efficacy Study row added to Insight 2 evidence table
4. **Typo fixed** — `wiki/meta-scene-api.md`: "Smoothpassthrough" → "Smooth passthrough"
5. **Orphan resolved** — `wiki/vr-gaming.md`: Added `[[vr-gaming]]` to Related pages in `wiki/competitive-landscape.md`
6. **Unconfirmed launch date flagged** — `wiki/xr-platforms.md`: Samsung Project Moohan "2025" now marked *(launch date unconfirmed in ingested sources as of 2026-04-24)*
7. **Unsourced chip claim flagged** — `wiki/xr-hardware.md`: Apple Vision Pro M5 chip claim now marked *(chip model unconfirmed in ingested sources)*
8. **Missing concept page created** — `wiki/ai-npc-platforms.md` (new): Covers Convai and Inworld AI as real-time AI NPC platforms; linked from `genai-animation.md`, `xr-simulations-training.md`, and `index.md`
9. **Disambiguation note added** — `wiki/xr-simulations-training.md`: Clarifies PwC data (soft skills, 2020) is distinct from XR Simulations Report data (procedural/technical skills)

**Pages modified**:
- `wiki/spatial-ai-assistant-architecture.md`
- `wiki/9d-technologies-strategic-brief.md`
- `wiki/meta-scene-api.md`
- `wiki/competitive-landscape.md`
- `wiki/xr-platforms.md`
- `wiki/xr-hardware.md`
- `wiki/xr-simulations-training.md`
- `wiki/genai-animation.md`
- `wiki/index.md`
- `wiki/log.md`

**Pages created**:
- `wiki/ai-npc-platforms.md` — new concept page

**Summary**: All 9 lint issues resolved. Wiki now has 23 pages. No contradictions introduced; all changes are corrections, clarifications, or additions consistent with ingested sources.

---

## 2026-04-24 — New Source Ingestion (4 source groups, 47 files)

**Operation**: Ingested 3 PDFs + 44 Discord daily landscape summaries (Mar 11 – Apr 24, 2026)

**Sources ingested**:
- `2_3a_spatial_reasoning_llm_analysis.pdf` — 9D Technologies AI Research (23 pages): LLM spatial reasoning benchmarks, VLA models
- `2_3b_voice_interaction_spatial_context.pdf` — Internal Research April 2026 (16 pages): voice pipeline latency, S2S architectures, recommended stack
- `Spatial AI Assistant – High-Level Architecture.pdf` — 10 pages: scene graph architecture, <100ms latency spec, on-device vs cloud split
- `discord-daily-summaries/2026-03-11` through `2026-04-24` — 44 daily landscape summaries (note: 2026-03-11 is internal meeting prep, not a landscape summary; skipped for ingestion)

**Pages created (3)**:
- `wiki/llm-spatial-reasoning.md` — LLM spatial reasoning benchmarks (GPT-4o 27.5% viewpoint accuracy), 6 failure patterns, VLA models (RT-2, OpenVLA, π0), LLM-as-reasoning-layer architecture recommendation
- `wiki/voice-interaction-spatial.md` — Voice pipeline generations (Gen 1.5 cascaded ~2500ms vs Gen 2 S2S 200-300ms), <600ms XR threshold, ElevenLabs 3+ tool call latency issue, recommended stack table, Sesame CSM 1B voice cloning, Salsa lip sync, emotion detection not production-ready
- `wiki/xr-market-signals-2026.md` — Synthesis of 44 daily summaries into 9 major market signals: smart glasses momentum (7M+ sold in 2025, +44.4% XR shipments), VR social economics (Rec Room shutdown, studio casualties), Samsung Galaxy XR launch ($1,799), Android XR maturation, Vision Pro enterprise niches, platform refinement (FrameSync, Pico Swan, Steam Frame), OpenXR ecosystem, Quest price hike, market size data

**Pages modified (9)**:
- `wiki/spatial-ai-assistant-architecture.md` — Added Scene Graph Architecture section, <100ms latency spec, on-device vs cloud split table from architecture PDF; added links to new pages
- `wiki/xr-platforms.md` — Added visionOS 26.4/26.5 foveated streaming + enterprise updates; Meta FrameSync + Horizon Worlds reversal + Quest price hike; Samsung Galaxy XR launch + Android XR auto-spatialization + 100+ apps + enterprise MDM; VDXR runtime; Gucci × Google glasses
- `wiki/xr-hardware.md` — Added Samsung Galaxy XR $1,799 launch specs; Meta Ray-Ban prescription glasses $499; VITURE Beast XR; Pico Project Swan; Valve Steam Frame; Samsung/Snap smart glasses pipeline; XREAL 1S; Lynx liquidation; price gap update
- `wiki/competitive-landscape.md` — Added VLA models section (RT-2, OpenVLA, π0) as emerging intelligence layer; Meta Reality Labs ~$80B loss update; Google Galaxy XR launch update; links to llm-spatial-reasoning + xr-market-signals-2026
- `wiki/market-size-overview.md` — Added 2026 signals section: +44.4% XR shipments YoY, $210.96B AR market 2026, $3.81B SoC market, $41.5B→$145B CAGR 19.6%, 100k+ Galaxy XR projection; link to xr-market-signals-2026
- `wiki/vr-gaming.md` — Added Rec Room shutdown (150M users, $3.5B valuation, Jun 1, 2026); VR studio casualties table (nDreams, Polyarc, Kluge, Red Storm); Quest -16% sales + +13% in-app + Horizon+ 1M subs; updated what works vs what doesn't
- `wiki/slam.md` — Added note on why persistent memory cannot be replaced by LLMs (GPT-4o 27.5% viewpoint accuracy); linked to llm-spatial-reasoning
- `wiki/index.md` — Added "AI Research" and "Market Intelligence" sections with 3 new pages; updated Last updated
- `wiki/log.md` — This entry

**Summary**: Ingested 47 new source files. Created 3 new wiki pages (LLM spatial reasoning, voice interaction, 2026 market signals). Updated 9 existing pages with data from the new sources. Wiki now has **26 pages** and covers the full technical and market landscape through April 24, 2026. The key new insight confirmed across all sources: persistent spatial memory is the central gap that no current product fills — it is architectural, cannot be solved by LLM scaling alone, and remains the core opportunity for Imagination AI and 9D Technologies.

---

## 2026-04-24 — New Source Ingestion (2 files, ingestion pass 3)

**Operation**: Ingested two new source documents

**Sources ingested**:
- `Key Trends & Research Pipelines.pdf` — 9D Technologies AI Research (16 pages): 9 industry trends, research pipelines for Meta/Google/Apple/NVIDIA, academic labs, 10 key papers
- `Market Size & Growth.pdf` — 9D Technologies AI Research (8 pages): overall market projections ($55.69B 2024 → $462.57B 2030), by-segment/vertical/region breakdowns, hardware install base, competitive market share, mobile AR users, key analyst forecasts

**Pages created (1)**:
- `wiki/xr-trends-research-pipelines.md` — 9 industry trends (On-Device AI, Spatial Computing Convergence, GenAI for 3D, Passthrough MR, Voice-First, Agentic AI, Smart Glasses, Real-Time 3D Reconstruction, Privacy-First), research pipeline detail for Meta (Codec Avatars, Ego4D, Project Aria, Orion), Google (Project Astra as primary competitor), Apple (RoomPlan, ARKit 7, on-device LLM), NVIDIA (GR00T, Omniverse, CloudXR), 8 academic labs, 10 key papers table (SpatialVLM, 3D-LLM, SplaTAM, ConceptFusion, LEO, GaussianEditor, Depth Anything V2, EmbodiedScan, SceneScript, WorldGPT)

**Pages modified (5)**:
- `wiki/market-size-overview.md` — Added full 9D Technologies internal research section: $55.69B→$462.57B overall, by-technology table (AR/VR/MR with CAGRs), by-vertical table (10 verticals with CAGRs), IDC hardware install base forecast (10M→41M units 2024-2029), Counterpoint market share Q3 2025 (Meta 57%), mobile AR users (983M→1,187M), key analyst forecasts (Goldman Sachs, McKinsey, Counterpoint)
- `wiki/competitive-landscape.md` — Added Project Astra callout as primary competitive reference; added `Key Trends & Research Pipelines.pdf` to sources; linked to xr-trends-research-pipelines
- `wiki/genai-animation.md` — Replaced early-stage text-to-3D section with 2026 production-ready table (Meshy v3, Rodin Gen-2, Meta 3D Gen, InstantMesh, Genie 2, World Labs, GaussianEditor); updated Last updated date
- `wiki/slam.md` — Added 3D Gaussian Splatting section: SplaTAM architecture, comparison table (traditional vs 3DGS maps), GaussianEditor, strategic implications for persistent spatial memory
- `wiki/index.md` — Added xr-trends-research-pipelines to AI Research section; updated Last updated to pass 3

**Summary**: Added 2 internal research documents. Created 1 new wiki page covering trends and research pipelines. Updated 5 existing pages. Wiki now has **27 pages**. Key new insights: Project Astra confirmed as primary competitor with 3 specific gaps (cloud-only, no persistent cross-device map, no action execution); GenAI for 3D has crossed production threshold (Meshy v3 in 60 seconds); 3DGS via SplaTAM is the photorealistic alternative to geometric SLAM for persistent spatial memory; Education/Training (38% CAGR) + Healthcare (35% CAGR) confirmed as top-growth verticals for Spatial AI Assistant.

---

## 2026-04-27 — New Source Ingestion (10 academic papers, ingestion pass 4)

**Operation**: Ingested 10 academic papers from `raw/papers/`

**Sources ingested**:
- `SpatialVLM Endowing Vision-Language Models with Spatial Reasoning Capabilities.pdf` — Google DeepMind, 2024
- `3D-LLM Injecting the 3D World into Large Language Models.pdf` — UCLA/Microsoft, 2023
- `SplaTAM Splat Track and Map 3D Gaussians for Dense RGB-D SLAM.pdf` — CMU, 2024
- `ConceptFusion Open-set Multimodal 3D Mapping.pdf` — MIT/CMU, 2023
- `An Embodied Generalist Agent in 3D World.pdf` — Zhejiang/Shanghai AI Lab, 2023
- `GaussianEditor Swift and Controllable 3D Editing based on Gaussian Splatting.pdf` — ETH Zurich/BIT, 2023
- `Depth Anything V2.pdf` — HKU/ByteDance, 2024
- `EmbodiedScan A Holistic Multi-Modal 3D Perception Suite Towards Embodied AI.pdf` — Shanghai AI Lab, Dec 2023
- `SceneScript Reconstructing Scenes With An Autoregressive Structured Language Model.pdf` — Meta Reality Labs, Mar 2024
- `WorldGPT Empowering LLM as Multimodal World Model.pdf` — Zhejiang University, Apr 2024

**Pages created (14)**:

*Paper summaries*:
- `wiki/spatialvlm.md` — SpatialVLM: 2B synthetic spatial QA pairs, 75.2% vs GPT-4V 68%, spatial reasoning is a data problem
- `wiki/3d-llm.md` — 3D-LLM: 3D point clouds injected into LLMs, 3D location tokens, +9% BLEU-1, 300K 3D-language pairs
- `wiki/splatam.md` — SplaTAM: first dense 3DGS SLAM, 0.6cm ATE RMSE, 400 FPS rendering, silhouette-guided densification
- `wiki/conceptfusion.md` — ConceptFusion: CLIP+DINO+SAM → any-modality queryable 3D maps, >40% mIoU zero-shot
- `wiki/leo.md` — LEO: embodied generalist agent, Vicuna-7B + LoRA, two-stage training, O-CoT data generation
- `wiki/gaussianeditor.md` — GaussianEditor: text-driven 3DGS editing, Gaussian semantic tracing, HGS, 5–10 min/edit
- `wiki/depth-anything-v2.md` — Depth Anything V2: synthetic-to-real pipeline, 97.1% δ₁ vs Marigold 86.8%, edge variants
- `wiki/embodiedscan.md` — EmbodiedScan: 5K+ scans, 1M prompts, 760+ categories, SAM-assisted annotation, linear scaling
- `wiki/scenescript.md` — SceneScript: scenes as structured language commands, F1@5cm 0.903 vs 0.139, 2–5s inference, extensible
- `wiki/worldgpt.md` — WorldGPT: generalist world model, progressive training, ContextReflector, dream tuning 30× cheaper

*Concept pages*:
- `wiki/scene-language-models.md` — The paradigm of representing 3D scenes as language sequences; SceneScript as primary example; strategic implications
- `wiki/synthetic-training-data.md` — Five synthetic data techniques across papers; dream tuning as centrepiece; 30× cost reduction analysis
- `wiki/ego-centric-3d-perception.md` — The shift to streaming first-person 3D perception; EmbodiedScan + SceneScript + LEO + ConceptFusion unified
- `wiki/world-models.md` — World models for spatial AI; WorldGPT architecture; dream tuning economics; gap to ego-centric XR

**Pages modified (7)**:
- `wiki/slam.md` — Added SplaTAM page link; linked GaussianEditor; added ConceptFusion semantic mapping section; expanded Related pages
- `wiki/llm-spatial-reasoning.md` — Added "Recent Progress" section covering SpatialVLM, 3D-LLM, LEO/EmbodiedScan as gap-closing evidence; expanded Related pages
- `wiki/open-source-scene-understanding.md` — Added ConceptFusion as the leading synthesis of open-source models; expanded Related pages
- `wiki/xr-trends-research-pipelines.md` — Updated 10 Key Papers table with wiki links to all paper pages and updated descriptions with key metrics; added concept pages to Related pages
- `wiki/genai-animation.md` — Linked GaussianEditor table entry to [[gaussianeditor]] wiki page
- `wiki/index.md` — Added "Research Papers (Ingestion Pass 4)" and "Research Concept Pages" sections with 14 new entries; updated Last updated
- `wiki/log.md` — This entry

**Key cross-cutting themes surfaced from this ingestion**:

1. **The ego-centric turn**: EmbodiedScan, SceneScript, LEO, ConceptFusion all shift from global pre-built scans to streaming first-person 3D perception — the paradigm that matches XR headset deployment reality

2. **Gaussian Splatting as new 3D backbone**: SplaTAM (capture/mapping) + GaussianEditor (editing) form a complete pipeline for photorealistic persistent spatial maps with visual change detection

3. **Scene language models**: SceneScript demonstrates that representing scenes as autoregressive language sequences outperforms geometric reconstruction by 6.5× and is extensible without retraining — a qualitative architectural shift

4. **Synthetic data unlock**: SpatialVLM (2B QA from maps), Depth Anything V2 (97.1% from synthetic → pseudo-label), SceneScript (100K synthetic scenes), WorldGPT dream tuning (30× cheaper) — all four demonstrate near-real-data performance from synthetic sources

**Summary**: Ingested 10 academic papers from `raw/papers/`. Created 14 new wiki pages (10 paper summaries + 4 concept pages). Updated 7 existing pages. Wiki now has **42 pages**. The core insight from this pass: the spatial AI capability stack is largely assembled from available research — SplaTAM (mapping), ConceptFusion (semantics), SceneScript (language interface), SpatialVLM/3D-LLM (LLM grounding), LEO (embodied agency), Depth Anything V2 (depth without sensors). The engineering problem for Imagination AI / 9D Technologies is integration and productionization, not research breakthroughs.

---

## 2026-04-28 — "Office ctOS" Concept Development

**Operation**: Formulated Spatial Professional Assistant (SPA) product concept and updated architecture

**Pages modified**:
- `wiki/spatial-ai-assistant-architecture.md` — Added "Real-Time 'ctOS' Interface (The Profiler HUD)" section detailing identity anchoring, semantic proximity triggers, and the "Ghost Layer" deployment tiers.
- `wiki/index.md` — Added `[[spatial-professional-assistant]]` to Core Strategic Pages; updated Last updated date.

**Pages created**:
- `wiki/spatial-professional-assistant.md` — Dedicated concept page for the "Office ctOS" / SPA. Covers core features (Profiler HUD, Office Recall, Ambient Briefing), technical foundations (SplaTAM, LEO, SceneScript), and privacy-first marketing strategy.

---

## 2026-04-30 — New Source Ingestion (Market Analysis V2)

**Operation**: Ingested comprehensive updated market analysis and created smart glasses concept page.

**Sources ingested (1 total)**:
- `AR & VR Market Size Analysis V2 35108ff66bbf8049b947d8195a624a90.md` — Updated projections (2025–2033), category framework, and opportunity rankings.

**Pages created (1)**:
- `wiki/smart-glasses.md` — Dedicated page for the AI-first eyewear segment; covers the 44% shipment growth in 2025 and strategic shift away from traditional headsets.

**Pages modified (4)**:
- `wiki/market-size-overview.md` — Updated with 2025/2033 projections ($1.05T AR market), new V2 category framework, and consolidated opportunity rankings.
- `wiki/xr-hardware.md` — Added section on "The Great Form Factor Shift" and updated market signals regarding smart glasses growth and headset declines.
- `wiki/xr-productivity.md` — Refined the "Collaboration" section to reflect the failure of general-purpose VR collaboration and the pivot to vertical-specific workflows.
- `wiki/competitive-landscape.md` — Updated Meta's 2025 performance ($2.2B revenue, 72.2% market share) and added Snap as a hidden AR leader.
- `wiki/index.md` — Added `[[smart-glasses]]` to Market Segments and updated Last updated date.

**---

## 2026-04-30 — New Source Ingestion (Competitive & Opportunity Analysis)

**Operation**: Ingested comprehensive competitive landscape and opportunity analysis reports.

**Sources ingested (2 total)**:
- `Competitive Landscape 35208ff66bbf8085b5cecc199075a2df.md` — Three-layer market structure, 2025 revenue data (Meta, Apple, Google, Snap, NVIDIA, etc.), and frontier builder profiles.
- `Opportunity Analysis 35208ff66bbf80c9aca3e79e4879e60b.md` — Ranked 10-point opportunity matrix, Horizon 1/2/3 roadmap, and detailed sub-segment market sizing (Navigation, Retail).

**Pages created (3)**:
- `wiki/xr-trust-and-safety.md` — Addressing the 70%+ privacy concern as a software opportunity.
- `wiki/niantic-spatial.md` — Frontier builder profile (LGM, VPS, 30B images).
- `wiki/world-labs.md` — Frontier builder profile (Fei-Fei Li, $1B raise, spatial intelligence).

**Pages modified (5)**:
- `wiki/competitive-landscape.md` — Completely restructured into Platforms, Specialists, and Enablers; added 2025 financial data.
- `wiki/market-size-overview.md` — Integrated sub-market CAGRs (Navigation 39%, Retail 32%) and consumer demand signals.
- `wiki/9d-technologies-strategic-brief.md` — Overhauled roadmap to Horizon model; integrated ranked opportunity matrix.
- `wiki/xr-productivity.md` — Added "Field Workflow Copilot" as the #1 ranked enterprise opportunity.
- `wiki/index.md` — Added 3 new pages and updated last updated date.

---

## 2026-04-30 — Full Opportunity Ingestion (Pass 6.1)

**Operation**: Fully ingested all 10 opportunities from the Opportunity Analysis report.

**Pages created (1)**:
- `wiki/opportunity-analysis.md` — Complete 10-point ranked matrix detailing product logic, strategic value, and capability scoring for every identified opportunity.

**Pages modified (2)**:
- `wiki/index.md` — Added opportunity-analysis to Core Strategic Pages.
- `wiki/9d-technologies-strategic-brief.md` — Integrated explicit reference to the full 10-point matrix.

**Summary**: Ensured 100% ingestion of the Opportunity Analysis source, covering lower-ranked but strategically relevant vectors like AR Commerce, Spatial Notes, and Education Tutoring. Wiki now has **47 pages**.

---

## 2026-05-06 — New Source Ingestion (Monthly Brief, Pass 7)

**Operation**: Ingested leadership alignment meeting record

**Sources ingested (1 total)**:
- `Monthly Brief with Moiz 05-05-2026.md` — Dreamverse monthly debrief, May 05 2026 (57 min session with Moiz)

**Pages created (1)**:
- `wiki/monthly-brief-2026-05-05.md` — Full meeting record: B2C→B2B pivot decision, data moat thesis, vertical selection criteria, 4 named candidate verticals, action items, strategic constraints

**Pages modified (4)**:
- `wiki/9d-technologies-strategic-brief.md` — Added "Strategic Direction Update" section at top with B2B pivot, data moat thesis, vertical criteria, and candidate verticals; updated Last updated to v2.2
- `wiki/opportunity-analysis.md` — Added "Leadership Validation (May 2026)" section with data moat filter, pilot access strategy, refined vertical shortlist, and B2C POC pause
- `wiki/spatial-ai-assistant.md` — Added "Strategic Direction Update (May 2026)" subsection to 9D implications section
- `wiki/index.md` — Added monthly-brief-2026-05-05 as first entry in Core Strategic Pages; updated Last updated

**Summary**: Ingested the first leadership alignment document in the wiki. The primary strategic shift is a formal B2C → B2B pivot with a data moat defensibility thesis. Wiki now has **48 pages**.

---

## 2026-05-06 — B2B Use Case Draft (Pass 7.1)

**Operation**: Synthesized web research + wiki into 8 ranked B2B use cases for Moiz review

**Pages created (1)**:
- `wiki/b2b-use-cases-draft-2026-05-06.md` — 8 use cases (construction BIM, field technician, warehouse picking, telecom/utilities, data center, healthcare, pharma lab, aviation MRO), each scored on glasses fit / ROI / data moat / local access; priority recommendation: Construction #1, Industrial Field Service #2, Warehouse #3; CPEC 2.0 identified as Pakistan-specific accelerator across verticals

**Pages modified (1)**:
- `wiki/index.md` — Added use case draft to Core Strategic Pages; updated Last updated

**Key research inputs**: PTC 2025 industrial AR benchmark (32% task time, 40% error reduction), XYZ Reality $135M / 7 data centers (10x ROI), DHL 40% error reduction / <12 month payback, Boeing 25% time reduction (near-zero errors), CPEC 2.0 industrial relocation roadmap (2025–2029)

**Summary**: Created the B2B use case document requested at May 05 debrief. Wiki now has **49 pages**.

---

## 2026-05-13 — May 07 Sync Ingestion (Pass 8)

**Operation**: Ingested "Spatial AI Sync - May 07" meeting notes

**Sources ingested (1 total)**:
- `raw/Spatial AI Synch - May 07.txt`

**Pages created (2)**:
- `wiki/spatial-ai-sync-2026-05-07.md` — Summary of the May 07 sync: pivot to vertical B2B, technical approaches (Tablet First, On-Device Vision), and new vertical leads.
- `wiki/b2b-evaluation-criteria.md` — Detailed breakdown of the LLM-based scoring framework for B2B use cases.

**Pages modified (3)**:
- `wiki/9d-technologies-strategic-brief.md` — Updated with May 07 strategic insights and evaluation framework.
- `wiki/b2b-use-cases-draft-2026-05-06.md` — Added Medical Rehabilitation and Kitchen Operations use cases; updated selection criteria.
- `wiki/index.md` — Added new pages to the Core Strategic Pages section; updated last updated date.

**Summary**: Integrated the May 07 strategic sync. Key additions include the **B2B Evaluation Criteria** (Big Tech avoidance, Industry willingness), the **Tablet First** entry strategy, and two new high-priority verticals: **Medical Rehabilitation** and **Large-Scale Kitchen Operations**. Confirmed the move towards a defensive MOAT via local industry penetration. Total wiki now has **51 pages**.

---

## 2026-05-13 — Pakistani B2B Ideas Generation (Pass 8.1)

**Operation**: Generated and scored 20 localized B2B Spatial AI ideas based on May 07 strategy.

**Pages created (1)**:
- `wiki/pakistan-b2b-ideas-20.md` — 20 vertical B2B use cases designed for the Pakistani industrial constraints. Ideas are grouped by sector (Textile, Medical, Agriculture, Heavy Industry) and scored across Solution Quality, Adoption Criteria, and Moat Confidence. Highlights the "Tablet-First" and "Defensive Data Moat" concepts from the May 07 sync.

**Pages modified (2)**:
- `wiki/index.md` — Added the new ideas list to the Core Strategic Pages.
- `wiki/log.md` — This entry.

**Summary**: Translated the high-level strategic pivot into 40 actionable, local-market-grounded pilot ideas across two phases. Identified critical constraints (Hardware import taxes, low digital literacy, connectivity issues) and ranked Sialkot Surgical QC, Textile QC, Diabetic Ulcer Monitoring, and Medical Rehab as top pilot targets. Wiki now has **72 pages**.

---

## 2026-05-13 — Pakistan Market Constraints & MOAT Analysis (Pass 8.2)

**Operation**: Extracted and expanded market analysis into a dedicated document.

**Pages created (1)**:
- `wiki/pakistan-adoption-and-moat-analysis.md` — Detailed analysis of the 4 primary adoption hurdles (Hardware, Connectivity, Literacy, ROI Culture) and the 3-tier MOAT strategy (Localized Data, Industry Penetration, Regulatory Integration). Includes a scoring matrix for adoption difficulty.

**Pages modified (2)**:
- `wiki/pakistan-b2b-ideas-20.md` — Replaced internal constraints section with a link to the dedicated analysis.
- `wiki/index.md` — Added the new analysis file to the Core Strategic Pages.

**Summary**: Structured the Pakistani market "Headwinds" into a standalone strategic asset. This document provides the "Why" and "How" behind the "Tablet-First" and "On-Device" technical decisions, serving as a foundational reference for all future B2B vertical developments. Wiki now has **73 pages**.

---

## 2026-05-13 — Spatial AI Solution Enrichment (Pass 8.3)

**Operation**: Added "Spatial AI Solution" section to all 40 B2B ideas.

**Pages modified (40)**:
- All files in `wiki/b2b-ideas/`.

**Summary**: Enhanced the 40 B2B ideas by explicitly detailing how **AI Spatial Assistants** (real-time computer vision) and **AR/VR Overlays** (visual guidance) solve the specific business problems. This grounding ensures the technical implementation path for each idea is clearly understood.

---

## 2026-05-13 — B2B Problem Statements Ingestion (Pass 9)

**Operation**: Ingested 35 B2B problem statements from 9D Technologies Research report.

**Sources ingested (1 total)**:
- `raw/B2B Problem Statements (AR_VR_MR).pdf`

**Attachments created**:
- 72 images extracted from the PDF and stored in `attachments/b2b-problem-statements/`.

**Pages created (33)**:
- `wiki/b2b-problem-statements-report.md` — Summary of the 35 problem statements and evaluation framework.
- 32 new idea pages in `wiki/b2b-ideas/` (e.g., `spinal-fusion-xray-vision.md`, `nuclear-decommissioning.md`, etc.).

**Pages modified (4)**:
- `wiki/b2b-ideas/medical-rehabilitation-assistant.md` — Updated with technical depth and images from the report.
- `wiki/b2b-ideas/vocational-ar-training.md` — Updated with images and new content.
- `wiki/b2b-ideas/warehouse-vision-picker.md` — Updated with micro-fulfillment picking depth.
- `wiki/pakistan-b2b-ideas-database.md` — Reconstructed to include 72 unique ideas grouped by sector.

**Summary**: Ingested a high-density research report from 9D Technologies, adding 35 technical use cases with deep "Moat" logic. Extracted and embedded 72 illustrative images. The B2B Ideas Database now contains **72 unique localized opportunities**, categorized across 8 sectors. Total wiki now has **106 pages**.

---

## 2026-05-15 — B2B Technical Evaluation Criteria (Pass 10) — Usama Ashraf

**Operation**: Created engineering perspective scoring framework for the 72 B2B Spatial AI ideas.

**Pages created (1)**:
- `wiki/b2b-evaluation-criteria-technical.md` — Technical/engineering feasibility scoring framework for Idea Quality, Adoption, and Moat, each with 1–10 scales, scoring guides, key engineering questions, and technical constraint checklist.

**Pages modified (2)**:
- `wiki/index.md` — Added [[b2b-evaluation-criteria-technical]] to Core Strategic Pages.
- `wiki/log.md` — This entry.

**Summary**: Created a dedicated engineering evaluation framework for scoring 72 B2B ideas from an Associate AI Engineer's perspective. Reinterprets leadership's three metrics (Quality, Adoption, Moat) through technical feasibility, deployment complexity, and engineering defensibility lenses. Each metric includes a 1–10 scoring guide, key engineering questions, and linkage to the existing [[b2b-ideas-scoring-report]]. A cross-cutting Technical Constraints table covers camera dependency, accuracy thresholds, latency budgets, edge vs cloud trade-offs, offline capability, and training data cost. Designed to produce independent technical scores that may diverge from the existing business-perspective scores.

---

## 2026-05-15 — Technical Scoring of 72 B2B Ideas (Pass 10.1) — Usama Ashraf

**Operation**: Performed a comprehensive technical evaluation of all 72 B2B ideas.

**Pages created (1)**:
- `wiki/b2b-scoring-technical.md` — Full scoring table for all 72 ideas from a technical perspective, a top-10 list of technically-backed picks, category breakdowns, and key engineering insights on feasibility, deployment, and moat.

**Pages modified (2)**:
- `wiki/index.md` — Added [[b2b-scoring-technical]] to Core Strategic Pages.
- `wiki/log.md` — This entry.

**Summary**: Scored all 72 B2B ideas in `wiki/b2b-ideas/` using the [[b2b-evaluation-criteria-technical]] framework. The scoring prioritizes simple CV, mobile/tablet deployment, offline capability, and strong data moats. The final report identifies the top 10 most technically viable projects for MVP consideration, led by [[surgical-instrument-qc]], [[crop-disease-scouting]], and several other manufacturing-focused CV applications. It also provides high-level technical insights and flags high-risk projects to avoid for initial development.

---

## 2026-05-15 — B2B Evaluation Criteria — Salman Khalid (Pass 11)

**Operation**: Created expanded global-market evaluation framework incorporating Spatial_AI_Venture_Evaluation_Framework.docx

**Sources ingested (1 total)**:
- `Spatial_AI_Venture_Evaluation_Framework.docx` — Comprehensive 7-section evaluation framework

**Pages created (1)**:
- `wiki/b2b-eval-criteria-salman.md` — Full expanded framework with 7 sections: Strategic Defensibility, Global Market Potential, Technical Feasibility, Enterprise Commercial Viability, Execution & Go-To-Market, Long-Term Platform Potential, Competitive Timing; plus Simplified Scoring Framework (Quality/Adoption/Moat 1-10) and evaluation workflow

**Pages modified (2)**:
- `wiki/index.md` — Added b2b-eval-criteria-salman to Core Strategic Pages; updated last updated date
- `wiki/b2b-evaluation-criteria.md` — Added cross-reference to SK version in Related pages

**Key modification from original framework**: All-market (global) focus instead of local Pakistani market targeting. Primary considerations now include:
- International scalability as a primary filter
- Solutions that work across multiple countries with minimal localization
- Global labor shortages and operational inefficiencies as target problems
- Enterprises with international presence as target customers

**Summary**: Expanded the B2B Evaluation Criteria with the full Spatial AI Venture Evaluation Framework, reoriented toward global market potential. Wiki now has **107 pages**.

---

## 2026-05-15 — Unified B2B Scoring Matrix (Pass 12) — G. Raza

**Operation**: Created a consolidated scoring dashboard combining local and global critical evaluations.

**Pages created (1)**:
- `wiki/b2b-scoring-raza.md` — Unified table for 71+ ideas with side-by-side local and global scores (Quality, Moat, Adoption) and direct links to original research.

**Pages modified (1)**:
- `wiki/index.md` — Added the unified scoring page to the index.

**Summary**: Finalized the critical evaluation workflow by merging local and global insights into a single strategic dashboard. This provides a high-signal view for cross-market opportunity assessment without modifying the original idea files.

---
## 2026-05-18
- [[b2b-eval-criteria-u-ashraf]] — Technical evaluation by Usama Ashraf
- [[b2b-scoring-u-ashraf]] — Technical scoring of 72 ideas by Usama Ashraf
---

## 2026-05-19 — File Renames (Pass 14)

**Operation**: Renamed 7 wiki files for consistent naming convention; updated all internal wiki-links.

**Files renamed**:
- `b2b-criteria-madratzz-global.md` → `b2b-eval-criteria-G-raza.md`
- `b2b-criteria-madratzz-local.md` → `b2b-eval-criteria-L-raza.md`
- `b2b-evaluation-criteria-sk.md` → `b2b-eval-criteria-salman.md`
- `b2b-evaluation-criteria-Usama_Ashraf.md` → `b2b-eval-criteria-u-ashraf.md`
- `madratzz-b2b-scoring.md` → `b2b-scoring-raza.md`
- `global-b2b-ideas-database.md` → `b2b-scoring-salman.md`
- `b2b-scoring-Usama_Ashraf.md` → `b2b-scoring-u-ashraf.md`

**Files updated** (internal links patched):
- `wiki/b2b-eval-criteria-salman.md`
- `wiki/b2b-scoring-madratzz-global.md`
- `wiki/b2b-scoring-madratzz-local.md`
- `wiki/b2b-scoring-raza.md`
- `wiki/b2b-scoring-salman.md`
- `wiki/index.md`
- `wiki/log.md`

**Summary**: Renamed 7 files and patched all internal wiki-links to match. No content was modified.

---

## 2026-05-19 — New Evaluation Criteria (Pass 15) — U. Athar

**Operation**: Created new B2B evaluation criteria file for scoring the 72 problem statements.

**Pages created (1)**:
- `wiki/b2b-eval-criteria-u-athar.md` — Evaluation framework covering Quality, Adoption, and Moat (1–10 rubrics with scoring guides and key questions per dimension), a four-property filter (Vertical Specificity, Data Moat, Regional/Geo Leverage, Two-Pronged Vector), a technical constraints checklist, a disqualifiers list, and a per-idea scoring worksheet template.

**Pages modified (2)**:
- `wiki/index.md` — Added b2b-eval-criteria-u-athar to Core Strategic Pages.
- `wiki/log.md` — This entry.

**Summary**: Created a comprehensive evaluation framework for scoring all 72 B2B Spatial AI problem statements. The framework introduces a Four-Property Filter as a required pre-scoring pass, and adds explicit disqualifiers to fast-reject ideas that cannot be deployed in the Pakistan market.

---

## 2026-05-19 — B2B Scoring Pass (Pass 16) — U. Athar

**Operation**: Scored all 72 B2B problem statements using the [[b2b-eval-criteria-u-athar]] framework.

**Pages created (1)**:
- `wiki/b2b-scoring-u-athar.md` — Full scoring of all 72 ideas: summary table (Quality/Adoption/Moat/Total), detailed per-idea entries with four-property filter and disqualifier flags, top 15 ranked ideas, and deprioritize list with reasons.

**Pages modified (2)**:
- `wiki/index.md` — Added b2b-scoring-u-athar to Core Strategic Pages.
- `wiki/log.md` — This entry.

**Top findings**:
- Highest scorer (27/30): surgical-instrument-qc
- Top 3 recommended for immediate pilot: surgical-instrument-qc, textile-quality-control, construction-bim-tracker, telecom-tower-maintenance
- 7 ideas flagged for deprioritization: nuclear-decommissioning, defense-maintenance-training, deepwater-bop-diagnostics, semiconductor-euv-maintenance, interior-designer-assistant, brick-kiln-monitoring, remote-surgical-mentorship

**Summary**: Completed the full scoring pass across all 72 B2B Spatial AI problem statements. The manufacturing cluster (surgical-instrument-qc, glove-seam-inspector, sports-goods-stitching, sports-apparel-alignment, surgical-forging-assistant) emerges as the highest-concentration pilot opportunity — five high-scoring ideas in one geography that share a data collection infrastructure.

---

## 2026-05-20 — New B2B Idea Added + Scored (Pass 17) — U. Athar / Claude Code

**Operation**: Created the 73rd B2B problem statement and scored it across all four evaluator frameworks.

**Pages created (1)**:
- `wiki/b2b-ideas/sports-coaching-ar-assistant.md` — Coach wears AR smart glasses to monitor all athletes in real-time with biomechanical overlays (running pace, stride angles, joint mechanics, fatigue markers, tactical spacing). Sector: Sports & Athletics. Moat built on longitudinal player-level biomechanical data and coach workflow lock-in.

**Pages modified (12)**:
- `wiki/index.md` — Updated idea count 72 → 73; added [[sports-coaching-ar-assistant]] entry; updated last-updated date to 2026-05-20.
- `wiki/pakistan-b2b-ideas-database.md` — Updated idea count 72 → 73 in summary; added new "Sports & Athletics" sector section with sports-coaching-ar-assistant row.
- `wiki/b2b-eval-criteria-u-ashraf.md` — Updated idea count 72 → 73 in three places.
- `wiki/b2b-eval-criteria-u-athar.md` — Updated idea count 72 → 73 in three places.
- `wiki/b2b-scoring-raza.md` — Added sports-coaching-ar-assistant at L.Total=26 / G.Total=22 tier (L: Q=9, M=9, A=8; G: Q=9, M=5, A=8).
- `wiki/b2b-scoring-salman.md` — Updated idea count 72 → 73; added new "Sports & Athletics" section with Q=9/A=8/M=9=26; inserted at rank 9 in Top 11 Global Opportunities.
- `wiki/b2b-scoring-u-ashraf.md` — Updated idea count 72 → 73; added Q=8/A=8/M=9=25 row alphabetically between sports-apparel-alignment and sports-goods-stitching.
- `wiki/b2b-scoring-u-athar.md` — Updated idea count 72 → 73; inserted as row #61 (alphabetically between sports-apparel and sports-goods) in summary table and detailed entries; renumbered old rows 61-72 to 62-73. Scores: Q=8/A=8/M=9=25. Four-Property Filter: Vertical=Strong, Data Moat=Strong, Regional=Partial, Two-Pronged=Strong.
- `wiki/b2b-scoring-averaged.md` — Inserted at rank 6 (Avg Q=8.50, Avg A=8.00, Avg M=8.50, Avg Total=25.00); renumbered old ranks 6-72 to 7-73.
- `wiki/log.md` — This entry.

**Final scores**:
| Evaluator | Q | A | M | Total |
|-----------|---|---|---|-------|
| Raza Local | 9 | 8 | 9 | 26 |
| Raza Global | 9 | 8 | 5 | 22 |
| Salman | 9 | 8 | 9 | 26 |
| u-ashraf | 8 | 8 | 9 | 25 |
| u-athar | 8 | 8 | 9 | 25 |
| **Averaged** | **8.50** | **8.00** | **8.50** | **25.00** |

**Summary**: Added the sports coaching AR assistant as idea #73 and scored it across all four evaluation frameworks. Final averaged rank: #6 of 73. The idea targets a coach wearing smart glasses to receive real-time per-athlete biomechanical overlays during live practice — addressing the universal coaching blindspot of monitoring multiple athletes simultaneously. Applicable to cricket, football, hockey, athletics, and combat sports. Moat is longitudinal player-level data plus coach workflow lock-in; entry SKU via fixed-camera tablet mode reduces hardware adoption friction.

