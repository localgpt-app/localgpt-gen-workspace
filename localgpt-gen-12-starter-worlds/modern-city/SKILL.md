---
name: "modern-city"
description: "A modern city block with glass towers, park, fountain, timed delivery quest, street-level exploration, and bus route"
user-invocable: true
metadata:
  emoji: "🏙️"
  type: "world"
  version: "2.0"
  genre: "Exploration / Time Challenge"
  estimated_entities: 120
  features: [terrain_flat, collectibles, triggers_timer, triggers_area, signs, hud, spatial_audio, physics_kinematic]
  seo:
    primary_keyword: "3D city environment"
    secondary_keywords: ["modern urban template", "city block 3D world"]
useWhen: [{contains: "modern city"}, {contains: "urban environment"}, {contains: "city block"}]
---

# Modern City Block — "Delivery Dash"

Third-person exploration of a modern city block with glass towers, a park with fountain, and a timed delivery quest. Pick up 5 packages and deliver them to marked buildings before time runs out. A bus follows a looping route the player can ride.

## Design Intent

**Busy and bright.** Daylight, blue sky, glass reflections. The city feels alive through movement: spinning bus wheels, bobbing fountain, NPC pedestrians. Timer creates urgency without punishment — running out just resets the packages.

## Key Features

- 12 buildings: 3 glass towers, 4 offices, 2 apartments, 2 retail, 1 curved cylinder tower
- Park with 5 trees, bench, bobbing fountain with water audio
- 4 simplified cars (parked cuboid shapes)
- 8 streetlights with warm point lights
- Bus on kinematic path_follow loop (rideable moving platform)
- 5 packages as collectibles, 5 delivery zones as area_enter triggers
- Timer HUD counting down from 120 seconds

## Player

```
camera_mode: "third_person", camera_distance: 7
walk_speed: 5.5, run_speed: 11.0, jump_force: 7.0
spawn: [0, 1, -15]
HUD: timer top-center + "Packages: 0/5" top-right
```
