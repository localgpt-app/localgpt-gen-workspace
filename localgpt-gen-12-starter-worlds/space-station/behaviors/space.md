# Space Behaviors

Everything in space moves — slowly, perpetually, silently. Behaviors here convey the scale and emptiness of orbital mechanics.

## Habitat Ring Rotation
```
entity: ring_1
{ type: "spin", axis: [0, 0, 1], speed: 3 }
```
Only one ring rotates — the others are structural. 3 deg/s = one full rotation every 2 minutes. Cinematic, not fast.

## Shuttle Approach
```
entity: shuttle
{ type: "path_follow",
  waypoints: [[0,0,-25], [0,-0.5,-18], [0,-0.2,-12], [0,0,-9]],
  speed: 0.3, mode: "once" }
```
The shuttle takes ~50 seconds to approach. The slow speed conveys mass and precision. The slight Y dips simulate course corrections.

## Asteroid Tumble
Each asteroid uses spin with a unique axis:
```
asteroid_1: { type: "spin", axis: [0.7, 0.3, 0.5], speed: 8 }
asteroid_2: { type: "spin", axis: [0.2, 0.9, 0.1], speed: 5 }
asteroid_3: { type: "spin", axis: [0.5, 0.1, 0.8], speed: 10 }
```
Non-axis-aligned spin creates natural tumbling. Different speeds prevent synchronization.

## Solar Panel Tracking
```
{ type: "spin", axis: [0, 1, 0], speed: 1 }
```

## Docking Guide Lights
```
{ type: "pulse", min_scale: 0.5, max_scale: 1.0, frequency: 0.8 }
```
Sharp on/off pulse (0.5 min) simulates sequential docking guide beacons.

## Reactor Core Tremor
```
{ type: "bob", amplitude: 0.01, frequency: 2.0, axis: [0, 1, 0] }
```
High frequency (2 Hz), tiny amplitude — engine vibration that the player barely notices but subconsciously registers as "machine power."

## Warning Indicator Pulse (Life Support)
```
{ type: "pulse", min_scale: 0.0, max_scale: 1.0, frequency: 1.5 }
```
Red sphere blinking: system failure indicator. Sharp 0→1 creates alarm-like visual.

## Repair Part Beacons
All 4 repair parts:
```
spin: { axis: [0,1,0], speed: 45 }
bob: { amplitude: 0.08, frequency: 0.6 }
```
Consistent with other template collectibles but slightly slower bob (space = floating, not bouncing).
