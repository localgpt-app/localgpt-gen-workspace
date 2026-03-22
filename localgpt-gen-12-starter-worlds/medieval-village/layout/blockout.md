# Layout Blockout

Spatial planning for the medieval village. This file defines zone placement, sightlines, and critical spatial relationships before any entities are built.

## Grid & Scale

- **World units:** 1 unit ≈ 1 meter
- **Player height:** 1.8 units (collision capsule)
- **Comfortable doorway:** 1.2 wide × 2.2 tall minimum
- **Comfortable path:** 2.5 units wide (2 players side-by-side)
- **Building footprints:** 2.5×2.5 (small cottage) to 6×8 (market square)
- **Tree spacing:** minimum 3 units between trunks for walkability

## Zone Bounding Volumes

```
Zone              Center         Size           Primary Entities
─────────────────────────────────────────────────────────────────
village_gate      [0, 0, -30]    [10, 5, 15]    spawn, sign, medallion_5
village_center    [5, 0, 5]      [20, 10, 20]   market, well, church, 3 cottages, 2 NPCs
river_crossing    [-8, 0, 8]     [16, 8, 20]    bridge, pond, forge, 2 cottages, 1 NPC
forest_edge       [0, 0, 25]     [40, 15, 20]   12 trees, old oak, mushroom ring
```

## Critical Sightlines

These sightlines must remain unobstructed:

1. **Spawn → Church Tower:** Player at [0, 1.6, -38] must see the church steeple at [-2, 7, 10]. No tree canopy or building should block this line. The tower is the primary "go toward that" wayfinding cue.

2. **Market Square → Old Oak:** From the market center [5, 1.6, 5], the old oak canopy at [8, 5, 28] should be visible above the tree line. This pulls the player northward toward medallion #4.

3. **Bridge → Forge Interior:** Standing on the bridge [-5, 1.6, 10], the forge's glowing fire pit at [-5, 0.3, 5] should be visible through the open south face. The orange light draws players toward the forge and Kira's dialogue hint.

4. **Path Continuity:** The dirt path should always be visible at least 10 units ahead of the player. No building should fully obscure the next path segment.

## Elevation Profile

```
Height (Y)
    8 ┤                                     church steeple (7.5)
    7 ┤                                     old oak canopy (7)
    6 ┤
    5 ┤
    4 ┤
    3 ┤                                     cottage roofs (3-4)
    2 ┤  sign (2.5)
    1 ┤  ██ player ██                       bridge deck (0.8)
  0.5 ┤  ───────── terrain avg ──────────── water level
    0 ┼──┬──┬──┬──┬──┬──┬──┬──┬──┬──┬──┬──
      -40 -30 -20 -10  0  10  20  30  40
                     Z axis (south → north)
```

## Spatial Density Guidelines

- **Village center:** DENSE. Buildings close together (2-3 unit gaps). Stalls fill the square. Feels bustling even with only 2 NPCs.
- **River crossing:** MEDIUM. Buildings spaced 5-8 units apart. Open riverbank areas. The bridge is a natural chokepoint.
- **Forest edge:** SPARSE becoming DENSE. Open meadow near village, thickening into forest. Tree density increases with Z (deeper into forest = more trees).
- **Village gate:** EMPTY to SPARSE. Open approach path. The emptiness after spawning makes the village ahead feel inviting.

## Collision Coverage Checklist

Every structure the player shouldn't walk through needs a collider:

| Entity | Collider Shape | Priority |
|--------|---------------|----------|
| All cottage bodies | box | P0 |
| Church tower | box | P0 |
| Forge body | box | P0 |
| Market stall posts | (skip — too thin to matter) | — |
| Well base | cylinder | P1 |
| Bridge walls | box | P1 |
| Bridge deck | box | P0 |
| All tree trunks | capsule | P1 |
| Gate posts | box | P1 |
| Fence sections | box | P2 |
| Mushrooms | (skip — decorative) | — |
| Signs | (skip — decorative) | — |

## Terrain Integration Notes

With `height_scale 8` and perlin noise:
- Average terrain height ≈ 4.0 (half of height_scale)
- All entity Y positions in region files assume **terrain-relative placement**
- The generation pipeline must query or estimate terrain height at each entity's XZ position and add it to the specified Y offset
- River channel depth is controlled by the noise seed (42) — verify the channel aligns with the intended river position at Z ≈ 8-12
- If terrain height query is not available (`query_terrain_height` doesn't exist yet), use manual Y offset: place entities at Y = 4.0 + their design Y offset
