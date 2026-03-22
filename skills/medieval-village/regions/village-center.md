# Village Center Region

The social and commercial heart of Aldric's Hollow. The market square is the first major landmark players see after walking up the path from the gate. The church tower is visible from everywhere in the world as a navigation beacon.

## Layout

The market square is a raised stone platform (6×0.15×6) at [5, 0.1, 5]. Three cottages form an L-shape around the north and east edges. The church tower anchors the northwest corner. The well sits slightly off-center in the square, drawing the eye.

```
        Church Tower
            │
    ┌───────┼───────────┐
    │       │   Cottage 3│
    │  Well ·            │
    │       Market       │
    │       Square       │
    │  Cottage 1  Cot. 2 │
    └────────────────────┘
         ↓ path to gate
```

## Entities

### Market Square Platform
- Shape: Cuboid
- Position: [5, 0.1, 5]
- Dimensions: {x: 8, y: 0.15, z: 8}
- Color: [0.5, 0.5, 0.5, 1.0] (weathered stone gray)
- Roughness: 0.85
- Collider: box (static)

### Market Stalls (4)
Each stall: 2 thin cylinder posts (radius 0.08, height 2.5, brown [0.4, 0.25, 0.1]) supporting a flat plane canopy.

| Stall | Position | Canopy Color | Content hint |
|-------|----------|-------------|-------------|
| stall_fruit | [3, 0, 3] | [0.7, 0.1, 0.1, 1] (red) | Apples and pears |
| stall_cloth | [7, 0, 3] | [0.1, 0.2, 0.6, 1] (blue) | Fabric bolts |
| stall_bread | [3, 0, 7] | [0.6, 0.5, 0.2, 1] (tan) | Bread loaves |
| stall_herbs | [7, 0, 7] | [0.15, 0.4, 0.15, 1] (green) | Hanging herbs |

### The Well
- Position: [4.5, 0, 5.5]
- Base: Cylinder (radius 0.6, height 0.8, stone gray [0.45, 0.45, 0.45, 1])
- Posts: 2 thin cylinders (radius 0.06, height 1.8, brown) rising from base edges
- Crossbar: thin cuboid connecting post tops
- Bucket: tiny cylinder hanging from crossbar center, bob behavior (amplitude 0.03, frequency 0.2)
- Rope: (simulated by thin cylinder from crossbar to bucket, parented to bucket)
- Collider: cylinder on base (static)

### Cottage 1 — "The Baker's House"
- Position: [2, 0, 1]
- Body: Cuboid (3, 2.5, 3), color [0.55, 0.35, 0.2, 1] (warm timber)
- Roof: Pyramid on top (base 3.5×3.5, height 1.5), color [0.35, 0.15, 0.1, 1] (dark thatch), parent: cottage_1_body
- Door: thin plane on south face, color [0.3, 0.18, 0.08, 1]
  - `gen_add_door(entity "cottage_1_door", trigger "proximity", open_angle 90, open_duration 1.0, auto_close true, auto_close_delay 3.0, sound_open "wood_creak")`
- Window: 2 small planes on east face, color [0.6, 0.75, 0.85, 0.5], alpha_mode "blend"
- Collider: box on body (static)
- **Medallion #1** hidden inside on the floor: position [2, 0.3, 1.5]

### Cottage 2 — "The Weaver's Workshop"
- Position: [8, 0, 1]
- Body: Cuboid (2.5, 2.2, 3.5), color [0.65, 0.45, 0.25, 1] (lighter timber)
- Roof: Pyramid (base 3×4, height 1.3), dark brown, parent: cottage_2_body
- Door: `gen_add_door(trigger "click", open_angle 85)`
- Collider: box (static)

### Cottage 3 — "The Healer's Abode"
- Position: [9, 0, 8]
- Body: Cuboid (3, 3, 2.5), color [0.5, 0.4, 0.3, 1] (aged timber)
- Roof: Pyramid, dark red-brown
- Door: `gen_add_door(trigger "proximity")`
- Small herb garden in front: 4 green spheres (scale [0.1, 0.08, 0.1]) at ground level
- Collider: box (static)

### Church Tower
- Position: [-2, 0, 10]
- Body: Cuboid (2.5, 5, 2.5), color [0.5, 0.48, 0.45, 1] (stone)
- Steeple: Cone on top (radius 1.5, height 2.5), color [0.15, 0.1, 0.08, 1]
- Bell: small torus inside steeple (emissive [0.7, 0.6, 0.3, 0.4])
- Interior light: point light (golden [1, 0.85, 0.5, 1], intensity 800, range 8)
- Collider: box (static)
- **Design note:** The tower should be visible from the player spawn point. It's the primary wayfinding landmark.

### Elder Aldric (NPC)
- Position: [5, 0, 5] (center of market square)
- Behavior: "idle"
- Model: "default_humanoid"
- Trigger: click, radius 3.0
- Dialogue: see `avatar/player.md` for full dialogue tree
- **Design note:** He faces south toward the approaching player path. His idle position is near the well — the natural focal point of the square.

### Merchant Brynn (NPC)
- Position: [3, 0, 4] (near fruit stall)
- Behavior: "wander" within market square bounds
- Patrol speed: 1.5 u/s
- Wander radius: ~5 units from center
- Dialogue: single node ("Fine wares! I've got potions, maps, and... well, mostly just potions today.")

### Medallion #2
- Position: [4.5, 1.2, 5.5] (hanging inside the well — look down!)
- Shape: Torus (scale [0.15, 0.15, 0.15])
- Emissive: [0.9, 0.7, 0.1, 1]
- Behaviors: spin (axis [0,1,0], speed 45), bob (amplitude 0.08, frequency 0.5)
- Collectible: value 1, category "medallions", pickup_effect "sparkle", pickup_sound "chime"

## Signs

| Name | Position | Text | Billboard |
|------|----------|------|-----------|
| sign_market | [5, 2.5, 1] | "Market Square" | true |
| sign_church | [-2, 2, 7] | "Chapel of the Dawn →" | true |
| sign_healer | [9, 2, 6] | "Healer — Salves & Tonics" | true |
