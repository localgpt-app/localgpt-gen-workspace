# Modern City — World Specification

## World Parameters

| Parameter | Value |
|-----------|-------|
| World size | 35×35 flat |
| Terrain | Flat concrete [0.55, 0.55, 0.55], roughness 0.8 |
| Time | Bright daylight |
| Player start | [0, 1, -15] third-person |

## Layout

4 quadrants around central intersection. Roads cross in + pattern (width 5, dark asphalt). One quadrant is a park.

```
┌────────┬────────┐
│ Office │  Park  │
│ towers │(green) │
├────────┼────────┤
│Retail/ │ Glass  │
│ Apart. │ towers │
└────────┴────────┘
```

## Buildings (12 structures)

- 3 glass towers: heights 8-18, color [0.5, 0.6, 0.7, 0.8] alpha "blend", metallic 0.9, roughness 0.05
- 4 office blocks: heights 5-10, warm stone [0.65, 0.6, 0.55]
- 2 brick apartments: heights 4-6, red-brown [0.5, 0.25, 0.15]
- 2 retail: heights 2-3, cream with colored awning planes
- 1 curved tower: cylinder radius 3, height 12, glass material

All buildings get box colliders (static).

## Park

- Green plane (8×8), 5 trees, bench (cuboid), fountain (cylinder base + torus water ring + bobbing sphere)
- Fountain water emitter (turbulence 0.5, radius 6, volume 0.3)

## Bus Route

Kinematic cuboid (3×1.5×1.5, blue) on path_follow loop around the block perimeter. Speed 3 u/s. Player can stand on roof to ride.

## Delivery Quest

5 packages spawn at post office location. Player collects → runs to marked building → area_enter trigger confirms delivery. Timer starts on first pickup. All 5 delivered = success message.

## Environment

```
background: [0.5, 0.7, 0.9, 1]   # bright sky blue
ambient: 0.25, color [0.85, 0.9, 1]
sun: white [1, 1, 0.95], intensity 4, direction [-0.4, -1, -0.3], shadows on
```
