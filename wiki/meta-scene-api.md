# Meta Scene API

**Summary**: Meta's Scene API provides persistent spatial scene models across Horizon OS, enabling consistent environment understanding across apps on Quest headsets and Meta glasses.

**Sources**: `Scene_Understanding_Object_Recognition_Landscape_2026-04-21.md`

**Last updated**: 2026-04-21

---

## What Meta Scene API Provides

- **Persistent Scene Models**: Environment understanding that persists across sessions and is shared with other apps
- **Surface Detection**: Floors, walls, and spatial features for content placement
- **Physics Integration**: Enables virtual objects to interact with real surfaces
- **Mixed Reality Support**: Smooth passthrough with spatial awareness

## Capabilities

| Capability | Status | Notes |
|------------|--------|-------|
| Persistent scene memory | Yes | OS-persisted across apps |
| Surface detection | Proven | floors, walls, objects |
| Cross-app sharing | Yes | Scene model accessible to all apps |
| Real-time updates | Yes | As environment changes |
| Open-world detection | Limited | Focused on surfaces |

## Hardware Integration

- Runs on Qualcomm Snapdragon XR platforms
- Optimized for Quest 3, Quest Pro
- Accessible via Horizon OS developer APIs
- Source: [Meta Horizon Scene Understanding](https://developers.meta.com/horizon/design/mr-design-scene/)

## Strategic Implications

- Unique among platforms for app-to-app spatial memory sharing
- Enables consistent MR experiences across different apps
- Foundation for ambient spatial AI assistance
- Gap: limited semantic granularity (object classification)

## Related pages

- [[slam]]
- [[spatial-ai-assistant]]
- [[competitive-landscape]]
- [[meta-rayban-ai-glasses]]