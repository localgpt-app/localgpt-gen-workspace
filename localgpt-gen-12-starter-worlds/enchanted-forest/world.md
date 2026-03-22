# Enchanted Forest — World Specification

## World Parameters

| Parameter | Value |
|-----------|-------|
| World size | 80×80 |
| Terrain | Perlin, octaves 5, height_scale 12, seed 7777, grass |
| Water | Stream at height 1.0, size [20, 30] |
| Player start | [0, 1, -30] third-person |

## Regions

### Deep Woods (north)
- Dense tree canopy, darkest area
- Contains: 4 oaks, 3 birches, orb_shadow, orb_frost
- Mushroom clusters with teal/purple emissive

### Stream Valley (center)
- Winding stream with 3 stepping stones
- Contains: orb_stream (on stepping stone), orb_moss (stream bank)
- Water audio emitter (turbulence 0.4, radius 10)

### Fairy Ring Clearing (center-north)
- 7 stone pedestals in circle, radius 2.5 from [5, 0, 24]
- Willowmere spirit NPC at center
- Contains: orb placement triggers

### Entry Meadow (south)
- Open, fewer trees, path entrance
- Welcome feeling, sunlight dappled through edge trees
- Contains: orb_dawn (visible from path, easy first find), orb_ember (behind entry boulder)

## 7 Orbs Placement

| Orb | Color (emissive) | Location | Difficulty |
|-----|-----------------|----------|-----------|
| Dawn | [1, 0.8, 0.2, 1] gold | Path edge, visible | Easy |
| Ember | [1, 0.4, 0, 1] orange | Behind entry boulder | Easy |
| Stream | [0.2, 0.5, 1, 1] blue | On stepping stone | Medium |
| Moss | [0.2, 0.8, 0.3, 1] green | Stream bank, under fern | Medium |
| Dusk | [0.6, 0.2, 0.8, 1] purple | High in oak canopy | Hard |
| Frost | [0.7, 0.9, 1, 1] ice-blue | North clearing, among mushrooms | Medium |
| Shadow | [0.3, 0.1, 0.5, 1] violet | Deepest part of woods | Hard |

## Environment

```
background: [0.15, 0.25, 0.15, 1]    # misty forest green
ambient: 0.12, color [0.7, 1, 0.7]    # green canopy tint
sun: warm gold [1, 0.95, 0.7], intensity 2, direction [-0.3, -1, -0.2], shadows on
3 point lights near mushroom clusters: teal + purple, intensity 150, range 4
```

## NPC: Willowmere (Forest Spirit)

Position: [5, 0, 24] (fairy ring center)
- State 1 (sleeping): "The spirit sleeps. Its voice echoes: 'Gather the seven lights... return them to the stones...'"
- State 2 (awakened, condition orbs >= 7): "You have restored the circle! The forest breathes again."

## Quest Completion

All 7 orbs collected → approach fairy ring → all pedestals begin glowing (emissive white pulse) → spirit switches to awakened dialogue → celebration audio chime.

## Player: Third-Person Explorer

```
camera_mode: "third_person", camera_distance: 5
walk_speed: 4.5, run_speed: 8, jump_force: 6
spawn: [0, 1, -30]
HUD: "Orbs: 0 / 7" top-left, green #88ff88
```
