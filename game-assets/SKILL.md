---
name: game-assets
description: Get and prepare game art and audio - textures, static and rigged 3D models, animations, sprites, UI, fonts, sound, music. Use to make, source, budget, optimize or unify a game's assets.
---

# Game assets

This skill is the production pillar of a game's look and sound: what assets exist, where they come from, the limits they must fit, and how they get into the build. What the game should look and sound like is a design question (game-design); how the project loads and renders things is an engineering one (web-game-build).

## Contents

Start with what can be finished · Asset types and their constraints · Budgets · Four routes to get assets · Conventions every asset follows · Pipeline into the build · Consistency pass · Hand-over

## Start with what can be finished

The most common way a small game stalls is an art style that needs more assets than anyone can make. Before producing anything:

1. **Write the asset list,** by type and count, from the tables below. Include every state and animation; a character with five animations is five jobs.
2. **Set budgets** for the weakest target device (next section but one).
3. **Choose a route for each asset** (made in code, sourced, generated, commissioned). Mixed is normal.
4. **Pick a style that fits the routes and budgets.** If most things will be made in code, design for flat colour, simple shapes and strong lighting. If they come from one pack, adopt that pack's style for everything else.
5. **Write a one-page style sheet:** palette with hex values, shape and line rules, material rules, scale, lighting direction, and three reference images. Every asset is checked against it.

Build with placeholders first (boxes, flat colours, beeps) at the correct size, pivot and timing, and replace them once the game is fun. Do not polish art for a mechanic that may be cut.

## Asset types and their constraints

Most games are made of the types below. For each asset on the list, record the constraints in the right-hand column; they are what an artist, a generator or a pack must satisfy.

### Visual, 3D

| Type | What it is | Constraints to specify |
|---|---|---|
| Static model | Props, environment pieces, pickups | Triangle count, real-world size, pivot position (base centre for things that sit on the ground), number of materials (aim for one), whether it needs a separate simple collision shape, level-of-detail versions if seen far away |
| Modular kit | Walls, floors, track or terrain pieces that snap together | Grid size, snap points, matching edges, shared material and texture atlas |
| Rigged model | Characters, creatures, anything that bends | Triangle count, bone count, at most four bone influences per vertex, rest pose, facing direction, named attachment points (hand, head), one skeleton shared across characters where possible |
| Animation clip | Idle, walk, run, jump, hit, death, actions | Name, length, frame rate, whether it loops cleanly, whether the character moves in place or the clip moves the root, key event frames (footstep, hit lands), transitions that must blend |
| Material | How a surface responds to light | Which maps it uses (base colour, normal, roughness, metalness, ambient occlusion, emissive), whether it is transparent (expensive, sorts badly), whether it is shared |
| Texture | The image maps for materials | Resolution, channel packing (roughness, metalness and occlusion in one image), colour space (base colour and emissive are sRGB, the rest are linear data), whether it tiles |
| Environment | Sky, backdrop, lighting probe | Format, resolution, whether it is used for reflections and lighting |

### Visual, 2D and screen

| Type | What it is | Constraints to specify |
|---|---|---|
| Sprite and sprite sheet | 2D characters, objects, frames of animation | Pixel size, pixels per world unit, anchor point, frame count and rate per animation, padding between frames, whether it is pixel art (no smoothing) |
| Tileset | Repeating 2D level pieces | Tile size, edge and corner variants, spacing |
| Interface art | Buttons, panels, icons, cursors, HUD | Vector where possible, a shared corner radius and stroke, states (normal, hover, pressed, disabled), minimum touch size, safe-area margins |
| Font | Text | Licence allows embedding, weights used, character set needed (subset to it), legibility at the smallest size |
| Effects | Particles, trails, flashes, decals, screen effects | Particle count ceiling, texture size, blend mode, duration, whether it can be turned down for reduced motion |
| Shader | Custom look for a surface or the screen | Inputs, cost, fallback on weak devices |
| Marketing | Icon, screenshots, capsule images, trailer clips | Sizes required by the target store; capture from real builds |

### Audio

| Type | What it is | Constraints to specify |
|---|---|---|
| Sound effect | One-shot sounds for actions and events | Length, mono for positioned sounds, number of variations (two to four for anything frequent), loudness relative to the set, no silence at the start |
| Loop | Ambience, engines, continuous states | Seamless loop points, length long enough not to be noticed repeating |
| Music | Tracks, or layers of one track | Tempo and key (so layers and stingers fit), loop points, layers or intensity versions if the music follows play, length |
| Stinger | Short musical cue for win, lose, pickup | Key and tempo matching the music, length |
| Voice | Narration, barks | Script, takes per line, consistent recording distance and loudness, subtitle text for every line |

### Data that behaves like an asset

Level files, animation state machines, dialogue tables and localisation tables. Keep them as plain versioned data alongside the art, with the same naming rules.

## Budgets

Set numbers before making assets, because fixing an over-budget game afterwards means remaking them. The figures below are starting points for a web game that should also run on a mid-range phone; measure on the weakest target device and adjust. Check current guidance for the engine and formats in use.

| Budget | Starting point |
|---|---|
| First load (to the first playable moment) | A few megabytes; under about 10 MB before the player can do something |
| Total triangles on screen | Low hundreds of thousands on phones; a few times that on desktop |
| Draw calls per frame | Around 100 to 200 on phones; share materials, instance repeats, merge static geometry |
| Hero character | Roughly 5,000 to 15,000 triangles, 30 to 60 bones |
| Ordinary prop | Hundreds to a couple of thousand triangles |
| Texture size | 1024 square for most things, 2048 for a hero or an atlas, 512 or less for small props |
| Texture memory | Use compressed GPU texture formats; uncompressed textures cost far more memory than their file size suggests |
| Animated characters on screen | Tens, not hundreds, unless the animation is baked or instanced |
| Transparent surfaces and particles | As few and as small on screen as the look allows; overdraw is the usual phone bottleneck |
| Sound effects | Short compressed files, tens of kilobytes each |
| Music | Compressed stereo, about a megabyte a minute, loaded after the first screen |
| Simultaneous sounds | A cap of roughly 16 to 32 voices |

A stylised look with flat colour, shared palettes and few textures stays inside these limits far more easily than a realistic one.

## Four routes to get assets

### 1. Made in code

Best for abstract, geometric or stylised games; it keeps the build small and the style consistent. Be direct about the limit: code is good at shapes, materials, patterns, particles and synthesized sound, and poor at detailed characters, faces, organic illustration and convincing character animation.

- **Geometry:** primitives, extrusions, lathes, rounded boxes, instanced repeats, simple procedural meshes.
- **Materials and shaders:** gradients, patterns, rim light, noise. A good material on a simple shape often beats a detailed model.
- **Textures:** drawn to a canvas at load instead of shipped as files.
- **Motion:** procedural animation (springs, squash and stretch, bobbing, simple inverse kinematics) for objects and simple creatures.
- **2D art:** SVG for icons, interface and simple sprites.
- **Sound:** synthesized effects and simple generative music, for prototypes and deliberately minimal games.

### 2. Sourced

The fastest route to a full set, and the usual answer for rigged characters and animation libraries. Search current free and paid libraries for packs that match the style sheet and budgets; prefer one coherent pack over many mismatched singles, and prefer characters that share a standard skeleton so animations can be reused across them.

- **Check the licence of every asset before using it,** on the asset's own page, and record it. Know the difference between public-domain-style licences, ones that require credit, ones that forbid commercial use, and ones that forbid redistribution. Do not assume a site-wide licence applies to every file.
- **Keep a credits file** listing each asset, author, source link and licence, and show required credits in the game.
- **Never take assets from other games,** or anything whose licence you cannot find.

### 3. Generated with AI tools

Useful for concept art, textures, backgrounds, some sprites, and drafts of voice and music. Results vary; plan for selection and clean-up.

- Use a generator only if one is available in the session or the person has one; otherwise write the prompts for them to run.
- **Write prompts from the style sheet,** reusing the same style wording and references across a set so pieces match.
- **Check the tool's terms** for commercial use and ownership, and do not ask for a named artist's style or an existing game's characters.
- Generated 3D models usually need cleanup, sensible topology and a rig before they can be animated; say so, and check them against the budgets.

### 4. Commissioned or made by the person

When the game needs a distinctive look. Help by writing the brief: the asset list with the constraint columns filled in, the style sheet, the budgets, the conventions below, delivery format, and usage rights.

## Conventions every asset follows

Agree these once and put them in the brief; mismatches here cause most integration bugs.

- **Units and axes:** one world unit means one metre (or one tile); the same up axis and forward direction for every model.
- **Pivots:** at the base centre for things that stand on the ground, at the hinge for things that rotate.
- **Transforms applied:** no leftover scale or rotation on exported models.
- **Naming:** lowercase, hyphenated, type-first (`mdl-crate`, `anim-hero-run`, `tex-floor-basecolor`, `sfx-jump-01`, `mus-level1-layer2`). Animation clips and attachment points use the same names on every character.
- **Collision is separate from visuals:** simple shapes (boxes, capsules, low-detail hulls) authored or derived for physics.
- **Loudness:** all sound effects levelled against each other, music a step below them, voice clearly above music.
- **Source files kept:** the editable original for every exported asset lives in the repository or a linked store.

## Pipeline into the build

Check the current recommended tools and loader setup before doing this; they change.

- **3D models and animations:** deliver as glTF binary, with animations as named clips in the same file or in a shared animation file for a common skeleton. Compress geometry and textures with the formats the loader supports. Verify in a viewer that scale, pivot, materials and every clip are right before wiring it into the game.
- **Textures:** power-of-two sizes, no larger than needed on screen, compressed GPU formats where supported, mipmaps on, correct colour space per map.
- **Sprites:** packed into atlases with padding and a data file of frames; consistent pixels per unit.
- **Fonts:** subset to the characters used.
- **Audio:** compressed in a format all target browsers play, with a fallback; trimmed, levelled, consistent sample rate. Decode short effects up front; stream or late-load music.
- **Loading:** an asset manifest with sizes; load what the first screen needs first and the rest in the background; show progress; cache.
- **Check the budgets in the running game,** not just per file: frame time, draw calls, memory and download size on the weakest target device.

## Consistency pass

Before calling the art done, look at everything together in the game, not in isolation:

- Same palette, lighting direction, outline rule and level of detail across assets.
- Scale is consistent and things sit on the ground; characters' feet do not slide when they move.
- Animations blend without popping, and their timing matches the game's actual speeds and hit moments.
- Interface elements share one shape language and spacing.
- Sounds share a character, sit at matched loudness, and fire on the right frame.
- The player, hazards and goals still stand out from the environment.

Anything that fails gets restyled, replaced or cut. One mismatched asset makes the rest look worse.

## Hand-over

State which assets are final and which are placeholders, where each came from, how the build measures against the budgets, and any licence obligations the person now has.
