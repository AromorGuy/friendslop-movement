# Chip Stack Movement Lab

A first-person physics movement controller for the browser, built with [Three.js](https://threejs.org/) and [Rapier](https://rapier.rs/). It runs on a test course with labeled steps, ramps, platforms and pushable dice, so you can check each movement limit.

## Play

Open `index.html` in a browser, or use the GitHub Pages link for this repo. No build step is needed: Three.js, Rapier and the fonts load from CDNs.

| Key | Action |
|---|---|
| WASD / arrows | Move |
| Shift | Sprint |
| C | Crouch |
| Space | Jump |
| Right mouse | Zoom |
| R | Ragdoll |
| T | Respawn |

Clicking **Click to play** locks the mouse for looking around. If the browser won't lock it, drag with the left mouse button instead. Esc releases the mouse, and double-clicking the scene locks it again.

## How the movement works

- The player is a dynamic rigid body (mass 1, linear damping 0.4) with rotation locked, simulated at a fixed 50 Hz.
- **Walking:** each step pushes the velocity toward the target speed (walk 8, sprint 12, crouch 5 m/s, acceleration 7). With friction and damping, the real top speeds settle at about 7.2 and 10.9 m/s.
- **Ground check:** a sphere cast below the body. Surfaces up to 75° count as ground.
- **Gravity:** 30 m/s², pulling toward the ground contact, so you stick to slopes instead of sliding.
- **Jump:** vertical velocity is set to +11 m/s, giving about 1.75 m of height.
- **Step-up:** ledges up to 0.5 m are climbed automatically.
- **Crouch:** lowers the head from 1.1 m to 0.6 m over 0.2 s.
- **Ragdoll:** rotation unlocks for 3 s, then the body turns upright again.
- **Camera:** head bob driven by speed, head sway, and a 1.25× FOV boost while sprinting.

Every value can be changed live from the **Tuning** panel in the top-right corner.

## Running locally

Any static file server works, for example:

```bash
python -m http.server 8000
```

Then open http://localhost:8000.
