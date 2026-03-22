# Haunted House — World Specification

## World Parameters

| Parameter | Value |
|-----------|-------|
| World size | 40×40 (exterior) + 20×25 (interior floor plan) |
| Terrain | Perlin, octaves 2, height_scale 2, dark earth |
| Time of day | Night (full moon) |
| Player start | [0, 1, 0] inside foyer (trapped) |

## Interior Floor Plan

```
SECOND FLOOR:
┌─────────────────────┐
│  Master      Hallway │
│  Bedroom     (3×10)  │
│  (5×5)       narrow  │
│  [silver key]        │
└──────┬──────┬────────┘
       stairs

GROUND FLOOR:
┌──────┬──────┬────────┐
│      │Foyer │        │
│Library│(6×6)│Kitchen │
│(5×4) │START │(4×5)   │
│[rusty│      │[silver │
│ key] │      │  key]  │
└──────┴──┬───┴────────┘
          │trapdoor
    ┌─────┴──────┐
    │  Basement  │
    │   (6×6)    │
    │ [golden    │
    │   key]     │
    └────────────┘
```

## Room Specifications

### Foyer (spawn room)
- Size: 6×3×6 (walls 3 high)
- Chandelier: point light, golden, intensity 300, FLICKERING (timer trigger, interval 3.5s)
- Front door: LOCKED (requires golden_key), heavy iron sound
- "GET OUT" sign on wall: red text, font 36, billboard false
- Staircase: cuboid steps leading up to hallway

### Library (left wing)
- Size: 5×3×4
- 3 bookshelf cuboids against walls (dark brown, tall)
- Rusty key hidden on floor between shelf and wall [hard to spot without emissive]
- Door: click-to-open, creak sound
- THE CHAIR: cuboid seat + legs, starts in corner. Area_exit trigger moves it to room center (once)

### Kitchen (right wing)
- Size: 4×3×5
- Table (cuboid) + 2 chair primitives
- Counter (long cuboid against wall)
- Silver key on floor near counter base
- Door: proximity-open

### Upstairs Hallway
- Size: 3×3×10 (deliberately narrow and claustrophobic)
- 2 point lights, one flickering slowly (frequency 0.15 — dying bulb)
- Whisper trigger at midpoint (area_enter, once, play_sound "distant_whisper")

### Master Bedroom
- Size: 5×3×5
- Bed (cuboid frame + mattress cuboid), wardrobe (tall cuboid)
- Door: LOCKED (requires silver_key)
- NO light source — player must navigate by hallway spill light

### Basement
- Access: trapdoor in foyer floor (LOCKED, requires rusty_key)
- Size: 6×2.5×6 (lower ceiling = more oppressive)
- ONE dim point light (intensity 50, range 3, warm yellow)
- Golden key in far corner, barely lit
- Heavy footsteps trigger on stair descent (area_enter, once)
- "she never left" sign on wall: gray text, font 14, barely visible

## Environment

```
background: [0.02, 0.02, 0.06, 1]    # dark night
ambient: 0.02, color [0.5, 0.5, 0.8]  # cold blue
moonlight: directional, color [0.6, 0.6, 0.8], intensity 1.2, direction [-0.3, -1, -0.5], shadows on
moon: sphere at [10, 20, -15], scale [2,2,2], emissive [0.9, 0.9, 0.75, 0.8], unlit
```

## Audio: Silence Is The Horror

- Wind: speed 0.6, gustiness 0.7, volume 0.35
- Distant fire: intensity 0.2, crackle 0.8, radius 4, volume 0.15
- Ambient dread: brown_noise, cutoff 150, radius 20, volume 0.06
- **NO music. NO background melody. Pure environmental sound.**

## Scare Trigger Sequence

| Trigger | Location | Event | Plays |
|---------|----------|-------|-------|
| chair_move | Library exit | Chair teleports to center | Once |
| whisper | Hallway midpoint | "distant_whisper" sound | Once |
| footsteps_above | Basement stairs | "heavy_footsteps" sound | Once |
| door_slam | Bedroom entry | Distant door slam sound | Once |

## Player: First-Person, Slow, Vulnerable

```
camera_mode: "first_person"
walk_speed: 3.5    # deliberately slow
run_speed: 6.0     # can't outrun fear
jump_force: 5.0
spawn: [0, 1, 0]   # foyer center
```

HUD: "Keys: 0 / 3" bottom-left, gray #aaaaaa, font 16
Win: front_door opened → "You escaped the manor." center text
