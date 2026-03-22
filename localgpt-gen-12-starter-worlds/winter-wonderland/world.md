# Winter Wonderland — World Specification

## World Parameters

| Parameter | Value |
|-----------|-------|
| World size | 30×30 |
| Terrain | White-blue snow [0.9, 0.92, 0.95], roughness 0.95 |
| Time | Overcast winter day |
| Player start | [0, 1, -10] near cabin |

## Layout

```
┌───────────────────────┐
│    Pine cluster N     │
│                       │
│  Bridge   FROZEN      │
│  (wood)   LAKE        │
│           (ice disc)  │
│                       │
│  CABIN    Snowman     │
│  (warm)   pedestal    │
│           Pine S      │
└───────────────────────┘
```

## Key Elements

### Frozen Lake (center)
- Flat cylinder: radius 5, height 0.05
- Color: [0.6, 0.75, 0.85, 0.7], alpha "blend", metallic 0.5, roughness 0.02, reflectance 0.9
- Collider: cylinder (walkable)

### Pine Trees (12)
- 3 stacked cones per tree (decreasing size up), dark green [0.08, 0.25, 0.08]
- Snow caps: slightly larger white cones as children over top cone
- Short brown cylinder trunks
- 2-3 trees with subtle bob (snow-laden)

### Cabin
- Body: cuboid 4×2.5×3, warm brown [0.35, 0.2, 0.1]
- Roof: white [0.9, 0.92, 0.95] (snow-covered), slight overhang
- 2 window planes: emissive amber [1, 0.7, 0.3, 0.6]
- Chimney: dark cylinder with 2 smoke puff spheres (path_follow up, loop)
- Point light from windows: warm orange, intensity 400, range 5
- Fire emitter inside: intensity 0.7, crackle 0.5, radius 3, volume 0.2

### Snowman Pedestal
- Position: [4, 0, -3]
- 3 pre-placed white spheres (body stack) that are incomplete
- When all 5 parts collected → approach → trigger celebration (all nearby lights pulse + chime)

### Falling Snow
- 20 tiny white spheres (scale 0.03), emissive white, unlit
- Each on path_follow: diagonal descent with sideways drift
- Speed: 0.2–0.5, mode "loop", varied start positions for coverage

## 5 Snowman Parts

| Part | Shape | Location | Color |
|------|-------|----------|-------|
| Top hat | Cuboid + cylinder | On cabin porch railing | Black |
| Carrot nose | Cone (tiny) | Behind tree trunk | Orange |
| Scarf | Flat plane (thin) | On bridge railing | Red |
| Coal eyes | 2 tiny spheres (paired) | Near frozen lake edge | Black |
| Stick arms | 2 thin cylinders | Under snow mound | Brown |

## NPC: Child "Lily"

Position: near snowman pedestal, wander behavior (small radius).
- "We were building a snowman but all the parts blew away in the storm! Can you find them?"
- Hints: "I think the hat landed on the porch..." / "The carrot went rolling toward the big tree..."

## Environment

```
background: [0.7, 0.75, 0.82, 1]      # overcast winter
ambient: 0.2, color [0.8, 0.85, 1]     # cool blue tint
sun: pale [0.85, 0.9, 1], intensity 2.5, direction [-0.3, -1, -0.4], shadows on
```

## Audio

- Wind: speed 0.4, gustiness 0.5, volume 0.3
- Silence otherwise. The muffled quiet of snow.
