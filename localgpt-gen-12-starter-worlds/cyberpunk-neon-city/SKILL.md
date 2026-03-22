---
name: "cyberpunk-neon-city"
description: "A rain-soaked cyberpunk city block with neon signs, rooftop parkour, teleporter pads, data chip collectibles, and moody purple-blue atmosphere"
user-invocable: true
metadata:
  emoji: "🌃"
  type: "world"
  version: "2.0"
  genre: "Exploration / Parkour / Sci-Fi"
  estimated_entities: 130
  features: [teleporters, collectibles, moving_platforms, npcs, dialogue, signs, hud, spatial_audio, emissive_lighting]
  seo:
    primary_keyword: "cyberpunk city 3D"
    secondary_keywords: ["neon city environment template", "cyberpunk game world AI"]
useWhen: [{contains: "cyberpunk"}, {contains: "neon city"}, {contains: "sci-fi city"}]
---

# Cyberpunk Neon City — "Neon Runner"

A rain-soaked cyberpunk city block at night. Dense skyscrapers with neon signs line a central street. First-person. Player uses teleporter pads to reach rooftops, collects 3 data chips, navigates a moving platform between buildings.

## Generation Strategy

1. Flat dark asphalt plane (40×40), wet-street PBR
2. 10 skyscrapers (heights 8–25), dark materials, box colliders
3. Street: road lanes, 6 streetlights, steam vents, neon signs
4. Emissive layer: window strips, holographic rings, pulsing signs
5. 3 teleporter pads (ground→rooftop) + 1 moving platform (Y=18)
6. 3 data chips on rooftops (cyan emissive, spinning)
7. Street Fixer NPC with hint dialogue
8. Audio: rain + hum + bass + rooftop wind
9. Kill zone at Y<-2 → respawn at street level

## Design Intent

**Oppressive and beautiful.** Night only. No sun. Neon is the ONLY color. Wet streets reflect. Player motivation is vertical: get UP. First-person maximizes the canyon effect of looking up at towers.

## Player

```
camera_mode: "first_person"
walk_speed: 6, run_speed: 12, jump_force: 9
spawn: [0, 1, -25]
HUD: "DATA CHIPS: 0/3" top-right, cyan #00ffff
```
