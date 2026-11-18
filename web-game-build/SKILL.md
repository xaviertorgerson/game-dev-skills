---
name: web-game-build
description: Build, test, debug and ship web-first games (three.js + TypeScript; wraps for phones and Steam). Use to make, prototype, extend, fix or release a game, demo, mechanic or level generator.
---

# Web game build

This skill is the engineering and process pillar of making a game: how to structure it, prove it works, respond to playtests, and get it onto devices. Decisions about what the game is and what makes it good (mechanics, levels, look, sound, story, scoring, tutorials) belong to the game-design skill, and making or sourcing the art and audio belongs to the game-assets skill; load them when the task touches those.

## Four rules

1. **Only a person playing can say whether it is fun.** Bots, solvers and screenshots show a build works and can be finished. Every time you hand one over, say what a machine checked and what nobody has played.
2. **Keep the rules in a pure module** (no DOM, no renderer). The same code then runs headless at many times real speed, so a bot or solver can play every level before the person does, and you can tune by measuring.
3. **Get something playable in front of them early, then iterate on their notes.** Answer each note explicitly, including what you could not fix, and carry a short list of known gaps forward.
4. **If two rounds of patching have not fixed a problem, the layer underneath is wrong.** Say so and propose rebuilding that layer.

## Starting a game

Settle scope in a few questions before code: 2D or 3D, target devices and input, session length, single-player or not. Build a grey-box of the core action on one test level, with placeholder art and sound, before menus, real assets or more levels. If the request is beyond this stack (a large open 3D world, real-time online multiplayer, heavy authored 3D content), say so early and name what would fit better.

## Stack defaults

Deviate when the game calls for it and say why. Check current versions, install steps and import paths before writing code, and pin them; these libraries change between releases.

- **TypeScript (strict) + Vite**, as a normal multi-file project in a Git repository, committed at each playable build.
- **three.js** for 3D. For a purely 2D game prefer PixiJS, Phaser or plain canvas.
- **Physics:** if it supports the game (rigid bodies, characters, vehicles, joints), use Rapier. If it is the game (grid rules, a bespoke movement model, a special material), write it yourself in the core module. Mixed is fine with one clear boundary.
- **Audio:** WebAudio, or Howler.js with sample files; start it from a user gesture and resume after the tab is hidden.
- **Saves:** behind a small interface, with a version number and migrations, written so a crash mid-write cannot corrupt them.
- **Tests:** Vitest for the core; Playwright screenshots of title, mid-play and result.

```
src/core    rules, physics, level data, generators (pure)
src/render  scene, camera, materials
src/input   keyboard, pointer, touch, gamepad -> one intent object
src/audio   src/ui   src/game.ts (fixed-step loop, state machine)
assets/     models, textures, audio, plus a credits file
tools/      bots, solvers, generators, screenshot scripts
```

- Use a fixed timestep so browser and headless runs agree.
- Describe levels as data and derive collision and visuals from the same source.
- Seed all randomness so a level or run can be reproduced.
- Keep player-facing text in one table, not scattered through code.
- Expose a development hook on `window` to load a level, step the simulation and read state.

## Proving it works

- **A bot or solver plays every level.** If it cannot finish, the level is broken. Use its runs to measure levels (time, losses, choices) and to set thresholds, and label those as bot-derived until a person has played.
- **Tune by sweeping** a constant in a headless script and printing the result.
- **Run slow searches offline** (level generation, solving) and ship the results as data.

## Iterating on playtest notes

Restate each note in a table with what changed. Look for the cause behind the symptom before changing numbers. Re-run the bot or solver on everything you touched. End with known gaps and what was not verified.

## Debugging

- **Blank or black render on their machine only:** suspect NaN in a shader (clamp inputs to pow, sqrt, normalize, division) or a GPU difference. Add an on-screen error overlay and a switch that disables post-processing so they can report what they see.
- **Do not let a material sample a render target it is being drawn into.**
- **Headless software rendering** is for "does it draw and where", not frame rate or colour. Check on their device when you can; say when you could not.
- **Slow:** measure first. Instance anything numerous, bake what does not move, cap pixel ratio, scale effects down on touch devices.

## Shipping

The build is a static folder; any static host or itch.io works. Capacitor wraps it for phone stores; Tauri or Electron for Steam and desktop. Where and when to ship is the person's call; look up the target store's current requirements when they are ready.

## Later, not now

For a first playable or proof of concept, leave these as notes unless the person asks. Mention each once when it becomes relevant, so early choices do not close it off, and look up current practice when the time comes.

- **Multiplayer:** real-time online play changes the architecture (authoritative server, prediction, lag). If it is wanted eventually, keep the simulation deterministic and separate from rendering, which this structure already does. Local or turn-based play is much cheaper. Shared leaderboards, accounts and cross-device saves also need a server.
- **Playtesting and analytics:** watch a few new players without helping, and note where they stall or quit. Later, log level starts, completions, failures and quits to find the same thing at scale, with consent.
- **Publishing and business:** store pages, pricing, age ratings, platform fees and marketing are the person's decisions. Capture screenshots and a short clip from each good build so there is material when they need it.
- **Accessibility:** from the start, do not rely on colour alone, allow remapped controls, and offer reduced motion and separate volume controls. A fuller pass comes before release.
- **Localisation:** the text table above is enough for now; translation comes later.

## Before every hand-over

Core tests and the bot pass on every level; you have looked at fresh screenshots; no console errors; pause, restart and losing all work; touch input works if phones are a target; and you have written down what was not verified, which assets are placeholders, and any licence obligations.
