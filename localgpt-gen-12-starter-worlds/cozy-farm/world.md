# Cozy Farm — World Specification

## World Parameters

| Parameter | Value |
|-----------|-------|
| World size | 35×35 |
| Terrain | Warm green [0.3, 0.5, 0.15], roughness 1.0 |
| Time | Golden hour sunset |
| Player start | [0, 1, -12] third-person |

## Layout

```
┌───────────────────────────┐
│  Pond     Wheat    Flower │
│  + dock   field    patch  │
│                           │
│  Windmill  BARN   Veggie  │
│  (spins)  (delivery) garden│
│                           │
│     Sheep    FARMHOUSE    │
│    paddock   (spawn)      │
└───────────────────────────┘
```

## Windmill (signature element)

- Tower: Cylinder (radius 1, height 5, stone)
- Cone roof on top
- Blade assembly: small cylinder hub at tower top → 4 flat plane blades (4×0.3×0.1) parented to hub
- Hub spin: axis [0, 0, 1], speed 20 deg/s
- All 4 blades rotate as children — single spin drives the whole assembly

## Crop Mechanics

- Wheat: 40 thin cylinders (0.6 height, golden), bob on X (amplitude 0.03, freq 0.35)
- Click trigger on each → destroy + chime + increment score
- Respawn: gen_add_collectible(respawn_time: 30)
- Barn delivery zone: area_enter trigger at barn doors

## Animals

3 sheep in fenced paddock:
- Body: white sphere (0.5×0.4×0.6)
- Head: small sphere
- Legs: 4 tiny cylinders
- One sheep has gentle bob (amplitude 0.02, freq 0.3) — breathing

## Audio

- Forest (bird_density 0.7, wind 0.25, volume 0.35)
- Wind (speed 0.2, gustiness 0.3, volume 0.25)
- Stream (flow_rate 0.2, volume 0.15) — distant brook
- Fire emitter in farmhouse chimney (intensity 0.6, crackle 0.5, radius 4, volume 0.3)
- Pond water emitter (turbulence 0.2, radius 5, volume 0.2)
