# B2B Evaluation Criteria — Technical/Engineering Perspective

**Summary**: Engineering feasibility scoring framework for evaluating 73 B2B Spatial AI ideas from the perspective of an Associate AI Engineer. Reinterprets leadership's three required metrics (Idea Quality, Adoption, Moat) through a technical implementation lens — focusing on what can be built, deployed, and defended from an engineering standpoint.

**Sources**: [[b2b-evaluation-criteria]], [[b2b-ideas-scoring-report]], problem statements from wiki/b2b-ideas/

**Last updated**: 2026-05-15

---

## Scoring Framework

### 1. Idea Quality (Technical Lens) — Score 1–10

**What this measures**: Technical feasibility and buildability of the Spatial AI solution.

| Score | Definition |
|-------|------------|
| 9–10 | Straightforward to implement. Pre-trained CV models (YOLO, SAM, GroundingDINO) work out-of-box. Runs on consumer tablet or phone. No custom hardware needed. MVP in 4–6 weeks. |
| 6–8 | Moderate complexity. Needs custom fine-tuning or synthetic data generation. May require thermal/depth cameras or basic ARKit/ARCore integration. MVP in 6–12 weeks. |
| 3–5 | Significant R&D required. Custom model training from scratch. Requires specialized sensors (e.g., thermal, LiDAR, multispectral). Real-time performance is uncertain. MVP 3–6 months. |
| 1–2 | Not technically feasible with current models or hardware. Requires breakthroughs in SLAM, scene understanding, or edge compute. |

**Key Engineering Questions**:
- Can we use an existing foundation model (YOLO, SAM, DINOv2) or must we train from scratch?
- What is the minimum accuracy bar? (e.g., QC tasks typically need >95% precision)
- What latency is acceptable? Real-time (<100ms) or batch/offline (>1s)?
- On-device inference possible, or cloud dependency required?
- Are public/paid datasets available, or do we need to collect and label our own?

---

### 2. Adoption (Implementation Lens) — Score 1–10

**What this measures**: How easily the solution can be deployed in a real-world B2B environment from a technical standpoint.

| Score | Definition |
|-------|------------|
| 9–10 | Plug-and-play. Works fully offline. Runs on existing mobile hardware (phone/tablet). No infrastructure changes needed. Zero onboarding friction. |
| 6–8 | Needs basic setup: install app, brief user training, occasional connectivity. May need simple peripheral (thermal cam attachment). |
| 3–5 | Complex deployment. Requires dedicated on-prem server or cloud backend. Needs stable high-bandwidth internet. Integration with legacy ERP/MES systems. Extensive training program. |
| 1–2 | Requires complete IT infrastructure overhaul. Needs specialized hardware (e.g., HoloLens, LiDAR scanner) not available in target market. Expert-only operation. |

**Key Engineering Questions**:
- Can the model run on-device (Snapdragon 8 Gen 2 / A16 equivalent or weaker)?
- What is the app size? (Bangladesh/Pakistan common phones have 32–64 GB storage)
- Does it need continuous internet? (Many factories have poor WiFi)
- Is the UI usable by a semi-literate worker? (Visual-only, no text, local language)
- Can we deploy as a web app (avoid app store friction) or must it be native?
- What camera quality is the minimum bar? (1080p? 4K? RGB-only? Stereo?)

---

### 3. Moat (Technical Defensibility Lens) — Score 1–10

**What this measures**: How hard it would be for a competitor to replicate the technical system.

| Score | Definition |
|-------|------------|
| 9–10 | Strong proprietary data flywheel. System improves with every use (active learning, human-in-the-loop). Deep integration with client workflows creates switching costs. Custom models on unique local datasets that global models cannot match. |
| 6–8 | Moderate data advantage. Per-client fine-tuning adds value. Model improves slowly over time. Some integration hooks that take effort to replace. |
| 3–5 | Relies on generic pre-trained models. Data is public or easily collected. Competitor can replicate with same open-source models in weeks. |
| 1–2 | Commodity. Any team can build the same using available APIs/models. No technical advantage. Zero switching costs. |

**Key Engineering Questions**:
- Does the model architecture support incremental learning (LoRA, adapters) so each deployment improves?
- Can we collect edge-case data (failures, anomalies) from live deployments for retraining?
- Is the labeling pipeline automated (active learning, weak supervision) or manual?
- How tightly coupled is the system to the client's existing toolchain (e.g., BIM models, ERP APIs)?
- Can we build a custom on-device model that outperforms generic cloud APIs on this specific task?
- Does the hardware setup (camera angles, lighting, fixtures) become standardized around our solution?

---

## Technical Constraints Across All Scores

These constraints should be evaluated for every idea regardless of category:

| Constraint | Notes |
|------------|-------|
| **Camera dependency** | Brightness, angle, stability requirements. Outdoor vs indoor lighting. |
| **Accuracy threshold** | QC tasks need 95%+ precision. Guidance tasks can tolerate ~80%. Safety tasks need 99.9%+. |
| **Latency budget** | Real-time (30fps = 33ms), near-real-time (<500ms for guidance), batch (minutes). |
| **Edge vs Cloud** | On-device models limited to ~7B parameters currently. Cloud adds latency + cost. |
| **Offline capability** | Critical for factories, mines, fields. Must cache models and run inference locally. |
| **Privacy/Regulatory** | Medical data (HIPAA), defense data, customer IP. On-device only. No cloud. |
| **Hardware availability** | If idea needs specific device (e.g., Apple Vision Pro), adoption ceiling is capped by install base. |
| **Training data cost** | Labeled industrial defect data is expensive. Synthetic data generation is cheaper but may have sim-to-real gap. |
| **Maintenance burden** | How often do models need retraining? (Seasonal changes, new product SKUs, lighting shifts) |
| **Drift monitoring** | Do we need a system to detect when model accuracy degrades in production? |

---

## How to Use This Framework

1. For each of the 73 ideas in `wiki/b2b-ideas/`, read the problem statement
2. Score each of the three metrics 1–10 using the guides above
3. Use the **Key Engineering Questions** in each section as a checklist
4. Flag any **Technical Constraints** that would block or severely limit the idea
5. Record scores alongside a brief engineering rationale referencing specific technical factors

### Reference Existing Scores

The existing [[b2b-ideas-scoring-report]] scores all 73 ideas on the same three metrics from a general business perspective. This technical framework is designed to produce an independent set of scores from the engineering viewpoint — the two may differ significantly. For example, an idea that scores high on business "Adoption" may score low on technical "Adoption" if it requires hardware not available in-market.

## Related Pages

- [[b2b-evaluation-criteria]]
- [[b2b-ideas-scoring-report]]
- [[b2b-ideas]]
- [[pakistan-adoption-and-moat-analysis]]
- [[spatial-ai-sync-2026-05-07]]
