# Player Avatar & Quest Design

## Player Configuration

```
gen_spawn_player:
  position: [0, 1, -38]
  rotation: [0, 0, 0]          # facing north toward village
  camera_mode: "third_person"
  camera_distance: 6
  camera_height_offset: 2
  walk_speed: 5.0
  run_speed: 9.0
  jump_force: 7.0
  collision_radius: 0.3
  collision_height: 1.8

gen_set_spawn_point:
  position: [0, 1, -38]
  name: "village_gate"
  is_default: true
```

**Design rationale:** Third-person camera at distance 6 lets the player see the village architecture while still feeling grounded. Walk speed 5 means crossing the full village (~70 units gate-to-forest) takes ~14 seconds at walk — long enough to explore, short enough to never feel tedious. Jump force 7 allows hopping onto the market square platform (0.15 height) and the bridge deck (0.8 height) but NOT onto rooftops.

## Spawn Experience

1. Player spawns at [0, 1, -38] facing north
2. The welcome sign ("Welcome to Aldric's Hollow") is directly ahead at -35
3. The dirt path leads forward, curving right toward the market square
4. The church tower is visible above the tree line — the primary navigation landmark
5. Camera starts at [0, 10, -45] for a brief cinematic overview (2 seconds), then transitions to third-person follow

## Quest: "The Five Medallions"

### Objective
Find 5 ancient medallions hidden around the village and return to Elder Aldric.

### Medallion Locations

| # | Name | Location | Region | Difficulty | Hint Source |
|---|------|----------|--------|-----------|-------------|
| 1 | Medallion of Hearth | Inside Cottage 1, on floor | Village Center | Easy | Elder Aldric ("search the cottages") |
| 2 | Medallion of Depths | Inside the well, Y=1.2 | Village Center | Medium | Elder Aldric ("the well") |
| 3 | Medallion of Craft | Under the stone bridge | River Crossing | Medium | Forge Master Kira ("glinting under the bridge") |
| 4 | Medallion of Growth | Inside old oak hollow, Y=1.5 | Forest Edge | Hard | Elder Aldric ("the old tree by the river") |
| 5 | Medallion of Dawn | Behind right gate post | Village Gate | Sneaky | Elder Aldric ("search everywhere, even where you began") |

### Quest Flow

```
Player spawns
    │
    ▼
Walk toward village → see Welcome Sign
    │
    ▼
Arrive at market square → Elder Aldric visible at center
    │
    ▼
Interact with Elder Aldric → dialogue triggers
    │
    ├── "I'll help!" → Quest accepted, HUD appears "Medallions: 0/5"
    │
    └── "Tell me more" → Lore node → "I'll find them" → same result
    │
    ▼
Explore village, find medallions 1-5 in any order
    │  (each pickup: sparkle effect + chime sound + HUD increments)
    │
    ▼
Return to Elder Aldric with 5/5
    │
    ▼
Proximity trigger (condition: medallions >= 5) → "You found them all!" dialogue
    │
    ▼
Quest complete. (No mechanical reward yet — this is the template version.)
```

### HUD Elements

```
gen_add_hud:
  element_type: "text"
  position: "top-left"
  label: "Medallions"
  initial_value: "0 / 5"
  font_size: 20
  color: "#ffd700"     # gold to match medallion color
```

Each medallion pickup triggers:
```
gen_link_entities:
  source: "medallion_N"
  source_event: "collected"
  target: "hud_medallions"
  target_action: "increment"
```

### Quest Completion Trigger

```
gen_add_trigger:
  entity: "elder_aldric_quest_zone"
  trigger_type: "proximity"
  trigger_params: { radius: 3 }
  action: "show_text"
  action_params: { text: "Elder Aldric: You found them all! The village is saved!" }
  condition: "medallions_collected >= 5"
  once: true
```

## NPC Dialogue Trees

### Elder Aldric

```yaml
npc: "Elder Aldric"
trigger: "click"
trigger_radius: 3.0
start_node: "greeting"
nodes:
  - id: "greeting"
    text: "Welcome, traveler! Our village has lost five ancient medallions. Without them, the harvest will fail. Will you help us find them?"
    choices:
      - text: "I'll help!"
        next_node_id: "accept"
      - text: "Tell me more about the medallions."
        next_node_id: "lore"

  - id: "lore"
    text: "They were forged by the First Smith, who built this village three hundred years ago. Each one protects a different aspect of our life — hearth, water, craft, growth, and the dawn itself."
    choices:
      - text: "Where should I look?"
        next_node_id: "hints"
      - text: "I'll find them."
        next_node_id: "accept"

  - id: "hints"
    text: "Search the cottages, the well, near the old bridge, and the great oak at the forest edge. And search everywhere... even where you began your journey."
    choices:
      - text: "Got it. I'm on my way."
        next_node_id: "accept"

  - id: "accept"
    text: "Wonderful! The medallions glow with a faint golden light — you'll know them when you see them. Return to me when you have all five."

  - id: "complete"
    text: "By the stars, you found them all! The village is in your debt, traveler. May the medallions' light guide your path always."
```

### Merchant Brynn

```yaml
npc: "Merchant Brynn"
trigger: "click"
trigger_radius: 2.5
start_node: "shop"
nodes:
  - id: "shop"
    text: "Fine wares! I've got potions, maps, and... well, mostly just potions today. The real treasure's in the stories, not the stock."
    choices:
      - text: "Have you seen any medallions?"
        next_node_id: "medallion_hint"
      - text: "Nice stall."
        next_node_id: "thanks"

  - id: "medallion_hint"
    text: "Medallions? Old Aldric's been going on about those for weeks. I think I saw something shiny roll behind one of the gate posts when I arrived this morning. Probably nothing."

  - id: "thanks"
    text: "Thanks! Built it myself. Well... mostly myself. The carpenter helped. A lot."
```

### Forge Master Kira

```yaml
npc: "Forge Master Kira"
trigger: "click"
trigger_radius: 2.5
start_node: "greeting"
nodes:
  - id: "greeting"
    text: "The forge runs hot today. If you need a blade sharpened, come back tomorrow. I'm working on something... special."
    choices:
      - text: "Have you seen a medallion?"
        next_node_id: "hint"
      - text: "What are you working on?"
        next_node_id: "secret"

  - id: "hint"
    text: "Aye, I saw something glinting under the old bridge last week. Gold, maybe? I couldn't reach it from the bank — too steep. You'd have to wade."

  - id: "secret"
    text: "Ha! A smith never reveals her work before it's done. Let's just say it involves moonstone and a very old blueprint."
```

## Interaction Signs

| Sign Entity | Position | Text | Font Size | Color | Billboard |
|-------------|----------|------|-----------|-------|-----------|
| sign_welcome | [0, 2.5, -35] | "Welcome to Aldric's Hollow" | 28 | #f5e6c8 | false |
| sign_market | [5, 2.5, 1] | "Market Square" | 20 | #ffffff | true |
| sign_church | [-2, 2, 7] | "Chapel of the Dawn →" | 18 | #ffffff | true |
| sign_forge | [-5, 2.5, 2] | "The Forge ↑" | 18 | #ffffff | true |
| sign_healer | [9, 2, 6] | "Healer — Salves & Tonics" | 16 | #ffffff | true |
| sign_bridge | [-5, 1.5, 8] | "River Crossing" | 16 | #ffffff | true |

## Fall Protection

If the player somehow falls below Y = -5 (e.g., off the terrain edge or into a river gap), respawn at the default spawn point:

```
gen_add_trigger:
  entity: "fall_protection_zone"
  trigger_type: "area_enter"
  trigger_params: { y_threshold: -5 }
  action: "teleport"
  action_params: { destination: [0, 1, -38] }
```
