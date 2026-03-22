---
name: "alien-bioluminescent"
description: "An alien planet with bioluminescent mushroom trees, crystal formations, floating jellyfish, glowing liquid pools, crystal tone puzzles, and a ringed moon"
user-invocable: true
metadata:
  emoji: "🍄"
  type: "world"
  version: "2.0"
  genre: "Sci-Fi / Exploration / Puzzle"
  complexity: "high"
  estimated_entities: 110
  features: [terrain, water_emissive, npcs, dialogue, triggers_click, triggers_proximity, signs, hud, spatial_audio, orbit_behavior, path_follow, emissive_lighting, linked_entities]
  seo:
    primary_keyword: "alien planet 3D"
    secondary_keywords: ["bioluminescent world template", "alien environment 3D"]
useWhen: [{contains: "alien planet"}, {contains: "bioluminescent"}, {contains: "alien world"}]
---

# Alien Bioluminescent World — "First Contact"

First-person exploration of an alien landscape lit entirely by bioluminescence. Follow glowing trail markers to the Nexus Pool at the center. 4 crystal resonance puzzles: click crystals in sequence to unlock the next path segment. A floating alien guide speaks in fragments. No sun — only living light.

## Design Intent

**Awe through otherness.** Nothing in this world has an Earth analog. Mushroom "trees" with torus caps glow teal and violet. Crystals hum with audible tones. Jellyfish float overhead trailing tendrils. The ground cover pulses. The only constant is darkness punctuated by living light. The alien guide's fragmented speech ("...light...follow...center...") suggests intelligence without comprehension.

## Key Constraints

- NO directional sunlight. All illumination from emissive materials + point lights
- Every major structure has a matching-color point light underneath
- Bioluminescent flora PULSE at different frequencies (0.3–0.8) — breathing rhythm
- Crystal puzzles require click triggers + entity linking (click A then B then C in order)
- Alien guide uses path_follow at heights 3–8 (floating above player)
- Background is near-black [0.02, 0.01, 0.08]
- Ambient ≤ 0.06

## Player

```
camera_mode: "first_person"
walk_speed: 4.0, run_speed: 7.0, jump_force: 6.0
spawn: [0, 1, -20] (edge of world, facing bioluminescent glow)
HUD: "Resonance: 0 / 4" top-right, soft purple
```
