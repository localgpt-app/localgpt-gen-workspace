---
name: "haunted-house"
description: "A horror escape puzzle in a haunted mansion. Find 3 keys, unlock doors, survive flickering lights and moving furniture."
user-invocable: true
metadata:
  emoji: "👻"
  type: "world"
  version: "2.0"
  genre: "Horror / Puzzle / Escape"
  complexity: "medium"
  estimated_entities: 80
  features: [terrain, doors_with_keys, collectibles, triggers_proximity, triggers_timer, flickering_lights, signs, hud, spatial_audio]
  seo:
    primary_keyword: "3D haunted house"
    secondary_keywords: ["horror environment template", "haunted mansion 3D", "free 3D haunted house"]
useWhen:
  - contains: "haunted"
  - contains: "horror house"
  - contains: "spooky mansion"
---

# Horror Haunted House — "Escape the Manor"

Player is locked inside a decrepit Victorian mansion. Find 3 keys hidden in rooms to unlock the front door and escape. Lights flicker. A chair moves when you leave a room. Something scratches behind the walls.

## World Knowledge Index

| Domain | Spec File | Description |
|--------|-----------|-------------|
| Master plan | `world.md` | Room layout, key locations, scare sequence |
| Interior | `regions/mansion-interior.md` | Foyer, library, kitchen, hallway, bedroom, basement |
| Exterior | `regions/mansion-exterior.md` | Graveyard, dead trees, fog, moon |
| Horror effects | `behaviors/horror-effects.md` | Flickering lights, moving chair, whisper triggers |
| Soundscape | `audio/dread-ambient.md` | Wind, creak, distant fireplace, NO music |
| Player | `avatar/player.md` | First-person, SLOW movement, 3-key quest |

## Design Intent

**Vulnerability through slowness.** Walk speed 3.5 (70% of normal). First-person locks the player into the space. The horror comes from atmosphere, not monsters: flickering lights, a chair that moves when you leave a room, doors that creak, whispers on approach. Silence is the primary instrument — no background music. Only wind, wood creak, and the player's own footstep echoes.

## Key Constraints

- First-person ONLY (third-person undermines horror)
- Slow movement: walk 3.5, run 6 (no sprint escape fantasy)
- 3 keys: rusty (library), silver (kitchen), golden (basement)
- rusty_key → unlocks basement_trapdoor
- silver_key → unlocks bedroom_door
- golden_key → unlocks front_door_exit (win condition)
- Scare triggers fire ONCE each (no repetition dulls impact)
- NO emissive on keys — they should be hard to spot
- Basement has only ONE dim light (intensity 50)

## Playtest Checklist

- [ ] Rusty key visible in library bookshelf if player looks carefully
- [ ] Silver key in kitchen drawer area (on floor near counter)
- [ ] Golden key in basement corner (barely lit)
- [ ] Each key unlocks correct door and only that door
- [ ] Front door opens → victory text displays
- [ ] Chair moves to room center when player exits and re-enters library
- [ ] Whisper sound plays once in upstairs hallway
- [ ] Heavy footsteps sound plays once when entering basement
- [ ] Flickering lights vary in frequency (foyer fast, hallway slow)
- [ ] "GET OUT" sign on foyer wall readable
