# Underwater Ocean — World Specification

## World Parameters

| Parameter | Value |
|-----------|-------|
| World size | 30×30 |
| Terrain | Sandy floor [0.55, 0.5, 0.35], roughness 1.0 |
| Water | Entire scene is underwater — blue-green background, blue ambient |
| Player start | [0, 3, 15] first-person, gravity 0.1 |

## Regions

### Coral Reef (center)
- 5 branching corals (stacked cylinders): orange, pink, red
- 4 brain corals (spheres): purple, green
- 3 fan corals (double-sided planes): pink, bob behavior
- 6 sea anemones (inverted cones): emissive tips, pulse
- 6 pollution items (dark cuboids) scattered among coral

### Open Sand (perimeter)
- 6 sand dune mounds (stretched spheres)
- 10 seaweed clusters (thin cylinders, bob on X axis)
- Treasure chest (cuboid, dark brown) with gold coin spheres nearby

### Fish Layer (mid-water)
- 5 small tropical fish: capsules on path_follow ovals (speed 1-2)
- 3 larger fish: silver capsules on slower paths (speed 0.5)
- 3 bubble columns: tiny spheres on vertical path_follow loops

## Pollution Cleanup Quest

6 dark cuboid "trash" items scattered in reef. Each is a collectible:
- On pickup: nearby coral section changes color (gray → vibrant)
- `gen_link_entities(source "trash_1", event "collected", target "coral_section_1", action "set_color:[1, 0.4, 0.1, 1]")`
- HUD updates: "Reef Health: 17%" → "33%" → etc.
- All 6 cleaned: "The reef is restored!" message + all coral pulses briefly

## NPC: Turtle Guide "Kai"

Capsule shape (green), path_follow in slow circle around reef.
- "The reef is sick. See those dark shapes? They don't belong here."
- "Each piece you remove heals the coral. Look closely — you'll see the change."
- Completion: "Beautiful. The reef lives again. Thank you, friend."

## Environment

```
background: [0.02, 0.08, 0.2, 1]     # deep ocean blue
ambient: 0.15, color [0.3, 0.7, 0.8]  # blue-green underwater
directional: blue-green [0.4, 0.7, 0.8], intensity 2, direction [0, -1, -0.2], shadows on
2 spot lights aimed down (caustic simulation): [0.5, 0.8, 0.7], intensity 800, slow bob
```

## Audio

- Ocean ambience (wave_size 0.7, volume 0.4)
- Water emitter at reef center (turbulence 0.6, radius 20, volume 0.3)
- Whale song: custom (sine, cutoff 300, lowpass, radius 30, volume 0.1)
