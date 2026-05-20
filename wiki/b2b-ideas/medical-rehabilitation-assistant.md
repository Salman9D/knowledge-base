---
sector: Healthcare & Medical
target_city: National
quality: 9
adoption: 6
moat: 9
status: Shortlisted
---
# Rehabilitation & Motor Assessment Platform for Stroke & Spinal Cord Injury

> This is the highest-moat idea in the entire shortlist. Clinical recovery trajectory data (thousands of patient-hours linked to functional outcomes) is genuinely impossible to replicate without running the same clinical partnerships. The adoption score is lower because of the headset distribution challenge, but the tablet-based entry path (no headset required) removes that blocker for the pilot. AKUH or Shaukat Khanum are the natural first partners.

**Evaluator Consensus**: Q=9 / A=7 / M=9 | Avg Total=24.00/30

---

## 1. The Problem

Rehabilitation after stroke, spinal cord injury, or traumatic brain injury is one of the most under-served areas in global healthcare, and the situation in under developed and developing countries is severe.

**The global deficit**:
- ~15 million new stroke patients per year worldwide (WHO 2024)
- <5% receive adequate, evidence-based rehabilitation (Lancet Neurology 2023)
- Standard care requires 1 physiotherapist : 1 patient, in-person, 3–5 sessions per week for 3–6 months
- The global neurorehabilitation specialist shortage is worsening: there are not enough trained specialists to serve the existing patient population even in high-income countries

**Local-specific severity**:
- ~350,000 new stroke patients per year (estimated from WHO regional data)
- Qualified neurorehabilitation specialists are concentrated almost exclusively in Lahore, Karachi, and Islamabad
- For patients in any tier-2 or rural city, the realistic rehabilitation option is either travelling to a major city multiple times per week (unaffordable for most) or receiving no structured rehabilitation at all
- The consequence is preventable long-term disability. Stroke patients who receive inadequate rehabilitation have significantly higher rates of permanent motor impairment

**The measurement gap** (compounding the access gap):
- Current clinical motor assessment (Barthel Index, Fugl-Meyer scale) is administered by a clinician during a physical session. Subjective, episodic, and resource-intensive
- Between sessions, there is no objective record of how a patient is actually moving, compensating, or regressing
- Compensation patterns (where a patient achieves a movement goal using the wrong muscle group, masking weakness) are routinely missed in standard observation

---

## 2. The Spatial AI Solution

A VR/tablet platform that simultaneously delivers calibrated therapy and objectively measures motor recovery, replacing 1:1 sessions with a system that scales 1:N.

**For patients**:
- Gamified VR exercises simulating daily activities: reach for a cup, press a button, maintain balance while reaching
- Tasks are calibrated to the patient's current motor capacity and advance adaptively
- No expensive motion-capture hardware: body tracking runs entirely from the front-facing camera using AI pose estimation (no wearables on the patient)
- Available in Urdu (or regional language) with familiar visual environments (domestic scenes)
- Accessible via a low-cost headset (Meta Quest 3S, ~$299) or a tablet with no headset at all. The tablet mode enables rural deployment

**For therapists**:
- A web dashboard monitoring all active patients simultaneously
- Per-patient metrics: joint angles at each exercise repetition, movement smoothness score, reaction time, compensation pattern flags, session-over-session trajectory
- Auto-generated progress reports for clinical notes
- Alert system: the AI flags anomalies (regression in shoulder abduction, new compensatory hip lean) that the therapist reviews asynchronously
- One therapist can effectively monitor 15–20 patients remotely, vs. 4–6 in a traditional in-person schedule

**Technology stack**:

| Component | Technology | Deployment |
|-----------|-----------|------------|
| Body + hand pose estimation | MediaPipe Holistic (on-device) | On-device (tablet or headset) |
| Motor metrics computation | Custom biomechanics pipeline on top of pose data | On-device |
| Compensation pattern detection | Trained classifier on labeled recovery trajectories | Cloud (inference) |
| VR exercise environment | Unity (cross-platform: Quest, PC, Android) | On-device |
| Therapist dashboard | React web app with REST API | Cloud |
| Clinical data storage | HIPAA/PDPA-compliant encrypted cloud database | Cloud |
| Platform | Meta Quest 3S (~$299) or tablet (no headset) | Entry: tablet |

---

## 3. Market Size & Opportunity

| Scope | Metric | Source |
|-------|--------|--------|
| Global stroke rehabilitation market | ~$1.5B (2024), 6% CAGR | Grand View Research |
| Broader neurorehabilitation market | ~$3.2B (2024) → $5.8B (2030) | Mordor Intelligence |
| VR in healthcare/rehabilitation | Part of $1.2B (2024) → $9.7B (2030) healthcare XR market | Various analysts |
| Healthcare XR CAGR | 35% | 9D internal research |
| Stroke incidence | ~350,000/year | Estimated from WHO regional |
| Qualified neurorehab specialists | <200 (estimated) | Clinical community estimate |
| US stroke incidence | ~800,000/year | CDC 2024 |
| UK, Germany, Japan | Significant aging populations with documented rehabilitation backlog | NHS, WHO |
| Digital therapeutics (DTx) market (including rehab) | $6.9B (2024) → $18.1B (2030) | MarketsandMarkets |
| VR rehab clinical evidence | 45 RCTs meta-analysis confirms efficacy (Sung et al. 2024) | [[vr-healthcare-evidence]] |

**The clinical evidence base is established**. The question is no longer "does VR rehabilitation work?". The Sung et al. meta-analysis of 45 randomised controlled trials confirms it does. The question is who builds the scalable delivery platform.

**International revenue potential** is disproportionately large: a pilot that generates peer-reviewed clinical data (which AKUH is well-positioned to co-publish) opens doors to the US and EU markets where reimbursable digital therapeutics pathways (FDA 510(k), NICE evaluation in the UK) exist.

---

## 4. Technical Feasibility

**Confidence: High** for the MVP; medium-high for the full clinical AI layer.

| Capability | Readiness | Notes |
|-----------|-----------|-------|
| Markerless body tracking on tablet/headset | Mature (MediaPipe Holistic, proven in production) | 33 body landmarks at 30fps on mid-range Android |
| Joint angle computation from pose data | Mature | Standard biomechanics calculation from landmark positions |
| VR exercise environment (Unity) | Mature | Standard game-development toolchain |
| Compensation pattern detection (ML classifier) | Medium. Requires labelled training data | The pilot generates the data; a baseline model is trainable from published neurorehab research datasets |
| Adaptive exercise difficulty | Medium | Rule-based for Phase 1; ML-adaptive in Phase 2 |
| Therapist dashboard | Mature | Standard web development |
| HIPAA/PDPA compliant data architecture | Mature with proper implementation | Requires legal review; not a technical blocker |

**MVP scope**:
1. 3–5 validated therapy exercises (reaching, grasping, shoulder flexion, balance)
2. Real-time joint angle and smoothness metrics displayed on-screen
3. Session logging with per-exercise performance record
4. Basic therapist dashboard: per-patient timeline, session history, printable report
5. Tablet mode (no headset required) as the primary entry point

**Phase 2 additions** (not in MVP): compensation pattern detection, adaptive difficulty, remote patient video review, multi-language UI, Quest headset integration.

---

## 5. Moat Potential

**Confidence: Very High.** The highest clinical moat of any idea in the shortlist.

**What we accumulate that no one else can replicate without running the same partnerships**:

1. **Longitudinal recovery trajectories**: Patient A on Day 1 vs. Day 14 vs. Day 90. Joint angles, movement smoothness, compensation patterns, all time-stamped and linked to formal clinical outcome scores (Barthel, Fugl-Meyer). This dataset does not exist. It barely exists in structured form globally.

2. **Compensation pattern library**: The precise biomechanical substitutions patients use when a primary motor pathway is blocked are not in any textbook. They are observable only through continuous instrumented tracking. After 1,000 patient-sessions, our classifier will identify compensation patterns that even experienced clinicians miss on observation.

3. **Population-specific models**: Local stroke patients differ from Western cohorts in age of onset (younger), co-morbidity profile (higher hypertension prevalence), and rehabilitation access history. A model trained on our data will outperform any globally-trained model for this population.

4. **Clinical partnership network**: IRB approvals, clinical co-investigation relationships with AKUH/Shaukat Khanum clinicians, and co-authored peer-reviewed papers create institutional barriers to switching that pure data cannot fully capture.

**Why switching is near-impossible**: A rehabilitation centre that has used our platform for 2 years has their patients' longitudinal motor histories on our platform. Switching to a competitor means losing the clinical record which is both a practical and regulatory concern.

---

## 6. Demo-ability

**Rating: Very Good**, and uniquely emotive. The patient impact is visible in the room.

**What a compelling 5-minute demo looks like**:

1. Open the tablet app. A demo participant (anyone in the room) holds the tablet facing them and performs a reaching task.
2. Live on screen: 33 body landmarks tracked in real time, shoulder and elbow angles displayed numerically, a "movement smoothness" gauge updating each repetition.
3. Show a recorded session comparison: "This is the same patient on Day 1 vs. Day 30" Visibly improved joint range and reduced compensation lean.
4. Open the therapist dashboard on a second screen: patient list, session history, auto-generated progress note.
5. Simulate a compensation pattern alert: "This patient is achieving shoulder abduction using trunk lean. We flagged it on session 7, the therapist intervened, and by session 12 the compensation was resolved."

**Hardware needed for demo**: One Android tablet. No headset required. No specialist space. Fully boardroom-demoable.

One physiotherapist in Lahore can now effectively monitor and guide 20 stroke patients simultaneously. 18 of them in cities where no specialist exists.

---

## 7. Path to Revenue

| Phase | Activity | Revenue |
|-------|----------|---------|
| **Phase 0** | No-cost pilot at AKUH or Shaukat Khanum rehab department. 20–30 patients enrolled with IRB approval. Therapist co-investigators validate metrics against standard assessments. | $0 Exclusive clinical data + co-publication rights |
| **Phase 1** | Expand to 100+ patients. Gather trajectory data. Submit first clinical paper. Onboard 2–3 additional rehab centres at pilot terms. | $0 Minimal. Establishing clinical credibility |
| **Phase 2** | Paid licensing to rehab centres. $1,500–3,000/device/year (headset) or $800–1,200/year (tablet-only). Enterprise plan for hospitals: $8,000–20,000/year for unlimited patient seats. | $50K–200K ARR |
| **Phase 3** | International expansion. FDA 510(k) / CE marking process (enabled by clinical data already in hand). US and EU insurance reimbursement pathway for digital therapeutics. | $1M–10M ARR potential |

**Revenue reality check**: The near-term revenue is modest (healthcare IT budgets are small). The real commercial case for this idea is **using local market as a data-generation and clinical-validation engine to unlock the international market**. The cost structure of running the pilot locally is 5–10x lower than in the US or UK, but the clinical data generated is internationally publishable and commercially valuable.

---

## 8. Alignment with Research Pillars

| Pillar (from [[9d-technologies-strategic-brief]] & [[monthly-brief-2026-05-05]]) | Alignment |
|-------|-----------|
| **B2B enterprise, clear ROI** | B2B sale to rehabilitation centres and hospital systems; ROI = therapist capacity multiplied 4–5x |
| **Data moat via exclusive pilot data** | Strongest data moat in the shortlist. IRB-approved longitudinal clinical data |
| **Tablet-first entry** | Yes: tablet-only MVP with no headset required; Quest integration as premium tier |
| **On-device-first architecture** | Yes: pose estimation runs on-device in real time; only summary analytics go to cloud |
| **High-frequency, hands-occupied workflow** | Yes: patient performing exercises; therapist monitoring remotely; continuous data stream |
| **AR-first (not VR/MR)** | Nuance: the patient-facing product is VR (immersive environment); the therapist-facing product is an AR-overlay dashboard. VR in healthcare is explicitly supported (see [[vr-healthcare-evidence]]) |
| **Named candidate vertical from Moiz debrief** | Yes: "Medical Rehabilitation" was explicitly added as a high-potential vertical in the May 07 strategy sync (see [[9d-technologies-strategic-brief]]) |
| **International scaling potential** | Highest of any shortlisted idea (clinical data generated locally is directly transferable to US/EU markets) |

---

## 9. Risks & Mitigations

| Risk | Severity | Mitigation |
|------|----------|------------|
| IRB approval delays (ethics review for clinical data collection) | Medium | Start the IRB process in parallel with system development; AKUH has an efficient IRB process |
| Therapist resistance to AI-assisted assessment | Low–Medium | Position as an aid to their judgment, not a replacement. Co-investigator role makes them advocates, not skeptics. |
| Headset distribution to patients (rural deployment) | Medium | Tablet-only mode removes this blocker entirely. Headsets are Phase 2. |
| Liability if a patient follows incorrect exercise guidance | Medium | Clinical co-investigator reviews and validates all exercise protocols before deployment. Human therapist remains responsible for clinical decisions. |
| Healthcare IT budget constraints | High | Revenue model is modest; international market is the commercial thesis. Pilot is primarily a data-generation and credibility-building exercise. |
| Competitive entry from PwC/Accenture health digital | Low | Large consultancies will not build this vertically locally. The clinical partner relationships we build are not replicable. |

---

## 10. Recommendation

Proceed with a 6–12 month timeline to the first publishable clinical results. This idea has the longest path to revenue but the largest international upside. The key strategic value is: using lower clinical trial costs and higher unmet need to generate world-class clinical evidence, then commercialise internationally.

**Suggested first call**: Dr. Saad Shafqat (Neurology, AKUH) or the head of physiotherapy at Shaukat Khanum Memorial. Alternatively, Umang Rehabilitation Centre (Karachi) or Hameed Latif Hospital physiotherapy department.

**Success metric for the pilot**: Achieve statistically significant improvement in Fugl-Meyer scores (or Barthel Index) in the VR-assisted group vs. standard care, publishable in a peer-reviewed journal within 12 months.

---

## Related Pages

- [[pakistan-b2b-ideas-database]]
- [[b2b-problem-statements-report]]
- [[vr-healthcare-evidence]]
- [[healthcare-xr]]
- [[spatial-ai-assistant]]
- [[9d-technologies-strategic-brief]]
- [[monthly-brief-2026-05-05]]
- [[b2b-scoring-averaged]]
