# Medieval Village — World Specification

## World Parameters

| Parameter | Value |
|-----------|-------|
| World size | 100 × 100 units |
| Terrain | Perlin noise, 4 octaves, height_scale 8, seed 42 |
| Water level | Y = 0.5 (river channel carved by terrain seed) |
| Time of day | Sunset (golden hour) |
| Mood | Warm, cozy, inviting |
| Player start | Village gate [0, 1, -38] facing north toward village |

## Region Map

```
                    N (+Z)
                     ↑
    ┌────────────────────────────────┐
    │         FOREST EDGE            │
    │   (trees, old oak, path entry) │
    │         z: 15 to 35            │
    ├────────────────────────────────┤
    │                                │
    │  RIVER CROSSING    │ VILLAGE   │
    │  (bridge, pond,    │ CENTER    │
    │   waterwheel,      │ (market,  │
    │   2 cottages)      │  church,  │
    │  x: -15 to 0      │  well,    │
    │  z: -5 to 15       │  3 cot.) │
    │                    │ x: 0..15 │
    │                    │ z: -5..15│
    ├────────────────────────────────┤
    │         VILLAGE GATE           │
    │     (entry path, signpost)     │
    │         z: -35 to -5           │
    └────────────────────────────────┘
                     ↓
                    S (-Z)
```

## Regions

### 1. Village Center (primary)
- **Bounds:** center [5, 0, 5], size [20, 10, 20]
- **Anchor:** Market square platform at [5, 0.1, 5]
- **Contains:** Market square, well, church/tower, 3 cottages, Elder Aldric NPC, Merchant Brynn NPC, 4 market stalls, 2 medallions
- **Spec:** `regions/village-center.md`

### 2. River Crossing (secondary)
- **Bounds:** center [-8, 0, 8], size [16, 8, 20]
- **Anchor:** Stone bridge at [-5, 0.8, 10]
- **Contains:** River (water plane), stone bridge, pond, waterwheel, 2 cottages, Forge Master Kira NPC, blacksmith forge, 1 medallion
- **Spec:** `regions/river-crossing.md`

### 3. Forest Edge (tertiary)
- **Bounds:** center [0, 0, 25], size [40, 15, 20]
- **Anchor:** Old oak tree at [8, 0, 28]
- **Contains:** 10+ trees, old oak with hollow, mushroom ring, path terminus, 1 medallion, entry signpost
- **Spec:** `regions/forest-edge.md`

### 4. Village Gate (entry zone)
- **Bounds:** center [0, 0, -30], size [10, 5, 15]
- **Anchor:** Welcome sign at [0, 2.5, -35]
- **Contains:** Gate posts, welcome sign, dirt path start, player spawn point, 1 medallion (hidden behind gate post)

## Generation Phases

### Phase 1: Terrain & Water
```
gen_add_terrain(size [100, 100], noise_type "perlin", octaves 4, height_scale 8, seed 42, material "grass")
gen_add_water(height 0.5, size [80, 15], color "#2a6e4f", opacity 0.65, wave_speed 0.5)
```
Terrain generates rolling hills. The river channel is carved by the noise seed — entities near the river need Y offset of ~0.5 to sit on the bank. Verify terrain height at key building locations before placing structures.

### Phase 2: Paths
```
gen_add_path(points [[0,0,-38], [0,0,-20], [3,0,-5], [5,0,5], [5,0,15], [-5,0.8,10]], width 2.5, material "dirt", curved true)
gen_add_path(points [[-8,0.8,8], [-2,0.8,10], [2,0.8,10], [8,0,8]], width 3, material "stone")  # bridge
```

### Phase 3: Village Center structures
Build market square platform, then cottages radiating outward, then church tower at the village edge. See `regions/village-center.md` for full entity list.

### Phase 4: River Crossing structures
Build bridge first (it anchors the crossing), then cottages and forge on the near bank. See `regions/river-crossing.md`.

### Phase 5: Forest Edge
Scatter trees organically (NOT in a grid). Place the old oak as a landmark visible from the market square. See `regions/forest-edge.md`.

### Phase 6: NPCs & Dialogue
Place Elder Aldric at market square center, Merchant Brynn wandering between stalls, Forge Master Kira at the anvil. Attach dialogue trees. See `avatar/player.md` for quest flow.

### Phase 7: Collectibles
Place 5 medallions in their hiding spots. Each gets spin + bob behavior and a collectible trigger. Wire to HUD counter. See medallion placement table in `avatar/player.md`.

### Phase 8: Audio & Lighting
Layer ambient soundscape, place spatial emitters, finalize sunset lighting. See `audio/ambient-soundscape.md`.

### Phase 9: Colliders & Polish
Add box colliders to every structure. Test walk-through. Adjust any floating or buried entities. Run `gen_scene_info` to verify entity count and positions.

## Environment Settings

```
background_color: [0.55, 0.4, 0.3, 1.0]    # sunset sky
ambient_light: 0.15
ambient_color: [1.0, 0.9, 0.8, 1.0]         # warm tint

sun:
  type: directional
  color: [1.0, 0.85, 0.6, 1.0]              # golden sunset
  intensity: 3.0
  direction: [-0.5, -1.0, -0.3]
  shadows: true
```

## Camera Defaults

```
initial_position: [15, 12, 18]    # overview shot for loading screen
look_at: [0, 1, 0]               # village center
fov: 60
```

After player spawns, camera switches to third-person follow (distance 6, height offset 2).
