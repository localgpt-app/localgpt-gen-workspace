---
name: "medieval-village"
description: "A cozy medieval fantasy village with NPC quest, collectible medallions, interactive doors, market square, and explorable cottages at sunset"
user-invocable: true
metadata:
  emoji: "🏰"
  type: "world"
  version: "2.0"
  genre: "RPG / Exploration / Quest"
  complexity: "medium"
  estimated_entities: 120
  features:
    - terrain
    - water
    - npcs
    - dialogue
    - collectibles
    - doors
    - signs
    - hud
    - spatial_audio
    - ambience
    - day_night_lighting
  seo:
    primary_keyword: "3D medieval village template"
    secondary_keywords:
      - "fantasy village 3D environment"
      - "medieval RPG game world"
      - "AI generated medieval village"
    landing_page: "/templates/fantasy/medieval-village/"
useWhen:
  - contains: "medieval"
  - contains: "village"
  - contains: "fantasy village"
  - contains: "rpg town"
  - contains: "cottage"
---

# Medieval Fantasy Village — "The Market Quest"

A cozy medieval fantasy village nestled in rolling hills with a river crossing, five cottages, a market square, a church tower, a blacksmith forge, and a quest to find five lost medallions. Built for third-person exploration with NPC dialogue, interactive doors, spatial audio, and a sunset atmosphere.

## World Knowledge Index

| Domain | Spec File | Data File | Description |
|--------|-----------|-----------|-------------|
| Master plan | `world.md` | `world.ron` | Regions, phases, generation order |
| Layout | `layout/blockout.md` | `layout/blockout.ron` | Spatial grid, zone placement, sightlines |
| Village center | `regions/village-center.md` | `regions/village-center.ron` | Market square, well, church, 3 cottages |
| River crossing | `regions/river-crossing.md` | `regions/river-crossing.ron` | Bridge, pond, waterwheel, 2 cottages |
| Forest edge | `regions/forest-edge.md` | `regions/forest-edge.ron` | Tree line, old oak, mushroom ring, path entry |
| Village life | `behaviors/village-life.md` | `behaviors/village-life.ron` | NPC wander, door open/close, smoke rise, wind sway |
| Soundscape | `audio/ambient-soundscape.md` | `audio/ambient-soundscape.ron` | Forest birds, river water, forge fire, wind layers |
| Player | `avatar/player.md` | `avatar/player.ron` | Spawn, movement, camera, quest state |

## Generation Strategy

This world uses **iterative region-based generation**:

1. **Terrain first** — Generate rolling hills with river channel using perlin noise
2. **Layout blockout** — Place region bounding volumes on terrain
3. **Village center** — Market square anchors the world; build outward from here
4. **River crossing** — Bridge and waterside cottages, establish water audio zone
5. **Forest edge** — Tree line frames the village, entry path, old oak quest location
6. **Behaviors** — Attach NPC patrol, door triggers, collectible pickups
7. **Audio** — Layer spatial emitters over ambient soundscape
8. **Avatar** — Player spawn at village gate, quest HUD, camera setup
9. **Polish pass** — Verify colliders on all structures, test door triggers, balance lighting

## Design Intent

The village should feel **lived-in and warm**, not pristine. Cottages vary in size and color. The dirt path is worn and organic, not geometric. Trees are scattered naturally, not in rows. The sunset lighting casts long shadows that make the market square feel intimate.

The quest is simple by design — find 5 glowing medallions hidden in obvious-but-rewarding spots. The goal is exploration motivation, not difficulty. Every NPC gives a hint. Every medallion is visible if you look carefully.

## Key Constraints

- All structures built from geometric primitives (cuboids, cylinders, cones, spheres)
- No imported mesh assets — pure procedural composition
- Every walkable structure needs a collider
- Doors must have both visual entity AND trigger + animation
- NPCs use default_humanoid model until character meshes are available
- Water uses alpha-blended flat geometry, not shader-based waves
- Terrain height baseline ≈ half the height_scale parameter; manually offset entity Y positions

## Playtest Checklist

- [ ] Player can walk entire path from gate to river without clipping through anything
- [ ] All 5 medallions are reachable and collectible
- [ ] HUD updates on each medallion pickup
- [ ] Elder Aldric's dialogue triggers on approach
- [ ] All 3 interactive doors open and close correctly
- [ ] Water audio fades with distance from river/pond
- [ ] Forge fire audio is audible from inside and faintly outside
- [ ] No entity is floating above ground or buried below it
- [ ] Camera doesn't clip through church tower roof
- [ ] Sunset lighting creates visible shadows on market square
