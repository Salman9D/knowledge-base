# Google Scene Semantics API

**Summary**: Google's Scene Semantics API provides real-time pixel-level semantic labeling of environments as part of the Android XR and ARCore ecosystem.

**Sources**: `Scene_Understanding_Object_Recognition_Landscape_2026-04-21.md`

**Last updated**: 2026-04-21

---

## What Scene Semantics Provides

- **Pixel-wise Semantic Labeling**: Classifies each pixel in the camera view
- **Object Categories**: Floors, walls, ceilings, furniture, vehicles, people, pets
- **Indoor/Outdoor Support**: Broad environmental coverage
- **Real-time Performance**: Low-latency inference via dedicated hardware

## Capabilities

| Capability | Status | Notes |
|------------|--------|-------|
| Pixel-level labeling | Proven | Per-pixel semantic classification |
| Object categories | Broad | 20+ semantic classes |
| Latency | Low | Hardware-accelerated via Hexagon DSP |
| Device support | Android XR | ARCore-compatible devices |
| Persistent memory | Limited | Session-based only |

## Hardware Integration

- Runs on Snapdragon XR platforms with Hexagon DSP co-processor
- Dedicated AI accelerator for on-device inference
- Power-efficient for mobile/glass form factors
- Source: [Google Scene Semantics API](https://developers.google.com/ar/develop/scene-semantics)

## Strategic Implications

- Leading semantic granularity among platform APIs
- Low latency enables real-time AR applications
- Integration with Android XR positions it for smart glasses
- Gap: no persistent spatial memory layer

## Related pages

- [[slam]]
- [[spatial-ai-assistant]]
- [[google-gemini-smart-glasses]]
- [[xr-platforms]]