# Modules Region

Four specialized rooms at the end of each arm. Each module is a cuboid room (3×3×3) with a floor platform, internal lighting, themed equipment, and one hidden repair part.

## Shared Module Construction

Each module:
- Room shell: Cuboid (3, 3, 3), metallic gray, collider (static)
- Floor: Cuboid (2.8, 0.1, 2.8), slightly lighter, collider (static)
- Return telepad: centered on floor, sends player back to hub
- Interior point light: color varies by module, intensity 400, range 4
- Arm connector: long thin cuboid (0.8×0.8×8) from hub to module, metallic, collider

## Life Support Module (West, [-15, 0, 0])

- **Theme:** Organic, green-tinted. The "garden" of the station.
- Interior light: green [0.3, 0.8, 0.4, 1]
- Equipment:
  - 3 cylinder "air tanks" (radius 0.2, height 1.5, green-tinted metal)
  - Flat plane "control panel" on wall, emissive green
  - Small sphere "warning indicator" pulsing red (the system is broken)
- **Air Filter (repair part):**
  - Position: behind the largest air tank (partially occluded)
  - Shape: Cuboid (0.15, 0.15, 0.08)
  - Emissive: [0.2, 0.8, 0.3, 1] (green)
  - Behaviors: spin (Y, 45), bob (0.08, 0.6)
  - `gen_add_collectible(entity "air_filter", value 1, category "parts")`

## Comms Module (East, [15, 0, 0])

- **Theme:** Blue, electronic. Arrays of antenna-like cylinders.
- Interior light: cyan [0.3, 0.6, 1, 1]
- Equipment:
  - 4 thin cylinder "antenna arrays" of varying heights
  - Flat plane "display screen" with emissive cyan text pattern
  - Small torus "dish" mounted on wall
- **Antenna Relay (repair part):**
  - Position: inside the dish torus (player must look inside it)
  - Shape: Cuboid (0.12, 0.12, 0.06)
  - Emissive: [0, 0.7, 1, 1] (cyan)
  - `gen_add_collectible(entity "antenna_relay", ...)`

## Engine Module (South, [0, 0, -15])

- **Theme:** Orange, industrial. Heat and power.
- Interior light: orange [1, 0.6, 0.2, 1]
- Equipment:
  - Large cylinder "reactor core" (radius 0.5, height 1.5, emissive orange [0.5, 0.2, 0, 0.3])
  - 4 pipe cylinders (thin, connecting core to walls)
  - Vibration: reactor core has bob behavior (amplitude 0.01, frequency 2.0) — high frequency tremor
- **Fuel Cell (repair part):**
  - Position: underneath the reactor (player must look down)
  - Shape: Cuboid (0.15, 0.1, 0.15)
  - Emissive: [1, 0.5, 0, 1] (orange)
  - `gen_add_collectible(entity "fuel_cell", ...)`

## Navigation Module (North, [0, 0, 15])

- **Theme:** Cool white-blue, clean, data-focused.
- Interior light: white-blue [0.8, 0.85, 1, 1]
- Equipment:
  - Flat plane "star map display" (1.5×1, emissive blue with white dots simulating star chart)
  - Cuboid "console desk" with small sphere "hologram" bobbing above it
  - 2 cylinder "data towers"
- **Nav Chip (repair part):**
  - Position: on the console desk (most obvious placement — this is the easiest module)
  - Shape: Cuboid (0.1, 0.1, 0.04)
  - Emissive: [0.8, 0.8, 1, 1] (white-blue)
  - `gen_add_collectible(entity "nav_chip", ...)`

## Solar Panels (2)

Flat planes extending from the North and South arms:
- Size: 6×0.05×2 each
- Color: [0.05, 0.05, 0.3, 1] (dark blue), emissive [0, 0, 0.15, 1] (faint blue glow)
- Angled 30° from arm axis
- Slow spin behavior: axis [0,1,0], speed 1 deg/s (tracking the "sun")
