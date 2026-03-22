---
name: "backrooms"
description: "An unsettling liminal backrooms space with fluorescent-lit yellow corridors, flickering lights, maze navigation, and oppressive silence"
user-invocable: true
metadata:
  emoji: "🟡"
  type: "world"
  version: "2.0"
  genre: "Horror / Puzzle / Liminal"
  complexity: "medium"
  estimated_entities: 60
  features: [triggers_timer, teleporters, signs, spatial_audio, flickering_lights]
  seo:
    primary_keyword: "backrooms 3D"
    secondary_keywords: ["liminal space environment", "backrooms game template"]
useWhen: [{contains: "backrooms"}, {contains: "liminal space"}, {contains: "liminal"}]
---

# Liminal Spaces / Backrooms — "Find the Exit"

First-person horror puzzle. Navigate identical-looking fluorescent corridors. Find the ONE real exit among 4 fake exits (3 loop you back to start via hidden teleporters). A red sphere sits in one corridor. A chair faces a blank wall. The lights buzz and flicker. There is no music. No wind. No life.

## Design Intent

**Wrongness through repetition.** The horror is architectural: identical rooms, too-regular columns, an exit sign pointing at a dead end. Slow movement. No HUD (disorientation is the game). The player's only tool is spatial memory — learning which corridors loop and which don't.

## Key Constraints

- First-person ONLY
- Very slow: walk 2.5, run 4.0
- NO HUD — no map, no compass, no objective marker
- Fluorescent point lights ONLY (no directional sun, no ambient above 0.08)
- 3 fake exits: teleporters that silently loop player to start
- 1 real exit: door that opens to white void (victory)
- Yellow-beige palette ONLY: [0.45–0.6, 0.4–0.58, 0.25–0.45]
- NO organic sound: no birds, no wind, no water. Only electrical hum.

## Player

```
camera_mode: "first_person"
walk_speed: 2.5, run_speed: 4.0, jump_force: 3.0
spawn: [0, 1.6, 0] (center of initial room)
NO HUD
```
