# Open-Source Scene Understanding Models

**Summary**: Open-source models including SAM, GroundingDINO, and YOLO-World provide flexible, zero-shot segmentation and object detection capabilities for spatial AI applications.

**Sources**: `Scene_Understanding_Object_Recognition_Landscape_2026-04-21.md`

**Last updated**: 2026-04-21

---

## ConceptFusion: The Synthesis

[[ConceptFusion]] (MIT/CMU, 2023) is the state-of-the-art integration of open-source scene understanding models into a unified semantic 3D mapping system. It combines SAM, CLIP, and DINO to build 3D scene maps where every point carries rich semantic embeddings queryable by any modality — text, image, audio, or click — with no task-specific training.

Key result: >40% mIoU improvement over LSeg and OpenSeg (both trained for specific tasks) in **zero-shot** mode. ConceptFusion is currently the most capable open-source framework for semantic 3D scene understanding. See the dedicated [[conceptfusion]] page for full details.

---

## Key Models

### Segment Anything Model (SAM)

- Universal segmentation model trained on 11M images and 1.1B masks
- Promptable: works with points, boxes, or text inputs
- Can segment any object without class-specific training
- Source: [Ultralytics SAM Docs](https://docs.ultralytics.com/models/sam/)

### GroundingDINO

- Open-set object detector that generalizes to unseen classes
- Combines vision and language for zero-shot detection
- Used with SAM in "Grounded SAM" for improved open-world segmentation
- Source: [Grounding DINO (ECCV 2024)](https://github.com/idea-research/groundingdino)

### YOLO-World

- Evolution of YOLO architecture toward open-world detection
- Real-time performance with vocabulary expansion
- Optimized for edge deployment

## Capabilities Comparison

| Model | Strength | Limitation | Compute Need |
|-------|----------|------------|--------------|
| SAM | Universal segmentation | Requires prompts | GPU/High |
| GroundingDINO | Zero-shot detection | Less precise masks | GPU |
| YOLO-World | Real-time speed | Limited vocabulary | Medium |

## Edge Deployment

- Research advancing for mobile/edge optimization
- ONNX and TensorRT export available
- Quantization reduces size for mobile inference
- Not yet at real-time on lightweight glasses

## Strategic Implications

- Open-source models offer flexibility no platform matches
- Zero-shot capabilities enable new use cases without retraining
- Key gap: optimization for real-time wearable use
- Opportunity: build optimized inference layer for spatial AI

## Related pages

- [[conceptfusion]]
- [[slam]]
- [[splatam]]
- [[spatial-ai-assistant]]
- [[ego-centric-3d-perception]]
- [[xr-hardware]]
- [[genai-animation]]