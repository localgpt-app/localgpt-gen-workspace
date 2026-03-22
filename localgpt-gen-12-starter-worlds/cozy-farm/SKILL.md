---
name: "cozy-farm"
description: "A warm cozy farm with farmhouse, red barn, spinning windmill, wheat fields, sheep paddock, crop harvesting quest, and golden sunset"
user-invocable: true
metadata:
  emoji: "🌾"
  type: "world"
  version: "2.0"
  genre: "Cozy / Farming Sim"
  estimated_entities: 120
  features: [terrain, water, collectibles_respawn, npcs, dialogue, triggers_click, signs, hud, spatial_audio, spin_behavior]
  seo:
    primary_keyword: "cozy farm 3D"
    secondary_keywords: ["farming game environment template", "cozy village 3D"]
useWhen: [{contains: "cozy farm"}, {contains: "farm village"}, {contains: "farming"}]
---

# Cozy Farm Village — "Harvest Day"

Third-person farming world. Collect 10 crops from fields (click to harvest), deliver them to the barn, pet the animals. The windmill spins lazily. Wheat sways in the breeze. Golden sunset bathes everything in warm light.

## Design Intent

**Warm and unhurried.** No timer, no fail state. Crops respawn after 30 seconds so you can keep harvesting. The joy is in the rhythmic loop: harvest → deliver → hear the satisfying "ding" → watch score climb. The sheep bob gently (breathing). Smoke curls from the chimney. Everything is safe.

## Key Elements

- Farmhouse (cream walls, red roof, glowing windows, chimney with smoke puffs)
- Red barn (classic, with double doors)
- Spinning windmill (cylinder tower + 4 blade planes on spinning parent)
- 3 crop fields: wheat (40 thin golden cylinders with wind bob), vegetables (green spheres), flowers (colorful tiny spheres)
- Sheep paddock: 3 white sphere "sheep" with legs, fence enclosure
- Pond with wooden dock, water emitter
- Hay bales near barn (golden cuboids)

## Quest: Harvest 10 Crops

Click on crop entities → they disappear (with chime sound) → respawn after 30s. Walk to barn → area_enter trigger registers delivery. HUD tracks "Crops Harvested: 0/10."

## Player

```
camera_mode: "third_person", camera_distance: 6
walk_speed: 5.0, run_speed: 9.0, jump_force: 7.0
spawn: [0, 1, -12] (farmhouse porch)
HUD: "Crops Harvested: 0 / 10" top-left, warm gold
```

## Environment

```
background: [0.7, 0.55, 0.4, 1]       # warm sunset sky
ambient: 0.2, color [1, 0.95, 0.85]
sun: golden [1, 0.9, 0.65], intensity 3, direction [-0.6, -1, -0.3], shadows on
```
