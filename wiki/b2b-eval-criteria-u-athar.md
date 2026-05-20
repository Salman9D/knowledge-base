# B2B Evaluation Criteria — Synthesized Framework (U. Athar)

**Summary**: A synthesized, best-of evaluation framework for scoring the 72 B2B AR/VR/MR/Spatial AI problem statements. Combines technical feasibility (u-ashraf), local deployment realism (L-raza), global scaling constraints (G-raza), and commercial strategy (salman), with new criteria for vertical specificity, data moat, regional leverage, and the two-pronged research-plus-commercial vector.

**Sources**: [[b2b-eval-criteria-u-ashraf]], [[b2b-eval-criteria-G-raza]], [[b2b-eval-criteria-L-raza]], [[b2b-eval-criteria-salman]], [[pakistan-adoption-and-moat-analysis]], [[spatial-ai-sync-2026-05-07]]

**Last updated**: 2026-05-19

---

## Guiding Philosophy

Every idea must be evaluated against four core properties. These are not scoring dimensions on their own — they are the lens through which Quality, Adoption, and Moat scores must be justified.

| Property | Definition |
|----------|------------|
| **Vertical Specificity** | The problem is narrow and domain-specific. No horizontal solution covers 80%+ of the need. Big Tech will not build this because the addressable market is too small or too specialized for them to care. |
| **Data Moat** | Every time the system is used, it generates proprietary data — defect images, spatial maps, workflow patterns — that compounds into a durable advantage. The more it is used, the harder it is for a competitor to replicate. |
| **Regional / Geo Leverage** | The idea exploits something unique to the Pakistan / South Asia context: access to specific industrial clusters (Sialkot, Faisalabad, CPEC corridors), cheap high-quality annotation labor, leapfrog adoption (no legacy IT systems to fight), or informal trust networks that turn one pilot into twenty. |
| **Two-Pronged Vector** | The idea works simultaneously as a **research showcase / capability platform** (novel dataset, publishable methodology, conference-demonstrable) and as a **commercially viable product** (clear ROI, real pilot customer, replicable sales motion). Neither prong alone is sufficient. |

An idea that is strong on all four properties is a top-priority candidate. An idea that is strong on fewer than two should be deprioritized unless a specific strategic reason overrides.

---

## Scoring Framework

All 72 ideas are scored on exactly three dimensions: **Quality**, **Adoption**, and **Moat**. Each is scored **1–10**. A balanced score above 7 across all three dimensions indicates a strong candidate. A single very high score does not compensate for a very low score elsewhere.

---

### 1. Quality — Score 1–10

**What this measures**: How strong, valuable, and technically sound the Spatial AI solution is. Does it solve a real, painful, measurable problem in a way that AR/VR/MR uniquely enables — and could it not be solved more simply?

| Score | Definition |
|-------|------------|
| 9–10 | Solves a critical, high-stakes problem where spatial AI is the only viable approach — not replaceable by a simple camera feed or a regular app. Pre-trained CV models (YOLO, SAM, GroundingDINO) handle the core task largely out-of-box. MVP achievable in 4–8 weeks. Strong research novelty angle (novel dataset or novel application domain). |
| 7–8 | Clear problem with strong ROI narrative. Spatial AI has a meaningful advantage over non-spatial alternatives. Needs moderate fine-tuning or a small custom dataset. MVP in 8–16 weeks. Publishable research contribution likely. |
| 4–6 | Moderately useful. Spatial AI is an improvement but simpler solutions partially exist. Significant technical complexity — custom model training, specialized sensors, or multi-month R&D. Research contribution unclear or incremental. |
| 2–3 | Weak problem-solution fit. Spatial AI is a nice-to-have rather than a necessity. Technically risky or requires hardware not yet reliable. Unlikely to produce publishable research. |
| 1 | Not a real problem, spatial AI adds no discernible value, or technically infeasible today. |

**Questions to answer when scoring Quality:**
- Is the problem narrow enough that no Big Tech platform will absorb it as a generic feature?
- Does AR/VR/MR unlock a fundamentally new capability, or could a regular mobile app do 80% of the job?
- What is the minimum acceptable accuracy? (QC tasks: >95% precision; guidance tasks: ~80%; safety-critical: >99%)
- What latency is acceptable? Real-time (<100ms), near-real-time (<500ms), or batch (minutes)?
- Can existing foundation models (YOLO, SAM, DINOv2, Depth Anything V2, GroundingDINO) handle the core task?
- Is there a research publication angle — novel dataset, novel application, novel architecture?
- Is the outcome measurable? (error rate reduction %, time saved, cost per unit reduced)
- Does the solution address a problem driven by a structural trend — aging expert workforce, labor shortages, safety mandates — rather than a passing preference?

---

### 2. Adoption — Score 1–10

**What this measures**: How likely is this solution to actually get deployed, used, and paid for in the target environment. This combines enterprise willingness, technical deployment ease, and local Pakistan-specific deployment realism.

| Score | Definition |
|-------|------------|
| 9–10 | Plug-and-play. Works fully offline. Runs on existing Android phones or consumer-grade tablets. No infrastructure changes needed. ROI is immediate and measurable within weeks. The decision-maker is a single owner — one meeting to a pilot. UI is visual-first and works without English literacy. |
| 7–8 | Straightforward deployment with brief setup time. Occasional connectivity required. May need a basic peripheral (clip-on thermal camera, fixed mount). ROI demonstrable within 30–90 days. Willing pilot partner accessible within Pakistan's industrial clusters. |
| 4–6 | Moderate friction. Needs a dedicated hardware unit, ERP integration, or IT department cooperation. ROI narrative requires stakeholder education. Multiple approvals needed. May require regulatory sign-off before deployment. |
| 2–3 | High deployment friction. Requires infrastructure overhaul, unavailable hardware, or a 6–18 month enterprise sales cycle. Privacy or regulatory blockers (patient data, defense contracts) are hard to resolve quickly. |
| 1 | Cannot be deployed in the target market given current hardware availability, connectivity, regulatory environment, or digital literacy. |

**Questions to answer when scoring Adoption:**
- Who is the buyer and who is the daily user — are they the same person? (Owner-operator = fast; procurement committee = slow)
- Can the model run fully on-device on a Snapdragon 8 Gen 2 or equivalent — no cloud required?
- Does it require continuous internet? (Many Sialkot / Faisalabad factory floors have poor or no WiFi)
- Is the UI workable for a semi-literate factory worker — visual overlays, Urdu voice output, no mandatory English reading?
- Can it be deployed as a web app (avoids app store friction) or must it be a native install?
- Does the ROI story hold within Pakistan's cost structure — not just Western wage assumptions?
- Is there an industry cluster multiplier? (One successful pilot in Sialkot spreads by word-of-mouth to 20 nearby workshops)
- Are there safety certifications, import duties, or government approvals that add months of delay?
- Is the device hardware locally available and affordable? (Android tablet: yes; Apple Vision Pro: no; HoloLens 2: no)
- Does the solution tolerate load-shedding? (Offline-first is mandatory in most industrial SITE areas)

---

### 3. Moat — Score 1–10

**What this measures**: How hard would it be for a well-resourced competitor to replicate this system after 12–24 months of live deployment. The score should reflect the compounding advantage from proprietary data, regional entrenchment, deep workflow integration, and switching costs.

| Score | Definition |
|-------|------------|
| 9–10 | Strong proprietary data flywheel — every session generates labeled training data that compounds. Models fine-tuned on local industrial patterns (Sialkot surgical defects, Faisalabad textile weaves) that a global competitor cannot replicate without years of local physical access. Deep workflow integration creates high switching costs. Regional trust network amplifies distribution defensibility. |
| 7–8 | Meaningful data accumulation per deployment. Per-client fine-tuning adds compounding value over time. Moderate integration depth. A competitor would need 6–12 months of local data collection to match performance. |
| 4–6 | Mostly generic pre-trained models. Small amount of custom fine-tuning. A competitor using the same open-source stack could replicate in weeks to a few months. Some integration but low switching cost. |
| 2–3 | Commodity implementation. Any team with access to the same APIs can replicate. No proprietary data. No integration hooks. Zero switching cost. |
| 1 | Entirely built on publicly callable APIs. No differentiation whatsoever. A weekend hackathon team could replicate it. |

**Questions to answer when scoring Moat:**
- Does the system improve with each use session through active learning or HITL feedback? What is the flywheel mechanism?
- Does the deployed system collect failure / anomaly data from real production environments that feeds back into retraining?
- Is the labeling pipeline automatable (weak supervision, pseudo-labeling, active learning) or permanently manual?
- Does the spatial / visual dataset require physical presence in a specific facility, region, or industry to collect — making it non-copyable remotely?
- How tightly coupled is the system to client-specific data: BIM models, custom SKU catalogs, proprietary ERP schemas?
- Can Pakistan-local annotation labor build a dataset at 5–10× lower cost than a global competitor could match?
- Does deployment create a "facility fingerprint" — a calibrated spatial map, camera angle model, or lighting profile — that is non-trivially reproducible by a new entrant?
- Is there a regulatory moat? (First-mover certified by a hospital, safety body, or government agency in the vertical)
- Does the informal trust network in the target industry cluster create a distribution moat — where our reference customer actively vouches to peers?

---

## Four-Property Filter

After assigning the three scores, rate each of the four guiding properties: **Strong / Partial / Weak / None**.

| Property | Strong | Partial | Weak | None |
|----------|--------|---------|------|------|
| **Vertical Specificity** | Hyper-specific domain, Big Tech cannot absorb it | Specific but adjacent to a Big Tech product area | Could be a feature of a platform product | Entirely horizontal — any platform could do this |
| **Data Moat** | Strong flywheel, locally irreplaceable dataset | Moderate flywheel, some local data advantage | Minimal flywheel, data is widely available | Zero flywheel, fully replicable from public data |
| **Regional / Geo Leverage** | Exploits Pakistan-specific cluster, labor, or leapfrog in a way that is central to the business model | Pakistan is a good early market but the model does not depend on it | Pakistan is one of many equally viable markets | No regional advantage whatsoever |
| **Two-Pronged Vector** | Clear research publication angle AND clear commercial pilot pathway, both strong | One prong is strong, the other is plausible | One prong is strong, the other is speculative | Pure research with no commercial path, or pure commercial with no research angle |

**Priority guidance:**
- Strong on all four → Top-priority candidate
- Strong on 3, Partial on 1 → High-priority; address the weak dimension in MVP design
- Strong on 2, Partial on 2 → Conditional; only proceed if the two partial dimensions can be engineered into the product
- Weak on 3 or more → Deprioritize unless a compelling strategic reason overrides

---

## Technical Constraints Checklist

Apply this to every idea regardless of sector. Flag any item that is a hard blocker.

| Constraint | What to Assess |
|------------|---------------|
| **Camera dependency** | Brightness, angle, stability, mounting requirements. Outdoor vs. indoor. Fixed vs. handheld. |
| **Accuracy threshold** | QC: >95% precision. Guidance: ~80%. Safety-critical: >99%. Set the bar before scoring. |
| **Latency budget** | Real-time (33ms for 30fps), guidance (<500ms), or batch (minutes). Determines on-device vs. cloud split. |
| **On-device vs. cloud** | On-device models currently cap at ~7B parameters. Cloud adds latency, cost, and connectivity dependency. |
| **Offline capability** | Factories, mines, fields often have no reliable WiFi. Models must cache and run fully locally. |
| **Privacy / regulatory** | Medical data, defense contracts, financial records. On-device processing is the safest default. |
| **Hardware availability in Pakistan** | Apple Vision Pro / HoloLens 2 → not viable (import duty, cost). Android tablet / phone → viable. Clip-on thermal camera → sometimes locally available. |
| **Training data cost** | Labeled industrial defect data is expensive globally. Pakistan-local annotation is 5–10× cheaper. Assess whether synthetic data can bridge the sim-to-real gap. |
| **Model maintenance & drift** | How often must models retrain? New product SKUs, seasonal lighting changes, production line changes can degrade accuracy rapidly. |
| **ERP / legacy integration** | Global firms: locked into SAP, Oracle, Salesforce. Pakistani SMEs: often paper-based, enabling direct leapfrog to Spatial AI. |
| **Language / literacy** | UI must be visual-first. Urdu voice feedback. No mandatory English reading or typing. |
| **Power / infrastructure** | Load shedding is routine in industrial areas. Offline-first, battery-tolerant, low-power design is mandatory. |

---

## Disqualifiers

An idea with any of the following should be automatically deprioritized unless the blocker can be specifically designed around:

- Requires Apple Vision Pro, HoloLens 2, or other hardware with near-zero local penetration in Pakistan
- Requires persistent cloud connectivity in a deployment environment with unreliable or absent WiFi
- The core IP depends on Big Tech infrastructure (e.g., Apple RoomPlan, Google Maps API) as the primary defensibility
- Regulatory approval timeline exceeds 12 months before the first paying customer can be onboarded
- The problem is so broad or horizontal that Meta / Google / Microsoft will build it as a platform feature within 24 months
- Usage generates zero proprietary data — no flywheel, no compounding advantage
- Requires immediate full ERP integration before delivering any tangible value to the user

---

## Scoring Worksheet

Use this template for each of the 72 ideas during a scoring pass:

```
**Idea**: [Name]
**Sector**: [Textile / Medical / Agriculture / Manufacturing / Logistics / etc.]
**Source file**: [wiki/b2b-ideas/filename.md]

**Quality**: X/10
- Rationale: [1–2 sentences citing specific technical and problem-severity reasons]
- Flags: [Any technical blockers or accuracy/latency concerns]

**Adoption**: X/10
- Rationale: [1–2 sentences citing deployment environment, buyer type, and ROI timeline]
- Flags: [Any hardware, connectivity, literacy, or regulatory blockers]

**Moat**: X/10
- Rationale: [1–2 sentences citing data flywheel mechanism and switching cost sources]
- Flags: [Any defensibility concerns — e.g., easily replicated with public models]

**Four-Property Filter**:
- Vertical Specificity:  Strong / Partial / Weak / None
- Data Moat:             Strong / Partial / Weak / None
- Regional Leverage:     Strong / Partial / Weak / None
- Two-Pronged Vector:    Strong / Partial / Weak / None

**Disqualifiers triggered**: [List any, or "None"]

**Overall Recommendation**: Prioritize / Conditional / Deprioritize
**Key Risk**: [Single biggest risk to success]
**Suggested first step if prioritized**: [One concrete next action]
```

---

## Related Pages

- [[b2b-eval-criteria-u-ashraf]]
- [[b2b-eval-criteria-salman]]
- [[b2b-eval-criteria-G-raza]]
- [[b2b-eval-criteria-L-raza]]
- [[b2b-evaluation-criteria]]
- [[pakistan-adoption-and-moat-analysis]]
- [[b2b-problem-statements-report]]
- [[b2b-use-cases-draft-2026-05-06]]
- [[spatial-ai-sync-2026-05-07]]
- [[pakistan-b2b-ideas-database]]
