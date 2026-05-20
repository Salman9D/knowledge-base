# B2B Idea Scoring - Technical Engineering Perspective

## Summary
Technical evaluation of 73 B2B Spatial AI ideas focusing on implementation feasibility, deployment complexity, and technical defensibility.

Scoring by: Usama Ashraf
Framework: [[b2b-evaluation-criteria-technical]]
Sources: Problem statements from wiki/b2b-ideas/ directory
Last updated: 2026-05-15

## Scoring Methodology
- **Quality (1-10)**: Technical feasibility, MVP timeline, tech stack maturity
- **Adoption (1-10)**: Deployment ease, infrastructure needs, user training
- **Moat (1-10)**: Proprietary data, technical lock-in, model uniqueness

## Full Scoring Table

| Idea | Quality | Adoption | Moat | Total | Technical Notes |
|------|---------|----------|------|-------|-----------------|
| [[aircraft-engine-inspection]] | 7 | 6 | 9 | 22 | High-end CV needed for crack detection; 3D mapping adds complexity. High regulatory barriers but strong data moat. |
| [[auto-parts-verification]] | 9 | 8 | 8 | 25 | Straightforward CV task (object detection/classification). Tablet-first, easy MVP. Moat from local part defect data. |
| [[avionics-wiring-assembly]] | 6 | 7 | 8 | 21 | Holographic trails require advanced AR. Pin verification is CV. High-value but needs specialized hardware. |
| [[brick-kiln-monitoring]] | 8 | 5 | 7 | 20 | Simple CV for counting. Smoke density is harder. Low-tech environment makes adoption difficult. |
| [[brownfield-digital-twins]] | 5 | 6 | 8 | 19 | LiDAR/photogrammetry is data-heavy. Feature recognition is complex ML. High R&D, not a quick MVP. |
| [[cell-tower-alignment-diagnostics]] | 6 | 7 | 8 | 21 | Visualizing RF signals requires complex data fusion and 3D rendering. Needs ruggedized hardware. |
| [[cement-kiln-inspection]] | 7 | 6 | 8 | 21 | Thermal imaging analysis is feasible. High-temp environment is a hardware challenge. Niche data moat. |
| [[classroom-tutor-spatial]] | 7 | 6 | 7 | 20 | Requires significant 3D content creation. Hardware cost is a major adoption barrier for schools. |
| [[cold-chain-warehouse-slotting]] | 7 | 7 | 8 | 22 | Thermal modeling adds complexity to a standard warehouse problem. Hardware needs to be cold-rated. |
| [[construction-bim-tracker]] | 7 | 6 | 8 | 21 | Comparing reality to BIM is complex 3D analysis. Requires depth sensors/LiDAR. High integration burden. |
| [[construction-cost-intelligence]] | 8 | 7 | 8 | 23 | CV to quantify materials is feasible. Integration with financial systems is the main challenge. |
| [[construction-progress-monitoring]] | 8 | 7 | 8 | 23 | 3D scanning and comparison to BIM is feasible but requires expertise. 4D timeline is a feature extension. |
| [[container-damage-logger]] | 9 | 9 | 7 | 25 | Simple CV task on a mobile device. High-value, easy MVP. Moat is moderate, based on damage patterns. |
| [[cookware-casting-scanner]] | 9 | 8 | 9 | 26 | Excellent use case for CV (anomaly detection). Tablet-first, clear ROI. Strong, niche data moat. |
| [[crime-scene-reconstruction]] | 6 | 6 | 8 | 20 | LiDAR scanning and simulation require specialized tools and skills. Courtroom adoption is slow. |
| [[crop-disease-scouting]] | 9 | 9 | 8 | 26 | Proven CV application (classification). Mobile-first, works offline. Strong local dataset moat. |
| [[cutlery-finishing-guide]] | 8 | 7 | 9 | 24 | Simple AR overlay for angle guidance. Tablet-based. Moat from artisanal workflow data is very strong. |
| [[data-center-rack-guidance]] | 9 | 8 | 8 | 25 | CV for port/cable recognition is very feasible. Mobile-first. High value in preventing outages. |
| [[deepwater-bop-diagnostics]] | 5 | 4 | 9 | 18 | Extreme environment, highly complex machinery. Requires bespoke hardware and deep integration. Very high-risk project. |
| [[defense-maintenance-training]] | 6 | 5 | 10 | 21 | VR training is feasible but content-heavy. AR guidance is complex. Extreme security/procurement barriers. |
| [[denim-wash-consistency]] | 8 | 8 | 8 | 24 | CV for texture/color analysis is a good fit. Controlled factory environment simplifies deployment. |
| [[diabetic-ulcer-monitor]] | 9 | 7 | 9 | 25 | CV for area/color analysis is feasible. Depth sensors on phones help. Strong medical data moat. |
| [[facility-management-optimization]] | 7 | 6 | 8 | 21 | Ingesting diverse data sources is an integration challenge. VR planning is secondary to the data fusion problem. |
| [[fan-motor-winding-qc]] | 9 | 8 | 9 | 26 | Simple CV for counting and checking insulation. Tablet-based, clear ROI. Strong niche data moat. |
| [[fiber-splice-vision]] | 9 | 8 | 8 | 25 | Microscopic CV on a mobile device. High value, prevents re-work. Moat from local fiber brand data. |
| [[fruit-ripeness-grading]] | 9 | 8 | 8 | 25 | CV for color/texture classification. Fixed camera setup is easy to deploy. Moat from local cultivar data. |
| [[glove-seam-inspector]] | 9 | 8 | 9 | 26 | CV for stitch counting is a perfect application. Tablet-based, high ROI for compliance. |
| [[grain-export-grading]] | 9 | 8 | 7 | 24 | CV for impurity/defect detection. Fixed camera setup. Moderate moat, could be replicated. |
| [[hazardous-goods-segregation]] | 8 | 7 | 7 | 22 | CV for label recognition (OCR/classification). AR overlay for warnings is straightforward. Rule engine is key. |
| [[hazmat-spill-simulation]] | 6 | 7 | 8 | 21 | Physics-based simulation is computationally expensive. High-value training but not a simple product. |
| [[hvac-maintenance-copilot]] | 9 | 8 | 8 | 25 | CV for component ID. AR overlay for instructions on tablet is very feasible. High value. |
| [[industrial-digital-twin]] | 5 | 5 | 9 | 19 | Very complex. Requires 3D modeling, IoT integration, predictive AI. High R&D, not an MVP candidate. |
| [[interior-designer-assistant]] | 7 | 8 | 6 | 21 | Room scanning is mature (ARKit/ARCore). Furniture visualization is competitive. Low moat. |
| [[jet-landing-gear-training]] | 6 | 6 | 9 | 21 | High-fidelity 1:1 holographic projection is technically demanding. Requires high-end headsets. |
| [[kiryana-shelf-monitor]] | 9 | 8 | 7 | 24 | Simple CV (object detection) on mobile. High adoption potential via FMCG partners. Moat from local SKU data. |
| [[kitchen-operations-assistant]] | 8 | 7 | 7 | 22 | CV for tracking tasks and hygiene. Tablet-based. Workflow data provides a moderate moat. |
| [[last-mile-condition-log]] | 9 | 9 | 7 | 25 | Simple CV for damage detection on a smartphone. Very easy deployment. High value for logistics. |
| [[leather-sorting-optimizer]] | 8 | 7 | 8 | 23 | CV for defect detection. AR for pattern overlay. Tablet-based. Strong moat from local leather data. |
| [[livestock-health-monitoring]] | 8 | 8 | 8 | 24 | CV for lameness detection (gait analysis) and skin disease. Fixed camera setup. |
| [[loss-control-hazard-scoring]] | 8 | 7 | 9 | 24 | CV for compliance checks (e.g., blocked egress). AR for measurements. Strong moat linking spatial data to claims. |
| [[maintenance-technician-assistant]] | 8 | 7 | 9 | 24 | CV for machine ID. AR overlays on tablet. Knowledge graph is the core challenge, but data provides strong moat. |
| [[medical-rehabilitation-assistant]] | 7 | 6 | 9 | 22 | Pose estimation is mature. VR content needed. Headset distribution is a hurdle. Strong clinical data moat. |
| [[mep-routing-clash-resolution]] | 7 | 7 | 7 | 21 | Requires real-time comparison to BIM. Needs AR headsets for effective use. High-value but complex. |
| [[navigation-assistant-blind]] | 6 | 7 | 8 | 21 | Requires robust real-time SLAM and object recognition on wearable hardware. Technically challenging. |
| [[nuclear-decommissioning]] | 4 | 3 | 10 | 17 | Extreme R&D. Custom hardware, radiation hardening, complex simulations. Not a startup project. |
| [[oncology-surgical-planning]] | 6 | 5 | 9 | 20 | Auto-segmentation of DICOM is a hard ML problem. VR rehearsal is feasible, but AR navigation is high-risk. |
| [[pediatric-cardio-navigation]] | 5 | 5 | 9 | 19 | Beating heart models and real-time scalpel tracking are at the edge of research. Very high risk. |
| [[pharma-gmp-compliance]] | 8 | 6 | 9 | 23 | CV for PPE/label checks is feasible. Integration with lab systems is the main adoption hurdle. Strong compliance moat. |
| [[port-tally-assistant]] | 9 | 8 | 7 | 24 | CV for counting and OCR for license plates. Tablet-based. Very high value and easy to deploy. |
| [[power-grid-repair]] | 8 | 6 | 9 | 23 | CV for component ID is feasible. High-voltage environment makes hardware deployment a challenge. |
| [[real-estate-visualization]] | 8 | 9 | 6 | 23 | Mature tech (Unity/Unreal). High adoption, but competitive space with low technical moat. |
| [[remote-expert-utilities]] | 8 | 7 | 8 | 23 | Standard AR remote assistance. Works on mobile. Connectivity in remote areas is the main challenge. |
| [[remote-surgical-mentorship]] | 7 | 5 | 8 | 20 | High-quality, low-latency video streaming is critical. Regulatory hurdles are high. |
| [[retail-display-compliance]] | 9 | 9 | 6 | 24 | Simple CV on a smartphone. Very easy to deploy. Moat is moderate, based on local store data. |
| [[scrap-metal-sorting]] | 8 | 7 | 9 | 24 | CV for texture/color classification. Can be deployed on a fixed rig. Strong niche data moat. |
| [[seed-purity-vision]] | 9 | 7 | 9 | 25 | Microscopic CV on a tablet. High value for agriculture. Very strong local data moat. |
| [[semiconductor-euv-maintenance]] | 4 | 4 | 9 | 17 | Requires extreme precision and integration with proprietary machine data. Not feasible for a startup. |
| [[solar-health-monitor]] | 8 | 8 | 9 | 25 | CV + thermal imaging on a tablet/drone. High-growth market. Strong moat from local dust/pollution data. |
| [[spinal-fusion-xray-vision]] | 5 | 5 | 9 | 19 | Requires real-time instrument tracking and registration with pre-op scans. Medically high-risk. |
| [[sports-apparel-alignment]] | 9 | 8 | 9 | 26 | Simple CV with AR overlay on a fixed tablet rig. High value, clear ROI. Strong niche data moat. |
| [[sports-coaching-ar-assistant]] | 8 | 8 | 9 | 25 | Markerless multi-person pose estimation (MMPose/MediaPipe) is mature; fixed-camera tablet MVP achievable in 6–8 weeks. Per-athlete longitudinal biomechanics baselines and sport-specific injury models create a compounding technical moat. |
| [[sports-goods-stitching]] | 8 | 8 | 8 | 24 | AR overlay for stitch guidance on a tablet. Good application for artisanal-scale manufacturing. |
| [[subsurface-utility-mapping]] | 6 | 6 | 8 | 20 | Fusing GPR and GIS data is a complex data science problem. Requires specialized hardware. |
| [[surgical-forging-assistant]] | 8 | 8 | 9 | 25 | CV for color temperature analysis. Tablet mounted near forge. High value, strong niche data moat. |
| [[surgical-instrument-qc]] | 9 | 8 | 10 | 27 | Perfect CV use case. Controlled environment. Tablet-based. Ultimate data moat from Sialkot manufacturing. |
| [[telecom-tower-maintenance]] | 9 | 8 | 8 | 25 | CV for component ID + AR overlay on tablet. Remote assistance is a proven use case. |
| [[termite-detection-vision]] | 8 | 7 | 10 | 25 | CV for pattern recognition. Tablet-based. Very strong biological data moat. |
| [[textile-quality-control]] | 9 | 8 | 9 | 26 | High-speed CV on a fixed rig. Critical for Pakistan's largest export sector. Strong defect data moat. |
| [[truck-loading-optimizer]] | 8 | 8 | 7 | 23 | CV for dimensioning + optimization algorithm. Tablet-based. Good ROI, moderate moat. |
| [[underground-mine-safety]] | 6 | 6 | 9 | 21 | Requires specialized SLAM hardware. GPS-denied environment is a major challenge. |
| [[urban-planning-smart-cities]] | 5 | 5 | 8 | 18 | City-scale digital twins are massive data integration projects, not nimble MVPs. |
| [[vocational-ar-training]] | 7 | 7 | 8 | 22 | VR content creation is the main bottleneck. Pose estimation for technique assessment is feasible. |
| [[warehouse-vision-picker]] | 9 | 8 | 6 | 23 | Mature CV tech. Easy to deploy on existing devices. Low moat as it's a target for Big Tech (e.g., Amazon). |

## Top 10 Technical Picks

Ranked by total score, MVP feasibility, and alignment with technical preferences:

1.  **[[surgical-instrument-qc]]** - Score: 27
    -   Why: Perfect CV use case in a controlled environment. Tablet-first, offline-capable, and has the strongest possible technical moat from Sialkot's unique manufacturing data. 2-month MVP is highly feasible.

2.  **[[cookware-casting-scanner]]** - Score: 26
    -   Why: Simple, high-value CV (anomaly detection). Clear ROI, tablet-first, and a very strong, niche data moat from local recycled aluminum defects.

3.  **[[crop-disease-scouting]]** - Score: 26
    -   Why: Proven, high-impact CV application. Mobile-first, offline-capable, easy for agronomists to adopt. Localized pest/disease dataset creates a strong moat.

4.  **[[fan-motor-winding-qc]]** - Score: 26
    -   Why: Simple CV counting task with high ROI in preventing returns. Tablet-based, works in a factory setting. Moat from local fan motor designs is excellent.

5.  **[[glove-seam-inspector]]** - Score: 26
    -   Why: Straightforward CV for stitch counting to meet ISO standards. Critical for export compliance. Tablet-based and builds a strong industrial data moat.

6.  **[[sports-apparel-alignment]]** - Score: 26
    -   Why: Simple CV with AR overlay on a fixed rig. Solves the #1 cause of defects in a major export industry. Strong niche data moat from Sialkot cutting patterns.

7.  **[[textile-quality-control]]** - Score: 26
    -   Why: High-speed CV is a mature technology. Addresses the core need of Pakistan's largest export sector. The proprietary defect dataset is a world-class moat.

8.  **[[auto-parts-verification]]** - Score: 25
    -   Why: Straightforward CV on a tablet. Easy to deploy in supplier factories. Solves a key quality control problem for major local OEMs.

9.  **[[container-damage-logger]]** - Score: 25
    -   Why: Simple CV on a mobile device. Very easy to adopt for logistics personnel. Solves a major dispute resolution pain point.

10. **[[data-center-rack-guidance]]** - Score: 25
    -   Why: Feasible CV for port/cable ID. High-value in preventing costly outages. Can be deployed on existing enterprise mobile devices.

## Category Breakdown

### Manufacturing & Industrial
**Top 3:**
1. surgical-instrument-qc (27) - Ultimate CV + Moat combination
2. cookware-casting-scanner (26) - Simple, high-value defect detection
3. fan-motor-winding-qc (26) - Easy CV, solves #1 return cause

### Agriculture
**Top 3:**
1. crop-disease-scouting (26) - Proven CV, mobile-first, huge impact
2. seed-purity-vision (25) - High-value microscopic CV, very strong moat
3. fruit-ripeness-grading (25) - Simple CV, critical for export quality

### Logistics & Warehouse
**Top 3:**
1. container-damage-logger (25) - Easy CV, solves major pain point
2. last-mile-condition-log (25) - Simple CV on any smartphone, high adoption
3. port-tally-assistant (24) - High-value anti-theft tool, easy deployment

### Healthcare & Medical
**Top 3:**
1. diabetic-ulcer-monitor (25) - High-impact CV, strong medical data moat
2. pharma-gmp-compliance (23) - Feasible CV, ultimate compliance moat
3. medical-rehabilitation-assistant (22) - Mature pose-estimation tech, strong clinical moat

### Construction & Real Estate
**Top 3:**
1. construction-cost-intelligence (23) - Feasible CV, high value
2. construction-progress-monitoring (23) - Feasible with expertise
3. construction-bim-tracker (21) - High value but technically complex

## Technical Insights

**Highest Technical Feasibility (Quality 9-10):**
-   Ideas leveraging simple, proven 2D computer vision (classification, object detection, OCR, anomaly detection) are the most feasible for rapid MVP development.
-   Solutions that can be deployed on existing mobile/tablet hardware without custom sensors are heavily favored.
-   Examples: [[auto-parts-verification]], [[container-damage-logger]], [[crop-disease-scouting]], [[retail-display-compliance]].

**Easiest Deployment (Adoption 8-10):**
-   The easiest ideas to deploy are smartphone/tablet-based apps that require minimal changes to existing workflows and can function offline.
-   These solutions have a low barrier to entry for users and require minimal training.
-   Examples: [[container-damage-logger]], [[last-mile-condition-log]], [[retail-display-compliance]].

**Strongest Technical Moat (Moat 9-10):**
-   The strongest moats come from collecting unique, proprietary visual datasets in niche, hard-to-access Pakistani industrial or biological environments.
-   These datasets make it nearly impossible for a global competitor to replicate the solution's accuracy without spending years on data collection.
-   Examples: [[surgical-instrument-qc]], [[termite-detection-vision]], [[pharma-gmp-compliance]], [[defense-maintenance-training]].

**High Risk - Avoid for MVP:**
-   Ideas requiring complex 3D reconstruction, real-time SLAM, sensor fusion (beyond RGB+thermal), or integration with high-end, specialized hardware (LiDAR, GPR, medical scanners) are high-risk.
-   These projects involve significant R&D, have long development timelines, and are not suitable for initial MVPs.
-   Examples: [[nuclear-decommissioning]], [[semiconductor-euv-maintenance]], [[spinal-fusion-xray-vision]], [[brownfield-digital-twins]].

## Related Pages
[[b2b-evaluation-criteria-technical]]
[[b2b-ideas-scoring-report]]
[[pakistan-b2b-ideas-database]]