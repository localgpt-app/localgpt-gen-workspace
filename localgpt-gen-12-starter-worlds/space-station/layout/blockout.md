# Layout Blockout

The space station layout is a **3D cross** — unusual among the starter worlds because there's no ground plane. All navigation is hub-centric: the hub connects to 4 arms via teleporters.

## 3D Zone Map

```
                  Y (up)
                  │
                  │    Navigation [0,0,15]
                  │         │
   Life Support ──┼── HUB ──┼── Comms [15,0,0]
   [-15,0,0]      │  [0,0,0] │
                  │         │
                  │    Engine [0,0,-15]
                  │         │
                  │    Docking [-8..0, z]
```

## Zone Bounding Volumes

| Zone | Center | Size | Floor Y |
|------|--------|------|---------|
| hub | [0, 0, 0] | [8, 4, 8] | -1.4 |
| arm_west | [-9, 0, 0] | [10, 2, 2] | — |
| arm_east | [9, 0, 0] | [10, 2, 2] | — |
| arm_north | [0, 0, 9] | [2, 2, 10] | — |
| arm_south | [0, 0, -9] | [2, 2, 10] | — |
| mod_life | [-15, 0, 0] | [3, 3, 3] | -1.4 |
| mod_comms | [15, 0, 0] | [3, 3, 3] | -1.4 |
| mod_engine | [0, 0, -15] | [3, 3, 3] | -1.4 |
| mod_nav | [0, 0, 15] | [3, 3, 3] | -1.4 |
| docking | [0, 0, -8] | [4, 4, 4] | — |

## Sightlines

1. **Hub → Docking Bay:** From hub center, the docking bay frame and approaching shuttle should be visible through the south arm opening. This creates a sense of purpose and incoming help.

2. **Hub → Ring Rotation:** At least one ring section should always be visible from inside the hub, rotating slowly. This orients the player.

3. **Module → Repair Part:** Each module is 3×3 — small enough that the repair part's emissive glow should be detectable within seconds of arrival.

## Collision Notes

- Hub floor is the primary walking surface
- Module floors are secondary walking surfaces (teleport destinations)
- Arms do NOT need walkable floors — transport is via teleporter
- Hub cylinder walls do NOT need interior colliders (player spawns inside)
- Module walls DO need colliders (player walks around inside)
- Stars and asteroids: no colliders (decorative, far away)
