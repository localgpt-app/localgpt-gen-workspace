# Central Hub Region

The heart of the station. A cylindrical chamber where all 4 arms converge. The rotating ring surrounds it. 4 teleporter pads on the floor connect to the arm modules.

## Hub Structure

### Central Cylinder
- Position: [0, 0, 0]
- Shape: Cylinder (radius 4, height 3)
- Color: [0.3, 0.3, 0.35, 1], metallic 0.7, roughness 0.3
- Collider: mesh or box approximation (static)

### Hub Floor
- Flat cylinder (radius 3.5, height 0.1) at Y=-1.4 inside the hub
- Color: [0.25, 0.25, 0.3, 1], metallic 0.5
- Collider: box (static) — player stands on this

### Ring Sections (4 torus)
| Ring | Major Radius | Minor Radius | Color | Rotation | Behavior |
|------|-------------|-------------|-------|----------|----------|
| ring_1 | 6 | 0.8 | [0.4, 0.4, 0.45, 1] | default | spin (axis [0,0,1], speed 3) |
| ring_2 | 6 | 0.6 | [0.35, 0.35, 0.4, 1] | 90° yaw | none |
| ring_3 | 6 | 0.7 | [0.38, 0.38, 0.42, 1] | 45° yaw | none |
| ring_4 | 6 | 0.5 | [0.42, 0.42, 0.46, 1] | 135° yaw | none |

All rings: metallic 0.8, roughness 0.2.

### Teleporter Pads (4)

| Pad | Position (hub floor) | Destination (module) | Color | Label |
|-----|---------------------|---------------------|-------|-------|
| tp_west | [-2, -1.3, 0] | [-15, 0, 0] | [0.2, 0.8, 0.3, 1] (green) | "LIFE SUPPORT" |
| tp_east | [2, -1.3, 0] | [15, 0, 0] | [0, 0.7, 1, 1] (cyan) | "COMMS" |
| tp_south | [0, -1.3, -2] | [0, 0, -15] | [1, 0.5, 0, 1] (orange) | "ENGINE" |
| tp_north | [0, -1.3, 2] | [0, 0, 15] | [0.8, 0.8, 1, 1] (blue-white) | "NAVIGATION" |

Each pad: Cylinder (radius 0.8, height 0.05), emissive matching color, pulse behavior, surrounding torus ring spinning. `gen_add_teleporter` with fade effect. Sign above with label.

### VERA (AI Companion NPC)
- Position: [0, -0.8, 0] (center of hub floor)
- Behavior: "idle"
- Model: "default_humanoid"
- **Design note:** VERA is a holographic projection — use alpha_mode "blend" with emissive cyan. She's the station's AI, not a physical being.

## Docking Bay

Open-frame structure extending south from the hub:
- 4 thin cylinders forming a rectangular gateway (2×3 opening)
- Position: [0, 0, -8]
- Corner guide lights: 4 small spheres, emissive green [0, 1, 0.3, 1], pulsing (frequency 0.8)
- Point light inside bay: blue-white [0.8, 0.9, 1, 1], intensity 600, range 8

### Approaching Shuttle
- Body: Cuboid (1.5, 0.8, 3), metallic [0.35, 0.35, 0.4, 1], metallic 0.7
- Wings: 2 wedge shapes, children of body
- Path_follow: approaching dock from [0, 0, -25] to [0, 0, -9] over ~30 seconds
  ```
  waypoints: [[0, 0, -25], [0, -0.5, -18], [0, -0.2, -12], [0, 0, -9]]
  speed: 0.3, mode: "once"
  ```

## Stars (20)

Tiny spheres scattered at distances 20–40 units from station center:
- Scale: [0.05, 0.05, 0.05]
- Unlit: true
- Emissive: [1, 1, 1, 1]
- Random positions in all directions (not just on one plane)

## Asteroids (3)

Tumbling icosahedrons at station edges:
- Positions: [20, 5, 15], [-18, -3, -20], [12, -8, 22]
- Color: [0.2, 0.2, 0.2, 1], roughness 0.9
- Scale: [1.5–2.5] randomly
- Spin behavior: random axes, 5–10 deg/s
