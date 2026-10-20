# Pacman3D - todo

## PLAN: from "tilted 2D maze" to a real 3D chase-cam maze game (multi-agent)
Today the maze is a flat grid seen at an angle through one fixed perspective camera (see `NOt v 3d.png`); the 3D is only visual (`renderer.ts` 893 lines, `engine.ts` 998 lines, 5 levels, 5 ghosts). Goal: it plays and feels like a 3D game. Three.js stays, game logic stays grid-based underneath so ghost AI and tests keep working.
**Art rule:** original characters only. No Pac-Man or arcade-ghost likenesses: design an original chomper creature and original "glitch" enemies, and keep all names original.

**Agents.** Hermes = orchestrator (splits work, assigns, merges, runs the gate). Claude = core and hard reasoning. Freebuff = bulk/free-tier work. Antigravity = visuals and real-browser verification. Hermes routes by task, falls back down its provider chain if a quota wall hits, and never lets two agents edit the same file.

| Phase | Hermes | Claude | Freebuff | Antigravity |
|---|---|---|---|---|
| 0 Setup | Create branch `3d`, freeze `engine.ts` public API, write a task board here | Split `renderer.ts` into modules (scene, camera, maze mesh, actors, fx) behind an interface | Add Vitest + unit tests for ghost targeting and maze helpers (safety net before changes) | Record baseline screenshots + fps |
| 1 Camera + movement | Review gate | Chase camera behind the player, smooth turn at junctions, free look option, 3D collision-free smooth movement on the grid | Gamepad + swipe + keyboard input layer, settings screen (volume, bloom, FOV, camera mode) | Eyeball camera feel in a real browser, tune FOV/offset/shake |
| 2 Real 3D world | Review gate | Maze with real wall height, lit corridors, tunnels, ramps/bridges as a second layer (`constants.ts` gets a z-level), minimap | Two extra maze layouts as data + level progression table | Neon materials, fog, bloom, instanced orbs/walls for perf, retro-sun skybox |
| 3 Characters + feel | Review gate | Animated 3D player and enemies (squash/stretch, state-driven), power-up visuals, death/win sequences | Synth sfx additions, 3D positional audio, music layers per level | Original character models/shaders, particle fx, trail and glow polish |
| 4 Ship | Final gate: build, tests, smoke | Perf pass (draw calls, mobile), bug sweep | Local top-10 leaderboard, README + controls, versioned release names (`Pac-Neon - Windows Setup v<ver>.exe`) | Real-device check (phone + desktop), screenshots/GIF for README and profile |

**Gate for every phase (Hermes enforces):** `npm run build` clean, tests pass, game boots without console errors, a screenshot from Antigravity attached, this file updated. Fail = back to the owner agent.
**Handoffs:** each agent appends a dated one-line note under "Handoffs" below; Hermes reads them before assigning the next task.
**Ask the owner before:** pushing to GitHub, publishing a release, anything that changes what others see.

## Handoffs
- (empty)

## Old ideas (owner picks)
## IDEA - not ready, owner decides
- [ ] Mobile polish: test the on-screen d-pad on a phone-sized viewport and add swipe controls
- [ ] Gamepad support (Gamepad API) alongside keyboard and touch
- [ ] Settings screen: master volume, bloom strength, CRT scanline default
- [ ] Local top-10 leaderboard with initials instead of one hi-score
- [ ] More levels / a second maze layout (`game/constants.ts` holds the maze grid)
- [ ] Automated checks: unit tests for ghost targeting in `game/engine.ts` (Blinky/Pinky/Inky/Psychic rules)
- [ ] Package the Electron build with a clear versioned release name
