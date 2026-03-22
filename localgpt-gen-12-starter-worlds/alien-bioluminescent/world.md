# Alien Bioluminescent — World Specification

## World Parameters

| Parameter | Value |
|-----------|-------|
| World size | 35×35 |
| Terrain | Dark alien soil [0.08, 0.05, 0.12], roughness 0.9 |
| Time | Perpetual night (no sun) |
| Sky | [0.02, 0.01, 0.08, 1] deep purple-black |
| Player start | [0, 1, -20] first-person |

## Regions

### Mushroom Grove (south-center)
- 5 giant mushroom trees: thick cylinder stems (height 3-6) + torus caps
- Cap emissive: teal [0, 0.8, 0.7], blue [0.1, 0.2, 1], violet [0.6, 0.1, 0.9]
- Each cap pulses (0.3-0.5 freq) + point light underneath (matching color, 400-600 intensity, range 6)
- 8 glowing tendrils (thin cylinders, emissive green, bob on X axis)

### Crystal Field (east)
- 4 crystal clusters: elongated cuboids at angles, emissive pink [1, 0, 0.6] and amber [1, 0.6, 0]
- Each cluster = 3-4 cuboids + point light (matching color, 300 intensity)
- 4 PUZZLE CRYSTALS: clickable, play tone on click, must click in correct order

### Nexus Pool (center)
- Glowing liquid: flat cylinder (radius 4, emissive [0, 0.15, 0.1, 0.3], alpha "blend")
- 6 orbiting particles: tiny emissive spheres, orbit behavior (radius 4.5, speed 10, varied phases)
- Water emitter (turbulence 0.7, radius 8, volume 0.3)

### Canopy Layer (above)
- 4 jellyfish creatures: capsule bodies (emissive pink, alpha "blend") + 4 thin cylinder tentacles (children)
- Each jellyfish on unique path_follow (figure-8 or oval, heights 3-8, speed 0.4-0.8)
- Tentacles bob (amplitude 0.1, freq 0.5)

### Strange Moon (sky)
- Large sphere at [−15, 25, −10], scale [4,4,4], emissive [0.3, 0.15, 0.35, 0.3]
- Ring: torus around moon, same color, slow spin (axis [0,0,1], speed 5 deg/s)

## Crystal Puzzle System

4 puzzles, each unlocking a path segment toward the Nexus Pool:

| Puzzle | Crystals | Correct Order | Unlocks |
|--------|----------|---------------|---------|
| 1 | A, B (2 crystals) | A → B | Path to Crystal Field |
| 2 | C, D, E (3 crystals) | D → C → E | Path to Mushroom Grove |
| 3 | F, G, H (3 crystals) | H → F → G | Path to Nexus Pool |
| 4 | I, J, K, L (4 crystals) | J → L → I → K | Inner Nexus ring |

Each click: play unique tone + crystal changes emissive state.
Correct sequence: all crystals in group pulse simultaneously + path_follow guide orb appears.
Wrong order: all crystals reset (go dim briefly).

Implementation: `gen_add_trigger(click → toggle_state)` + `gen_link_entities` to chain states.

## NPC: Alien Guide "Fragment"

Capsule shape, translucent, emissive soft white [0.7, 0.7, 1, 0.4]. Path_follow in slow circle above Nexus Pool.
- "...light...follow...center..."
- "...crystals...sing...the order...matters..."
- "...you hear...the resonance...you understand..."
- Completion: "...the pool...opens...welcome...home..."

## Audio

- Cave ambience (drip_rate 0.4, resonance 0.5, volume 0.2)
- Alien drone: sine, 200Hz bandpass, radius 25, volume 0.12
- Crystal resonance: saw, 800Hz bandpass, radius 10, volume 0.06
- Wind: speed 0.05, gustiness 0.1, volume 0.1 (barely perceptible)
