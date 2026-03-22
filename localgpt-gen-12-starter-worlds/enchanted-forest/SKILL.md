---
name: "enchanted-forest"
description: "A magical enchanted forest with glowing mushrooms, firefly paths, a fairy ring ritual, 7 collectible orbs, and a forest spirit NPC"
user-invocable: true
metadata:
  emoji: "🧚"
  type: "world"
  version: "2.0"
  genre: "Peaceful Exploration / Collection"
  complexity: "medium"
  estimated_entities: 110
  features: [terrain, water, npcs, dialogue, collectibles, signs, hud, spatial_audio, path_follow, emissive_lighting]
  seo:
    primary_keyword: "enchanted forest 3D"
    secondary_keywords: ["magical forest environment", "fantasy forest template", "fairy forest 3D"]
useWhen:
  - contains: "enchanted forest"
  - contains: "magical forest"
  - contains: "fairy forest"
---

# Enchanted Forest — "The Fairy Ring Ritual"

A peaceful magical forest with glowing mushrooms, firefly paths, a winding stream, and a fairy ring. Player finds 7 magical orbs hidden among ancient trees and places them to complete a ritual that awakens a sleeping forest spirit.

## Generation Strategy

1. Terrain: rolling hills (perlin, octaves 5, height_scale 12, seed 7777)
2. Water: stream (height 1.0, size [20,30])
3. Path from entry to fairy ring (dirt, curved, width 1.5)
4. Trees: 8 oaks + 7 birches with staggered wind-sway bob
5. Magical elements: 8 glowing mushrooms (cone+cylinder, emissive, pulse), 10 fireflies (path_follow loops), fairy ring (7 stone pedestals)
6. Stream with stepping stones and water audio
7. 7 orbs scattered through forest (each unique emissive color)
8. Forest spirit NPC at fairy ring (sleeping until all orbs collected)
9. Audio: forest ambience + stream + wind layers

## Design Intent

**Wonder, not challenge.** Movement speed normal. No enemies. No timer. The joy is in discovery — finding each orb, watching fireflies, hearing the stream grow louder. The fairy ring activation is the emotional peak: all pedestals glow, the spirit speaks.

## Key Constraints

- Third-person camera (shows the beautiful canopy)
- Orbs have unique colors: Dawn (gold), Dusk (purple), Stream (blue), Moss (green), Ember (orange), Frost (white-blue), Shadow (dark violet)
- Fairy ring: 7 stone cylinder pedestals in a circle (radius 2.5)
- Spirit NPC has 2 states: sleeping (before quest) and awakened (after all 7 collected)
- Fireflies must have UNIQUE paths (no two fly the same route)
- Mushroom pulse frequencies varied 0.4–0.8 (not synchronized)
