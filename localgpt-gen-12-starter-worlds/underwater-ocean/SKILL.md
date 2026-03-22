---
name: "underwater-ocean"
description: "A vibrant underwater ocean with coral reef, tropical fish, pollution cleanup quest, sunken treasure, and caustic light rays"
user-invocable: true
metadata:
  emoji: "🐠"
  type: "world"
  version: "2.0"
  genre: "Peaceful Exploration / Environmental"
  estimated_entities: 100
  features: [water, collectibles, npcs, dialogue, signs, hud, spatial_audio, path_follow, physics_gravity]
  seo:
    primary_keyword: "underwater 3D world"
    secondary_keywords: ["ocean environment template", "coral reef 3D scene"]
useWhen: [{contains: "underwater"}, {contains: "ocean world"}, {contains: "coral reef"}]
---

# Underwater Ocean World — "Reef Rescue"

First-person underwater exploration. Clean 6 pieces of pollution from the coral reef. As trash is removed, coral sections "heal" — changing from gray to vibrant color. A friendly turtle NPC guides the player. Sunken treasure chest is a bonus find.

## Design Intent

**Serene activism.** Slow movement (underwater feel), low gravity (0.1), muffled audio. The reward is visual transformation: gray dead coral blooming into color as pollution is removed. No timer, no enemies. The turtle is gentle encouragement.

## Player

```
camera_mode: "first_person"
walk_speed: 3.0        # underwater slowness
run_speed: 5.0         # swimming burst
jump_force: 4.0
gravity_scale: 0.1      # buoyancy
spawn: [0, 3, 15]       # above the reef, looking down
HUD: "Reef Health: 0%" top-left, cyan
```
