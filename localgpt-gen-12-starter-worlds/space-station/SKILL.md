---
name: "space-station"
description: "A modular sci-fi space station with rotating rings, zero-g modules, 4 repair objectives, approaching shuttle, and asteroid debris"
user-invocable: true
metadata:
  emoji: "🚀"
  type: "world"
  version: "2.0"
  genre: "Sci-Fi / Exploration / Repair"
  complexity: "high"
  estimated_entities: 100
  features: [teleporters, collectibles, npcs, dialogue, signs, hud, spatial_audio, physics_gravity, spin_behavior, path_follow]
  seo:
    primary_keyword: "space station 3D"
    secondary_keywords: ["sci-fi corridor environment", "space station template", "zero gravity 3D world"]
useWhen:
  - contains: "space station"
  - contains: "sci-fi station"
  - contains: "zero gravity"
---

# Sci-Fi Space Station — "Docking Protocol"

First-person exploration of a modular space station. Repair 4 failing systems (life support, comms, engine, navigation) by finding parts in different modules. Teleporters connect modules. An AI companion gives guidance via radio dialogue. A shuttle slowly approaches the docking bay.

## Generation Strategy

1. Space background (near-black, very low ambient)
2. Central hub cylinder + 4 torus ring sections (1 rotating at 3 deg/s)
3. 4 extending arms with endpoint modules
4. Solar panels (flat planes, slow spin tracking)
5. Docking bay frame with green pulse guide lights
6. Shuttle on path_follow approaching dock
7. 20 star spheres + 3 tumbling asteroid icosahedrons
8. Teleporters connecting hub ↔ each arm module
9. 4 repair part collectibles (1 per module)
10. AI companion NPC with radio dialogue (hint system)
11. Reactor hum audio at core + radio static at dock

## Design Intent

**Isolation and wonder.** Harsh sunlight from one direction, deep shadows everywhere else. The station is functional, not beautiful — industrial grays and blues. The rotating ring is hypnotic. The approaching shuttle creates urgency without a timer.

## Player

```
camera_mode: "first_person"
walk_speed: 4.0         # magnetic boots pace
run_speed: 7.0
jump_force: 12.0        # low gravity allows high jumps
gravity_scale: 0.3       # low-g feel
spawn: [0, 1, 0]        # hub center
HUD: "Systems Repaired: 0 / 4" top-right, blue-white
```
