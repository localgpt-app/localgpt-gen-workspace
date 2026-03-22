# Village Life Behaviors

Reusable behavior patterns for the medieval village. Behaviors attach to entities as ECS components. They reference entities by name, not Bevy Entity ID.

## Wind Sway (trees and crops)

All tree canopies and tall vegetation use the `bob` behavior to simulate wind. Key rules:
- **Stagger phases** — if all trees sway in sync it looks mechanical. Vary frequency by ±0.1 and add phase offsets.
- **Scale amplitude to size** — large oaks: amplitude 0.03. Thin birches: amplitude 0.06. Wheat stalks: amplitude 0.02.
- **Always on X axis** — bob on Y looks like bouncing, not wind.

```
# Oak canopy (subtle sway)
{ type: "bob", amplitude: 0.035, frequency: 0.25, axis: [1, 0, 0] }

# Birch canopy (more responsive)
{ type: "bob", amplitude: 0.055, frequency: 0.38, axis: [1, 0, 0] }

# Well bucket (gentle creak)
{ type: "bob", amplitude: 0.03, frequency: 0.2, axis: [0, 1, 0] }
```

## Medallion Beacon

All 5 quest medallions share the same dual-behavior pattern to make them visually distinct from environment objects:

```
# Spin — draws the eye
{ type: "spin", axis: [0, 1, 0], speed: 45 }

# Bob — hover effect
{ type: "bob", amplitude: 0.1, frequency: 0.5, axis: [0, 1, 0] }
```

Combined with emissive gold [0.9, 0.7, 0.1, 1], this makes medallions read as "interactive pickup" even without UI prompts.

## Smoke Puffs (forge chimney, cabin chimney)

Smoke is simulated with 2–3 tiny semi-transparent spheres using path_follow on a vertical loop:

```
# Each smoke puff
shape: Sphere
scale: [0.2, 0.2, 0.2]
color: [0.5, 0.5, 0.55, 0.12]
alpha_mode: "blend"
behavior: { type: "path_follow", waypoints: [[x, y_start, z], [x+0.3, y_start+3, z-0.2]], speed: 0.3, mode: "loop" }
```

Stagger 2–3 puffs at different path offsets for continuous smoke effect.

## Waterwheel Rotation

The miller's waterwheel uses spin on the torus body:

```
{ type: "spin", axis: [1, 0, 0], speed: 15 }
```

The axis is [1,0,0] (X-axis) because the wheel rotates around its horizontal axle, which runs east-west perpendicular to the river.

## NPC Wander (Merchant Brynn)

Merchant Brynn uses the "wander" behavior with implicit bounds around the market square. If wander isn't available, fall back to path_follow with a closed loop through the stall positions:

```
# Fallback patrol path
{ type: "path_follow", waypoints: [[3,0,3], [7,0,3], [7,0,7], [3,0,7]], speed: 1.5, mode: "loop" }
```

## Door Open/Close Animation

Doors use `gen_add_door` which internally composes:
1. A rotation tween on the door entity (Y-axis, 0° → open_angle over open_duration)
2. A proximity or click trigger to initiate
3. An optional auto_close timer that reverses the tween
4. Optional audio (sound_open, sound_close)

**Behavior anchor gotcha:** If a door entity is repositioned after the door behavior is attached, the animation anchor drifts. Always position the door entity FIRST, then call `gen_add_door`.

| Door | Trigger | Open Angle | Duration | Auto Close | Sound |
|------|---------|-----------|----------|------------|-------|
| cottage_1_door | proximity | 90° | 1.0s | yes (3s) | wood_creak |
| cottage_2_door | click | 85° | 1.5s | yes (4s) | — |
| cottage_3_door | proximity | 90° | 1.0s | yes (3s) | — |
| forge_door | proximity | 110° | 0.8s | no | — |
| church_door | click | 95° | 2.0s | yes (5s) | heavy_door |

## Lily Pad Drift

Pond lily pads use a very slow, subtle bob to simulate floating:

```
{ type: "bob", amplitude: 0.01, frequency: 0.15, axis: [0, 1, 0] }
```

This is deliberately almost imperceptible — just enough to register as "alive water surface."
