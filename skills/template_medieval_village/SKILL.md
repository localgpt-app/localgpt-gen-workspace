---
name: "template_medieval_village"
description: "Medieval village template - Willowmere. Nearly-flat perlin terrain (200x200m, height_scale 1.5), cobblestone town square with central well, 3 market stalls (Bakery, Herbs & Potions, Leatherworks), 5 thatched-roof cottages with smoking chimneys, patrolling Guard with quest dialogue, Blacksmith with forge fire audio and branching dialogue, 3 wandering Villagers. Cobblestone crossroads + dirt paths to cottages. 5 collectible gold coins (spinning, sparkle pickup). 20 pine trees on outer hills. Interactive proximity door on cottage 1. Sunset atmosphere with fog, wind audio. Player spawns at village entrance facing the square."
user-invocable: true
metadata:
  type: "world"
useWhen:
  - contains: "template_medieval_village"
---
# template_medieval_village

Medieval village template - Willowmere. Nearly-flat perlin terrain (200x200m, height_scale 1.5), cobblestone town square with central well, 3 market stalls (Bakery, Herbs & Potions, Leatherworks), 5 thatched-roof cottages with smoking chimneys, patrolling Guard with quest dialogue, Blacksmith with forge fire audio and branching dialogue, 3 wandering Villagers. Cobblestone crossroads + dirt paths to cottages. 5 collectible gold coins (spinning, sparkle pickup). 20 pine trees on outer hills. Interactive proximity door on cottage 1. Sunset atmosphere with fog, wind audio. Player spawns at village entrance facing the square.

This is a gen world skill. Load it with `gen_load_world` to restore the 3D scene,
behaviors, audio, avatar, and tours.

To export for external viewers, use `gen_export_world` with format "glb" or "gltf".
