# Cyberpunk Neon City — World Specification

## World Parameters

| Parameter | Value |
|-----------|-------|
| World size | 40×40 units (street) + rooftops to Y=25 |
| Terrain | Flat dark asphalt [0.08, 0.08, 0.1, 1], metallic 0.2, roughness 0.4 |
| Time of day | Night (perpetual) |
| Weather | Rain (audio only) |
| Player start | [0, 1, -25] first-person, facing north |

## Region Map

```
┌──────────────────────────┐  Y=25  THE SUMMIT (chip 3)
│     SKY BRIDGE           │  Y=18  Moving platform
│  (rooftop connections)   │  Y=15  Telepad 1 landing
├──────────────────────────┤
│ Towers │ Street │ Towers │  Y=0   STREET LEVEL
│  West  │Corridor│  East  │        (spawn, Fixer NPC)
├──────────────────────────┤
│       STREET START       │  z=-25 Player spawn
└──────────────────────────┘
```

## Generation Phases

1. Ground plane (dark, wet-look PBR) + road center line (emissive yellow)
2. 10 skyscrapers: cuboids, heights 8–25, dark [0.05–0.1], arranged along street corridor
3. Window strips: emissive planes as children on 6 buildings (cyan + magenta alternating)
4. 8 neon signs: emissive planes on walls, 3 with pulse behavior (varied frequencies)
5. 6 streetlights: cylinder + sphere + point light (warm white, 500 lux, range 8)
6. 3 steam vents: transparent spheres with bob (amplitude 1.5, freq 0.4)
7. 2 holographic torus rings: emissive cyan, spinning (30 deg/s) + bob
8. 3 teleporter pads: cylinder (emissive, pulsing) → rooftop destinations
9. Rooftop walkways: cuboid platforms connecting buildings at Y=15-22
10. 1 moving platform: kinematic cuboid on path_follow loop at Y=18
11. 3 data chips: small cuboids with cyan emissive, spinning, on rooftops
12. Portal archway: large torus at street end, emissive purple, slow spin
13. Street Fixer NPC at ground level with hint dialogue
14. Audio: rain + hum + bass emitters
15. Colliders on ALL buildings + platforms; kill zone at Y < -2

## Environment

```
background: [0.02, 0.01, 0.05, 1]
ambient: 0.03, color [0.5, 0.5, 1, 1]
NO directional sun
4 colored point lights: 2 cyan, 1 magenta, 1 amber (intensity 500-700, range 8-12)
```

## Teleporter Connections

| Pad | Ground Position | Destination | Effect |
|-----|----------------|-------------|--------|
| telepad_1 | [5, 0.05, 8] | [5, 15, 8] | fade |
| telepad_2 | [-10, 0.05, -5] | [-10, 22, -5] | particles |
| telepad_3 | [12, 15, 8] | [0, 25, 0] | fade |

## NPC: Street Fixer

Position: [3, 0, 12]. Dialogue:
- "Looking for data? Three chips are hidden across the rooftops. Get to high ground."
- Hint: "See those blue pads on the ground? Step on one. Trust me."
- Identity: "Nobody you need to know."

## HUD

- Top-right: "DATA CHIPS: 0 / 3" (cyan #00ffff, font 18)
- Kill zone respawn: Y < -2 → teleport to [0, 1, -25]
