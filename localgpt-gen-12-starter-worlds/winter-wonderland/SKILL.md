---
name: "winter-wonderland"
description: "A magical winter wonderland with frozen lake, snow-covered pines, cozy cabin, snowman parts collection quest, and falling snow"
user-invocable: true
metadata:
  emoji: "❄️"
  type: "world"
  version: "2.0"
  genre: "Cozy / Collection / Seasonal"
  estimated_entities: 90
  features: [terrain, collectibles, npcs, dialogue, signs, hud, spatial_audio, path_follow, ice_surface]
  seo:
    primary_keyword: "winter wonderland 3D"
    secondary_keywords: ["snow world template", "winter scene 3D environment"]
useWhen: [{contains: "winter wonderland"}, {contains: "snow world"}, {contains: "winter scene"}]
---

# Winter Wonderland — "Snowman Builder"

Collect 5 scattered snowman parts (hat, carrot nose, scarf, coal eyes, stick arms) around a frozen lake. Return to the snowman pedestal to build Frosty. A child NPC gives hints. Cabin glows warmly. Snow falls gently. Everything is peaceful and cold and beautiful.

## Design Intent

**Warmth within cold.** The landscape is white and blue — crisp, quiet. The cabin is the warm anchor: orange window glow, chimney smoke, fire crackle. The snowman quest gives purpose without pressure. The falling snow (path_follow particles) creates constant gentle movement.

## Player

```
camera_mode: "third_person", camera_distance: 6
walk_speed: 4.5 (slightly slower — trudging through snow)
run_speed: 8.0, jump_force: 6.0
spawn: [0, 1, -10] near cabin
HUD: "Snowman Parts: 0 / 5" top-left, white
```
