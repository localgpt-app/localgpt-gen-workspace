# Space Station — World Specification

## World Parameters

| Parameter | Value |
|-----------|-------|
| World size | 60×60×60 (3D space, no ground plane) |
| Terrain | None (space) |
| Background | [0.005, 0.005, 0.02, 1] deep space |
| Ambient | 0.05, cool blue [0.6, 0.7, 1] |
| Sun | Directional, pure white, intensity 5, direction [1, -0.3, 0.5], harsh shadows |

## Station Architecture

```
              Solar Panel (spin)
                   │
    Module N ──── ARM N ────┐
                            │
    Module W ─── ARM W ── HUB ── ARM E ─── Module E
                            │
    Module S ──── ARM S ────┘
                            │
                     Docking Bay
                     (shuttle approaching)
```

### Central Hub
- Cylinder (radius 4, height 3), metallic gray, metallic 0.7, roughness 0.3
- 4 torus rings at different rotations, metallic 0.8
- 1 ring has spin behavior (axis [0,0,1], speed 3 deg/s) — habitat ring
- Reactor hum: custom emitter (sine, 45Hz, warmth 0.9, radius 20, volume 0.2)

### Arms (4)
- Long cuboids (0.8×0.8×8), radiating at 90° intervals
- Each ends with a module cuboid (2×2×3) + antenna cylinder

### Modules (repair objectives)
| Module | Position | System | Repair Part |
|--------|----------|--------|-------------|
| North | [0, 0, 12] | Life Support | Oxygen Filter (capsule, green) |
| East | [12, 0, 0] | Communications | Relay Chip (cuboid, yellow) |
| South | [0, 0, -12] | Engine | Fuel Cell (cylinder, orange) |
| West | [-12, 0, 0] | Navigation | Star Chart (plane, blue) |

### Teleporter Network

| From | To | Direction |
|------|----|-----------|
| Hub center | Module N | Both ways |
| Hub center | Module E | Both ways |
| Hub center | Module S | Both ways |
| Hub center | Module W | Both ways |

### Docking Bay
- Open frame: 4 thin cylinders forming rectangle
- Green pulse guide lights on corners (4 spheres, emissive [0, 1, 0.3], pulse freq 0.8)
- Shuttle: cuboid body (1.5×0.8×3) + 2 wedge wings
- Shuttle on path_follow: 4 waypoints approaching dock, speed 0.3, mode "once"

### Stars & Debris
- 20 tiny emissive white spheres at large distances (stars)
- 3 icosahedron asteroids, spin (random axes, 5-10 deg/s), dark gray

## NPC: AI Companion "ARIA"

Radio-style dialogue (no visible model — voice only via proximity to comm panels):
- "Welcome aboard. Four critical systems are failing. I've marked repair parts in each module."
- Per-module hints when approaching empty module: "The oxygen filter should be in the storage rack."
- Completion: "All systems nominal. The shuttle can dock safely now."
