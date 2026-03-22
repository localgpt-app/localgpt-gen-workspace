# The Void — Audio Design

Space is silent. The station is not. The contrast between machine sounds inside and absolute nothing outside defines the audio experience. When you're in the hub, you hear life support. When you teleport to a module, the sounds change. The void between them is terrifying silence.

## Ambience Layers

**NONE.** No global ambient layer. This is the only starter world with zero always-on sound. Sound is purely spatial — you hear what's near you.

## Spatial Emitters

### Reactor Hum (hub)
- Position: [0, 0, 0]
- Sound: hum (frequency 45, warmth 0.9)
- Radius: 20
- Volume: 0.2
- The heartbeat of the station. Deep, constant, reassuring.

### Radio Static (docking bay)
- Position: [0, 0, -8]
- Sound: custom (waveform "white_noise", filter_cutoff 2000, filter_type "bandpass")
- Radius: 5
- Volume: 0.05
- Intermittent radio chatter from the approaching shuttle.

### Life Support Hiss (West module)
- Position: [-15, 0, 0]
- Sound: custom (waveform "white_noise", filter_cutoff 800, filter_type "lowpass")
- Radius: 4
- Volume: 0.08
- Air cycling through filters. Means the system is (partially) working.

### Engine Throb (South module)
- Position: [0, 0, -15]
- Sound: custom (waveform "sine", filter_cutoff 80, filter_type "lowpass")
- Radius: 5
- Volume: 0.1
- Deep rhythmic pulse. The engine module vibrates.

### Comms Ping (East module)
- Position: [15, 0, 0]
- Sound: custom (waveform "sine", filter_cutoff 1200, filter_type "bandpass")
- Radius: 4
- Volume: 0.04
- Periodic high-pitched ping — antenna scanning for signals.

## Design Rules

1. **No sound in transit.** Teleporting between hub and modules should have a moment of silence during the fade. The silence IS space.
2. **Each module sounds different.** Air hiss (life support), engine throb (engine), electronic ping (comms), near-silence (navigation — the cleanest room).
3. **The hub is the safest-sounding place.** Reactor hum = stability.
4. **Total max volume: 0.3.** Space stations are quiet. Machines hum, they don't roar.
