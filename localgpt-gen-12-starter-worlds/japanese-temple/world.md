# Japanese Temple — World Specification

## World Parameters

| Parameter | Value |
|-----------|-------|
| World size | 30×30 |
| Terrain | Muted green [0.2, 0.35, 0.12], roughness 1.0 |
| Time | Soft morning, misty |
| Player start | [0, 1, -15] outside torii gate |

## Layout

```
┌──────────────────────────┐
│         TEMPLE           │
│   (raised platform,      │
│    tiered roofs)         │
│   Inner door (locked     │
│   until 5 meditations)   │
├──────────────────────────┤
│  Zen    │   Koi Pond     │
│ Garden  │  (with bridge) │
│ (rocks) │  Cherry trees  │
├──────────────────────────┤
│      Meditation Path     │
│  Station 1 → 2 → 3 →    │
│  → 4 → 5 → Temple       │
├──────────────────────────┤
│      TORII GATE          │
│      (entry)             │
│      Player spawn        │
└──────────────────────────┘
```

## 5 Meditation Stations

Each station: stone cylinder pedestal + proximity trigger (radius 2m) → show haiku + play bell sound + light lantern.

| Station | Position | Haiku |
|---------|----------|-------|
| 1 | [0, 0, -8] | "Old pond / a frog jumps in / sound of water" |
| 2 | [-5, 0, -2] | "In the cicada's cry / no sign can foretell / how soon it must die" |
| 3 | [3, 0, 5] | "The temple bell stops / but I still hear the sound / coming out of the flowers" |
| 4 | [-3, 0, 10] | "Over the wintry forest / winds howl in rage / with no leaves to blow" |
| 5 | [0, 0, 14] | "A world of dew / and within every dewdrop / a world of struggle" |

## NPC: Monk

Position: inside temple, visible through open front.
- Before quest: "Walk the garden path. Five stones mark the way. Listen at each one."
- After 5 meditations: "You have heard the garden speak. The inner door is open. Enter, and find stillness."

## Environment

```
background: [0.65, 0.7, 0.75, 1]     # misty morning
ambient: 0.2, color [1, 0.95, 0.9]    # warm tint
sun: warm [1, 0.95, 0.85], intensity 2.5, direction [-0.5, -1, -0.3], shadows on
```

## Audio

- Stream (flow_rate 0.3, volume 0.3)
- Forest (bird_density 0.5, wind 0.15, volume 0.3)
- Wind (speed 0.1, gustiness 0.1, volume 0.15)
- Koi pond water emitter (turbulence 0.15, radius 6, volume 0.25)
