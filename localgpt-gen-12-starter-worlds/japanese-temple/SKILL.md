---
name: "japanese-temple"
description: "A serene Japanese temple with zen garden, koi pond, cherry blossom trees, torii gate, and a meditation path quest with 5 haiku stations"
user-invocable: true
metadata:
  emoji: "⛩️"
  type: "world"
  version: "2.0"
  genre: "Walking Sim / Meditation"
  estimated_entities: 100
  features: [terrain, water, npcs, dialogue, triggers_proximity, doors_with_keys, signs, hud, spatial_audio, path_follow]
  seo:
    primary_keyword: "Japanese temple 3D"
    secondary_keywords: ["zen garden environment", "Japanese garden template"]
useWhen: [{contains: "japanese temple"}, {contains: "zen garden"}, {contains: "cherry blossom"}]
---

# Japanese Temple & Gardens — "The Meditation Path"

Peaceful walking sim through a temple complex. Follow a guided path through the garden, interacting with 5 meditation stations. Each shows a haiku and lights a stone lantern. Complete all 5 to unlock the inner temple door and hear the monk's final teaching.

## Design Intent

**Stillness.** Slow walk speed (4.0). Third-person to appreciate the landscape. Every element is placed with Japanese garden principles: asymmetry, borrowed scenery, hidden-and-revealed views. The torii gate frames the temple. Cherry blossoms drift. Koi circle endlessly. The quest is contemplative, not urgent.

## Key Elements

- Torii gate (2 red cylinders + 2 horizontal beams) at garden entrance
- Temple: raised platform, dark wood body, tiered pyramid roofs, 6 red pillars
- Zen garden: pale sand plane with 5 asymmetric rock groupings (2-3 pattern)
- Koi pond: flat cylinder (blue, alpha blend), 3 fish on path_follow ovals
- 4 cherry blossom trees: pink sphere canopies + falling petal path_follow
- 5 meditation stations: stone cylinders with proximity trigger → show haiku text
- 3 stone lanterns: cylinder+cuboid+pyramid with warm point lights
- Bamboo fence: row of thin green cylinders
- Monk NPC at inner temple

## Player

```
camera_mode: "third_person", camera_distance: 5
walk_speed: 4.0, run_speed: 6.5, jump_force: 5.0
spawn: [0, 1, -15] (outside torii gate)
HUD: "Meditations: 0 / 5" top-left, soft gold
```
