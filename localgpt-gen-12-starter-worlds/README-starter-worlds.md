# LocalGPT Gen — 12 Starter World Skills

A complete set of AI-readable world blueprints for the LocalGPT Gen template SEO loop. Each directory is a self-contained **skill** that any LLM connected to the LocalGPT Gen MCP server can read and build.

## The 12 Worlds

| # | World | Genre | Gameplay | Complexity |
|---|-------|-------|----------|-----------|
| 1 | `medieval-village/` | RPG / Exploration | Find 5 medallions, talk to NPCs, explore cottages | Medium |
| 2 | `cyberpunk-neon-city/` | Parkour / Sci-Fi | Reach rooftops via teleporters, collect 3 data chips | Medium-High |
| 3 | `haunted-house/` | Horror / Puzzle | Find 3 keys to escape the mansion | Medium |
| 4 | `enchanted-forest/` | Peaceful / Collection | Gather 7 orbs for fairy ring ritual | Medium |
| 5 | `space-station/` | Sci-Fi / Repair | Fix 4 station systems with parts from modules | High |
| 6 | `modern-city/` | Urban / Time Challenge | Deliver 5 packages before timer runs out | Medium |
| 7 | `underwater-ocean/` | Environmental / Peaceful | Clean 6 pollution pieces to restore reef | Low-Medium |
| 8 | `japanese-temple/` | Walking Sim / Meditation | Visit 5 haiku stations to unlock inner temple | Low |
| 9 | `cozy-farm/` | Farming Sim / Cozy | Harvest 10 crops, deliver to barn | Low |
| 10 | `backrooms/` | Horror / Liminal | Find the real exit among 3 fake loop teleporters | Medium |
| 11 | `winter-wonderland/` | Cozy / Seasonal | Collect 5 snowman parts around frozen lake | Low |
| 12 | `alien-bioluminescent/` | Sci-Fi / Puzzle | Solve 4 crystal tone puzzles to reach Nexus Pool | High |

## File Structure

### Full treatment (Medieval Village, Space Station)
```
world-name/
├── SKILL.md                  ← Entry point: metadata, knowledge index, generation strategy
├── world.md                  ← Master spec: region map, phases, environment, player config
├── regions/
│   ├── region-a.md           ← Per-region entity list, positions, materials, colliders
│   └── region-b.md
├── behaviors/
│   └── effects.md            ← Behavior patterns: wind sway, spin, pulse, path_follow
├── audio/
│   └── soundscape.md         ← Ambience layers, spatial emitters, audio zones
├── avatar/
│   └── player.md             ← Spawn, movement, quest flow, NPC dialogue trees, HUD
└── layout/
    └── blockout.md           ← Spatial zones, sightlines, elevation, collision coverage
```

### Essential pair (all 12 worlds have at minimum)
```
world-name/
├── SKILL.md                  ← Metadata + generation strategy + design intent
└── world.md                  ← Full world spec: layout, entities, environment, audio, quest, player
```

## How To Use

### Option A: Drop into LocalGPT Gen workspace
1. Copy any world directory into `{workspace}/skills/`
2. Open a conversation with Claude connected to LocalGPT Gen MCP
3. Say: "Load the medieval-village skill and build it"
4. The LLM reads SKILL.md → follows generation strategy → calls MCP tools → world renders

### Option B: Use as prompt reference
1. Open any `world.md` file
2. Copy the relevant sections into your prompt
3. Modify as needed for your own world

### Option C: Generate .ron data without the engine
1. Have an LLM read the .md files
2. Ask it to produce the corresponding .ron entity definitions
3. Load the .ron files with `gen_load_world` later

## What These Files Can vs. Cannot Do

### ✅ Can do (just .md files)
- Full world design specification readable by any LLM
- Version control in git (diff-friendly text)
- Human review and editing
- Multiple LLMs interpret the same spec differently
- SEO landing page content generation from descriptions

### ❌ Requires LocalGPT Gen engine
- Rendering the 3D scene
- Producing `world.ron` entity data with precise transforms
- Recording `generation-log.jsonl` tool call history
- Exporting to .glb / .html
- Taking screenshots for marketing

## Feature Coverage Across Templates

| Feature | Medieval | Cyber | Horror | Forest | Space | City | Ocean | Temple | Farm | Back | Winter | Alien |
|---------|----------|-------|--------|--------|-------|------|-------|--------|------|------|--------|-------|
| Terrain | ✅ | flat | ✅ | ✅ | — | flat | ✅ | ✅ | ✅ | — | ✅ | ✅ |
| Water | ✅ | — | — | ✅ | — | ✅ | ✅ | ✅ | ✅ | — | ice | glow |
| NPCs | 3 | 1 | — | 1 | 1 | — | 1 | 1 | 1 | — | 1 | 1 |
| Dialogue | ✅ | ✅ | — | ✅ | ✅ | — | ✅ | ✅ | ✅ | — | ✅ | ✅ |
| Collectibles | 5 | 3 | 3 | 7 | 4 | 5 | 6 | 5 | 10 | — | 5 | 4 |
| Doors | 5 | — | 6 | — | — | — | — | 1 | — | 1 | — | — |
| Teleporters | — | 3 | — | — | 4 | — | — | — | — | 3+1 | — | ✅ |
| Signs | 6 | 3 | 2 | — | — | ✅ | — | ✅ | — | 1 | ✅ | — |
| HUD | score | chips | keys | orbs | sys | timer | health | med. | crops | — | parts | reson. |
| Physics | static | kinem. | static | static | low-g | kinem. | buoy. | static | static | static | static | static |
| Camera | 3rd | 1st | 1st | 3rd | 1st | 3rd | 1st | 3rd | 3rd | 1st | 3rd | 1st |
