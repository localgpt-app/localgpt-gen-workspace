# Backrooms — World Specification

## World Parameters

| Parameter | Value |
|-----------|-------|
| World size | 40×40 interior (no exterior) |
| Terrain | None (floor plane) |
| Ceiling height | 3 units |
| Palette | Dirty yellow-beige ONLY |
| Player start | [0, 1.6, 0] first-person |

## Floor Plan (maze)

```
┌─────────┬───────────┬─────────┐
│ Room A  │ Corridor  │ Room B  │
│ (start) │  North    │ (fake   │
│ 10×10   │ 3×15      │  exit 1)│
├────┐    ├───────────┤    ┌────┤
│    │    │           │    │    │
│ C  │    │  Room D   │    │ E  │
│ o  │    │  (chair   │    │ x  │
│ r  │    │   room)   │    │ i  │
│ r  │    │  5×5      │    │ t  │
│ W  │    │           │    │ 2  │
├────┘    ├───────────┤    └────┤
│ Dead    │ Corridor  │ REAL    │
│ End     │  South    │ EXIT    │
│ (red    │ 3×10      │ (door)  │
│  sphere)│           │         │
└─────────┴───────────┴─────────┘
                        Exit 3 (fake, below)
```

## Construction

- Floor: plane 40×40, dirty carpet [0.45, 0.4, 0.25], roughness 1.0
- Ceiling: plane at Y=3, [0.6, 0.58, 0.45], roughness 0.9
- Walls: 15-20 cuboid segments (0.15 thick, 3 tall, varied width), beige [0.55, 0.5, 0.35]
- ALL walls need box colliders
- Doorway gaps: 1.3 units wide (just barely comfortable)

## Fluorescent Lights (12)

- Long thin cuboid "fixtures" on ceiling, emissive [1, 0.95, 0.7, 0.8]
- Point light below each (intensity 300, range 4, warm yellow)
- 3 lights: fast flicker (pulse freq 2.5, scale 0.7–1.0)
- 1 light: dying bulb (pulse freq 0.15, very slow)
- 8 lights: stable

## The Wrong Objects

- Red sphere in dead end corridor: [0.8, 0.05, 0.05], scale 0.15. No explanation. No interaction.
- Chair facing blank wall in Room D: cuboid construction. No purpose.
- Puddle on floor: flat cylinder (radius 0.5, Y=0.005, transparent). No water source.
- Exit sign: emissive green plane on wall, pointing at dead end.

## Fake Exits → Loop Teleporters

| Fake Exit | Position | Teleports To |
|-----------|----------|-------------|
| Exit 1 (Room B) | [15, 0, 12] | [0, 1.6, 0] (back to start) |
| Exit 2 (east) | [18, 0, -5] | [0, 1.6, 0] |
| Exit 3 (south) | [10, 0, -18] | [0, 1.6, 0] |

Real exit: [18, 0, -15], door trigger (click to open). Opens to white void → "You escaped." center text.

## Audio: Emptiness

- Electrical hum: sine, 120Hz cutoff, lowpass, radius 30, volume 0.15
- Undertone: square wave, 60Hz cutoff, lowpass, radius 30, volume 0.05
- Cave drip: drip_rate 0.2, resonance 0.7, volume 0.08 (distant, wrong)
- **NO wind. NO nature. NO music.**
