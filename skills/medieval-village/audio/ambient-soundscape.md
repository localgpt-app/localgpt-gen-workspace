# Ambient Soundscape

The village soundscape has three design goals: establish "lived-in warmth," provide spatial wayfinding (you can hear the river before you see it), and reward exploration (the forge sounds different inside vs. outside).

## Ambience Layers (global)

Two always-on ambient layers create the base atmosphere:

### Forest Layer
```
sound: "forest"
bird_density: 0.7
wind: 0.3
volume: 0.4
```
Primary atmosphere. Bird calls and distant rustling. Should feel like the edge of a forest, not deep wilderness.

### Wind Layer
```
sound: "wind"
speed: 0.2
gustiness: 0.25
volume: 0.2
```
Gentle, consistent. Supports the tree sway behaviors without dominating.

## Spatial Emitters

Spatial emitters create audio zones that the player moves through. Volume falls off with distance based on radius.

### River Water
- Attached to: river water plane (or positioned at river center)
- Sound: water (turbulence 0.4)
- Radius: 12 units
- Volume: 0.5
- **Design note:** This is the loudest emitter and the most important for spatial immersion. A player standing at the market square should hear it faintly. At the bridge, it should be prominent. Standing on the bridge, it should be the dominant sound.

### Pond Water
- Attached to: pond entity
- Sound: water (turbulence 0.2)
- Radius: 6 units
- Volume: 0.25
- **Design note:** Deliberately quieter than the river. A still pond, not a rushing stream.

### Forge Fire
- Position: inside blacksmith forge [-5, 1, 5]
- Sound: fire (intensity 0.8, crackle 0.6)
- Radius: 5 units
- Volume: 0.4
- **Design note:** Audible from outside the forge (radius 5 extends past the walls), but at reduced volume. Walking inside should feel noticeably warmer acoustically.

### Waterwheel Creak
- Attached to: waterwheel torus entity
- Sound: custom (waveform "brown_noise", filter_cutoff 300, filter_type "lowpass")
- Radius: 6 units
- Volume: 0.1
- **Design note:** Very subtle. A low wooden groaning that blends with the river water. Only noticeable when standing close to the miller's cottage.

### Church Bell (optional, if timer triggers are available)
- Position: church tower steeple [-2, 6, 10]
- Sound: custom (waveform "sine", filter_cutoff 800, filter_type "bandpass")
- Radius: 20 units (audible across entire village)
- Volume: 0.15
- Trigger: timer (interval 60 seconds), play for 2 seconds
- **Design note:** A distant bell toll every minute. Barely noticeable but deeply atmospheric. Creates a sense of time passing.

## Audio Zones Map

```
                Quiet forest ambience only
    ┌──────────────────────────────────────┐
    │                                      │
    │   ┌──river water (r=12)──┐           │
    │   │                      │           │
    │   │  ┌pond(r=6)┐        │  ┌────┐   │
    │   │  │         │ ┌forge  │  │bell│   │
    │   │  │         │ │(r=5)│ │  │r=20│   │
    │   │  └─────────┘ └─────┘ │  │    │   │
    │   │                      │  │    │   │
    │   └──────────────────────┘  └────┘   │
    │                                      │
    │          (wind + forest ambient)      │
    └──────────────────────────────────────┘
```

## Audio Mixing Rules

- Ambience layers are always on, regardless of player position
- Spatial emitters fade linearly from full volume at distance 0 to silence at radius
- Multiple emitters blend additively (river + forge when standing between them)
- No emitter should exceed volume 0.5 to prevent clipping when multiple overlap
- The total mix at the loudest point (bridge over river) should stay under 0.8 combined volume
