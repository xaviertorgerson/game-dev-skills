# Game dev skills for Claude

Three skills that help Claude design, build and dress a game with you. They were distilled from building two web game demos through several rounds of playtest feedback.

| Skill | Pillar | What it covers |
|---|---|---|
| [`game-design`](game-design/SKILL.md) | What the game is | Core mechanic, level design, procedural generation, level builders, difficulty and flow, scoring, tutorials, narrative, visual style, effects, sound and music, and an order for reviewing a game that is not working |
| [`web-game-build`](web-game-build/SKILL.md) | How it is built | Scoping, a three.js + TypeScript + Vite stack, when to use a physics engine and when to write your own, project structure, bots and solvers that play every level, iterating on playtest notes, rendering bugs, shipping to web, phones and Steam |
| [`game-assets`](game-assets/SKILL.md) | What it is made of | Asset types and the constraints each needs (textures, static and rigged 3D models, animations, sprites, interface art, fonts, sound, music), budgets, four ways to get assets, conventions, the pipeline into a web build |

The skills refer to each other, so they work best installed together. `game-design` is engine-independent; `web-game-build` assumes a web stack.

## Status

These are first versions. They have not yet been tested on a fresh game idea, and the budget numbers in `game-assets` are starting estimates to check on your own target devices.

## Install

### Claude apps (web, desktop, mobile)

Each skill is uploaded as a ZIP of its folder. Ready-made ZIPs are in [`dist/`](dist).

1. Download `game-design.zip`, `web-game-build.zip` and `game-assets.zip` from `dist/`.
2. In Claude, open **Customize > Skills**, click **+**, then **Create skill**, then **Upload a skill**.
3. Upload each ZIP and make sure each skill is switched on.

Skills need code execution and file creation to be enabled. On Team and Enterprise plans an owner may have to allow skills first. See [Use skills in Claude](https://support.claude.com/en/articles/12512180-use-skills-in-claude).

### Claude Code

Copy the skill folders into your personal skills folder (available in every project):

```bash
git clone https://github.com/xaviertorgerson/game-dev-skills.git
mkdir -p ~/.claude/skills
cp -r game-dev-skills/game-design game-dev-skills/web-game-build game-dev-skills/game-assets ~/.claude/skills/
```

Or into one project only, under `.claude/skills/` in that project. See [Extend Claude with skills](https://code.claude.com/docs/en/skills).

## Use

Claude picks a skill up when your request matches it; you do not need to name it. Examples:

**Ideate and design** (`game-design`)

> I want a short-session puzzle game for phones that feels like Monument Valley meets Sokoban. Give me three directions.

> Here's my level list. Players say the middle is boring. What's wrong with the difficulty curve?

> Design a scoring system for my time-attack game so that speed and safety pull against each other.

**Build and iterate** (`web-game-build`)

> Build a first playable of a tilt-the-world marble game in the browser. Keyboard and touch.

> I played the build. Notes: 1) too easy 2) the camera fights me 3) black screen on my laptop.

> Write a bot that plays every level and tell me which ones it can't finish.

**Art and audio** (`game-assets`)

> List every asset this game needs and set budgets so it runs on a mid-range phone.

> Find me a free low-poly character pack with walk, run and jump animations that I can use commercially.

> Write a brief for an artist for the hero character, including the rig and animation list.

In Claude Code you can also invoke a skill directly, for example `/game-design`.

## Layout

```
game-design/SKILL.md
web-game-build/SKILL.md
game-assets/SKILL.md
dist/                  ZIPs for uploading to the Claude apps
```

## Licence

No licence has been chosen yet, so all rights are reserved by default. Add one if you want others to reuse or adapt these.
