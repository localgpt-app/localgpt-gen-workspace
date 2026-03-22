# Forest Edge Region

The northern boundary of the village, where civilization gives way to wild woodland. Dense trees frame the village, making it feel sheltered. The old oak — the largest tree in the world — is both a quest location (medallion #4 hidden in its hollow) and a visual landmark visible from the market square.

## Layout

```
    ┌──────────────────────────────────┐
    │  birch  birch    birch   birch   │  (tree line - dense)
    │     oak cluster     birch        │
    │  birch     OLD OAK ★   oak      │  ★ = medallion location
    │        mushroom ring             │
    │  oak    ·  ·  ·  ·    birch     │  · = mushroom ring stones
    │     birch       oak              │
    │                                  │
    │ ──── path from village ────      │
    │                                  │
    │     WELCOME SIGN                 │
    └──────────────────────────────────┘
          ↓ to Village Center
```

## Trees

Two species, scattered **organically** (never in a grid or row):

### Tall Oaks (5 trees)
- Trunk: Cylinder (radius 0.4, height random 5–8), color [0.3, 0.18, 0.08, 1], roughness 0.9
- Canopy: 2–3 spheres per tree (scale [2.5, 2, 2.5] to [3, 2.5, 3]), various greens:
  - [0.15, 0.5, 0.1, 1], [0.12, 0.45, 0.08, 1], [0.18, 0.55, 0.12, 1]
- Canopy bob: amplitude 0.03–0.05, frequency 0.2–0.35, varied phases (stagger so trees don't sway in unison)
- Trunk collider: capsule (static)

Suggested positions (approximate — offset Y to match terrain height):
- [3, 0, 22], [10, 0, 25], [-5, 0, 20], [12, 0, 30], [-8, 0, 28]

### Slender Birches (7 trees)
- Trunk: Cylinder (radius 0.12, height random 4–6), color [0.75, 0.7, 0.6, 1] (pale bark)
- Canopy: 1 icosahedron per tree (scale [1.2, 1.5, 1.2]), bright green [0.3, 0.65, 0.15, 1]
- Canopy bob: amplitude 0.04–0.06, frequency 0.3–0.45
- Trunk collider: capsule (static)

Suggested positions:
- [0, 0, 18], [6, 0, 20], [-3, 0, 24], [14, 0, 22], [-10, 0, 26], [8, 0, 32], [2, 0, 30]

### The Old Oak (landmark)
- Position: [8, 0, 28]
- Trunk: Cylinder (radius 0.8, height 7), color [0.25, 0.15, 0.06, 1] (ancient dark bark)
- Canopy: 4 spheres (scale [3, 2.5, 3], [3.5, 2, 3.5], [2.5, 2, 3], [3, 1.5, 2.5]), deep green [0.1, 0.4, 0.08, 1]
- Hollow: A small dark sphere (scale [0.4, 0.5, 0.3], color [0.05, 0.04, 0.03, 1]) embedded in the trunk at Y=1.5 to suggest a cavity
- Trunk collider: capsule (static), larger radius than normal oaks
- **Medallion #4** inside the hollow: position [8, 1.5, 28.2]
  - The emissive glow [0.9, 0.7, 0.1, 1] is faintly visible from outside the hollow — rewarding players who look carefully

## Mushroom Ring
A circle of 8 small toadstool shapes (cone + cylinder stem), radius 2.5 from center point [5, 0, 24].

| Mushroom | Angle | Position (calculated) | Cap Color |
|----------|-------|----------------------|-----------|
| mushroom_1 | 0° | [7.5, 0, 24] | [0.8, 0.2, 0.15, 1] (red) |
| mushroom_2 | 45° | [6.77, 0, 25.77] | [0.9, 0.85, 0.6, 1] (cream) |
| mushroom_3 | 90° | [5, 0, 26.5] | [0.8, 0.2, 0.15, 1] |
| mushroom_4 | 135° | [3.23, 0, 25.77] | [0.6, 0.5, 0.2, 1] (brown) |
| mushroom_5 | 180° | [2.5, 0, 24] | [0.9, 0.85, 0.6, 1] |
| mushroom_6 | 225° | [3.23, 0, 22.23] | [0.8, 0.2, 0.15, 1] |
| mushroom_7 | 270° | [5, 0, 21.5] | [0.6, 0.5, 0.2, 1] |
| mushroom_8 | 315° | [6.77, 0, 22.23] | [0.9, 0.85, 0.6, 1] |

Each mushroom:
- Stem: Cylinder (radius 0.04, height 0.12), cream [0.85, 0.8, 0.7, 1]
- Cap: Cone (radius 0.1, height 0.08), color per table above
- Scale: [0.3, 0.25, 0.3]
- No collider needed (too small to block player)
- Proximity trigger on the ring center:
  `gen_add_trigger(entity "mushroom_ring_center", trigger_type "proximity", trigger_params {radius: 3}, action "show_text", action_params {text: "The fairy ring hums with old magic. The villagers say wishes made here come true at midsummer.", duration: 5})`

## Entry Path & Signpost

### Welcome Sign
- Position: [0, 2.5, -35] (at the very start of the approach path)
- `gen_add_sign(text "Welcome to Aldric's Hollow", font_size 28, color "#f5e6c8", billboard false)`
- Mounted on 2 wooden posts (thin cylinders, brown)
- **This is the first thing the player sees.** It establishes the world's name and tone.

### Medallion #5 (Village Gate)
- Position: [2, 0.5, -33] (hidden behind the right gate post — player must look behind them after walking past)
- Shape: Torus, emissive gold
- Behaviors: spin + bob
- Collectible: value 1, category "medallions"
- **Design note:** This is the sneakiest placement. Most players will walk right past it. The Elder's hint ("search everywhere, even where you began") points back here.
