# Player Avatar & Quest Design

## Player Configuration

```
gen_spawn_player:
  position: [0, -0.8, 0]            # hub floor
  camera_mode: "first_person"
  walk_speed: 4.0
  run_speed: 7.0
  jump_force: 12.0                    # high jump — low gravity
  gravity_scale: 0.15                 # floaty movement
  collision_radius: 0.3
  collision_height: 1.8

gen_set_spawn_point:
  position: [0, -0.8, 0]
  name: "hub_center"
  is_default: true
```

**Design rationale:** gravity_scale 0.15 makes movement feel weightless without losing control. Jump force 12 with low gravity means the player can leap across module rooms. Walk speed 4 (slightly slow) prevents "skating on ice" feel that plagues low-gravity implementations.

## Quest: "Station Repair"

### Objective
Find 4 repair parts in the station's modules and restore systems.

### HUD
```
gen_add_hud:
  element_type: "text"
  position: "top-right"
  label: "SYSTEMS"
  initial_value: "0 / 4 REPAIRED"
  font_size: 16
  color: "#88ccff"
```

### Quest Flow

```
Spawn in hub → VERA greets → explains station damage
    │
    ├─→ Telepad to Navigation (North) → Find NAV CHIP (easiest)
    ├─→ Telepad to Comms (East) → Find ANTENNA RELAY (moderate)
    ├─→ Telepad to Life Support (West) → Find AIR FILTER (moderate)
    └─→ Telepad to Engine (South) → Find FUEL CELL (hardest — look under reactor)
    │
    ▼
Return to hub with 4/4 → VERA: "All systems restored."
```

### VERA Dialogue

```yaml
npc: "VERA"
trigger: "proximity"
trigger_radius: 3
start_node: "greeting"
nodes:
  - id: "greeting"
    text: "Welcome back, Engineer. Station integrity is at 23%. Four critical systems are offline. I need you to retrieve repair components from each module."
    choices:
      - text: "Which systems?"
        next_node_id: "systems"
      - text: "How do I get to the modules?"
        next_node_id: "telepads"

  - id: "systems"
    text: "Life Support — west arm, green pad. Comms — east arm, cyan. Engine — south, orange. Navigation — north, blue-white. Each module contains the part needed to restore it."
    choices:
      - text: "How do I get there?"
        next_node_id: "telepads"

  - id: "telepads"
    text: "Step onto the color-coded pads on the hub floor. They'll transport you directly. I'll be here monitoring systems. Good luck, Engineer."

  - id: "complete"
    text: "All four systems restored. Station integrity at 98%. Well done, Engineer. The shuttle has docked — we're not alone out here anymore."
```

### Repair Part Collectibles

All 4 parts share:
```
gen_add_collectible(value 1, category "parts", pickup_effect "sparkle", pickup_sound "system_online")
gen_link_entities(source "PART_NAME", source_event "collected", target "hud_systems", target_action "increment")
```

### Completion Trigger

```
gen_add_trigger:
  entity: "hub_center_zone"
  trigger_type: "area_enter"
  condition: "parts_collected >= 4"
  action: "show_text"
  action_params: { text: "VERA: All systems restored. Station integrity 98%." }
  once: true
```

Chain: also change VERA's dialogue to "complete" node.

### Signs

| Sign | Position | Text | Color |
|------|----------|------|-------|
| hub_sign | [0, 1, 1.5] | "CENTRAL HUB — DECK 0" | #88ccff |
| tp_west_label | [-2, -0.5, 0] | "← LIFE SUPPORT" | #33cc55 |
| tp_east_label | [2, -0.5, 0] | "COMMS →" | #00aaff |
| tp_south_label | [0, -0.5, -2] | "↓ ENGINE" | #ff8800 |
| tp_north_label | [0, -0.5, 2] | "↑ NAVIGATION" | #aabbff |
