# Apple ARKit Scene Understanding

**Summary**: Apple's ARKit framework provides scene understanding capabilities including surface detection, environmental mapping, and body tracking for iOS/iPadOS devices.

**Sources**: `Scene_Understanding_Object_Recognition_Landscape_2026-04-21.md`

**Last updated**: 2026-04-21

---

## What ARKit Provides

ARKit offers several APIs for understanding the physical environment:

- **World Tracking**: Device pose estimation in 3D space using Visual-Inertial SLAM
- **Scene Understanding**: Detects surfaces (floors, walls, ceilings, tables) for virtual object placement
- **Environment Mapping**: Estimates lighting for realistic virtual object rendering
- **Body Tracking**: Tracks body pose and joints for AR fitness and motion capture

## Capabilities

| Capability | Status | Notes |
|------------|--------|-------|
| Surface detection | Proven | Floors, walls, tables, ceilings |
| Object recognition | Limited | Predefined classes only |
| Body tracking | Proven | Person pose and joints |
| Lighting estimation | Proven | Environmental lighting |
| Persistent maps | Limited | ARKit World Map not session-persistent |

## Hardware Integration

- Runs on-device via Apple Silicon (M-series chips)
- Hardware acceleration through Neural Engine
- LiDAR-equipped devices (iPhone Pro, iPad Pro) get enhanced depth

## Strategic Implications

- ARKit is the gateway for AR experiences on 600M+ Apple devices
- Scene Understanding focuses on spatial mapping rather than semantic depth
- Limited persistent memory across sessions
- Source: [Apple Developer ARKit](https://developer.apple.com/documentation/arkit)

## Related pages

- [[slam]]
- [[spatial-ai-assistant]]
- [[xr-hardware]]