---
name: game-design
description: What makes a game good - core mechanic, levels, procedural generation, difficulty, scoring, tutorials, story, look, effects, sound. Use to ideate, design, polish or review any game.
---

# Game design

This skill is the design pillar of making a game: what it should be and what makes it good. How to structure, test and ship the code belongs to the web-game-build skill; making or sourcing the art and audio belongs to the game-assets skill.

Read only the sections the task touches. These are tactics that usually help, not laws: a game is judged by people playing it, so present choices as proposals, try the smallest version, and let playtests decide. When a section runs out, look up current sources (postmortems, design talks) and cite them.

Two questions before applying anything:

- **What should the player feel in this moment?**
- **What is the one thing the eye and ear should notice right now?**

## Contents

Idea and core mechanic · Level design · Procedural generation · Level builder · Difficulty and flow · Scoring and progression · Tutorial and onboarding · Narrative · Visual style · Effects and feedback · Sound and music · Reviewing a game

## Idea and core mechanic

- **Start from a feeling and a verb.** Ask what the player should feel and what they do, second to second. Offer two or three distinct directions, each with its core verb, how the player fails, and its main risk; say which you would try first and why.
- **Study references for their logic.** When the person names games or shares footage, look at what those games do moment to moment: the verb, the failure, the camera, what makes a level hard. Borrow that logic, not characters, art or levels.
- **Mechanic before content.** The core action should be satisfying on an empty test level. If it is not, levels and art will not save it.
- **A way to fail and a way to be good.** If losing is nearly impossible or the best strategy is obvious, there is no game yet. Look for a trade-off the player makes constantly.
- **Pressure makes skill visible:** a clock, a draining resource, a rival.

## Level design

- **Introduce, develop, twist, conclude,** for each mechanic and each level. A new element first appears alone, somewhere it cannot punish.
- **Teach by layout, not text.** Shape the space so the natural move is the lesson.
- **One idea per level.** If you cannot say what a level is about in a sentence, cut or split it.
- **A safe line and a risky line;** the risky one is faster or richer. Put rewards where taking them costs time or safety.
- **Rhythm.** Alternate tension and release, tight and open, fast and slow; a breather after a spike.
- **Readability:** goal visible or signposted early, landmarks, a lit or framed critical path, hazards that look hazardous.
- **Let the space make the challenge.** Slopes, funnels, forced splits and moving obstacles create situations; walls and rails only prevent them.
- **Checkpoint before difficulty,** and make retry instant.
- **Order by measured difficulty** with a saw-tooth, not a straight ramp.

## Procedural generation

- **Author the rules, pieces and pacing; generate the arrangement.**
- **Construct valid, then test for good.** Prefer methods that cannot produce a broken result (build backwards from the goal, grow from a guaranteed path, assemble from pieces known to connect).
- **Generate many, keep few.** Score candidates on what you care about (length, real choices per step, how long mistakes stay plausible, variety) and pick the best.
- **A few meaningful dials** (size, density, element mix, target difficulty), each checked to move the measured result.
- **Same seed, same level,** which enables daily challenges and sharing.
- **Guard against sameness:** structure at more than one scale, set pieces, a theme per level; reject near-duplicates.

## Level builder

- **Edit and play in the same view,** one key apart.
- **Small palette, snapping, sensible defaults;** a new level is playable after three clicks.
- **Show whether the level can be finished** and flag unreachable or unused pieces.
- **Shareable** as a short code or link.
- **If players publish levels,** require the author to beat one first, and plan moderation before opening it up.

## Difficulty and flow

Flow needs challenge matched to skill, clear goals and immediate feedback.

- **A clear goal at every moment.**
- **Feedback on every input and outcome,** including why they failed.
- **Fail fast, retry faster:** about a second, no menus, music continuing.
- **Saw-tooth difficulty.** After each spike, a level that lets the player enjoy the skill they just earned.
- **Fair means predictable.** Telegraph, be consistent, and be generous at the edges while looking strict.
- **No interruptions mid-action.**
- **Depth without demand:** optional objectives, faster lines, harder medals; consider assist options.
- **Fix the drop-off first.** Where testers quit or stall is where the curve is wrong.

## Scoring and progression

- **Score what you want players to do,** and make the two or three things you care about pull against each other.
- **Legible formula:** show the number moving during play and the breakdown at the end.
- **Thresholds** (medals, stars, ranks) with the next one shown; just-missed is the strongest reason to retry.
- **Three loops:** seconds (the action feels good), minutes (finish, beat a best), sessions (unlock, master, complete). Each needs a reward.
- **Personal bests before leaderboards;** friend or daily boards in between.
- **Unlock to teach and to pace,** not to pad.
- **Never lose the player's progress,** and return them exactly where they were after an interruption.

## Tutorial and onboarding

- **Playing within seconds.** The first input does something satisfying.
- **One thing at a time, by doing,** where the only available action is the lesson and failure costs nothing.
- **Show, then prompt, then get out of the way.** Prompt only on hesitation; remove it once done.
- **The first levels are the tutorial.**
- **Teach the fail state early and safely.**
- **Rules in the player's words, in one line, at the moment they matter.**
- **A light reminder for returning players.**
- **Watch a fresh person play two minutes without help.** Every stall is a tutorial bug.

## Narrative

- **Let the mechanic carry the story.** Ask what the core action means in the fiction and why the rules are what they are.
- **Show through the world and through play;** keep lines short and at starts and ends, not mid-action.
- **One voice, one want, one turn** is enough for a small game.
- **A title and one sentence per level** can carry an arc.
- **Shape:** calm opening that teaches, rising complication, a twist, an ending that uses the mechanic one last way.
- **Test by retelling:** ask a player what happened. What they omit is not landing.

## Visual style

- **Pick a look you can finish.** A small palette with one accent reserved for what matters, and two or three materials done well.
- **Value first, colour second.** In greyscale, the player, hazards and goals should separate from the background. Do not rely on colour alone to carry a rule.
- **Light for shape and depth:** one key light with soft shadows, a dim fill, fog or gradient for distance, contact shadows so nothing floats.
- **Materials say what things are:** distinguish rule types by silhouette and material. Glow is a signal; spend it only where the player should look.
- **Restrained post-processing:** bloom on genuinely bright things only, a grade, then vignette and fine grain. If removing an effect does not change how the frame reads, remove it.
- **Camera is part of the art.** Frame the next two seconds, smooth it, and add small speed-dependent changes for sensation.
- **Motion over detail.** Ease everything; keep a slow idle motion in the world.
- **Ask what style words mean** to the person before committing.

## Effects and feedback

- **Confirm every action on two channels** (motion, light, sound, haptics).
- **Anticipation, action, reaction:** a brief wind-up, the event, a settle.
- **Scale to importance.** If everything shakes, nothing does.
- **Standard kit:** squash and stretch, a few frames of hit-pause, a short decaying camera kick, particles that inherit velocity, a flash on state change, trails.
- **Telegraph danger, celebrate success.**
- **Never hide what the player is steering.** Offer reduced motion; avoid full-screen flashes.

## Sound and music

- **Sound from the first playable.** A silent prototype feels worse than it is.
- **One sound per meaningful event, with variation:** a few percent of pitch change and two to four takes; a transient layered with a body for weight.
- **Tie sound to the simulation:** speed, force, size or height mapped to pitch, volume or filter.
- **Mix in groups** (music, effects, interface, ambience); duck music under important effects; cap simultaneous voices.
- **Music that follows play:** layers brought in with intensity, changing on bar lines. Quantising player-triggered notes to beat and scale makes play sound intentional.
- **Ambience and silence:** a quiet bed makes the world exist; near silence before a big moment makes it land.
- **Give the player separate music and effects volume.**

## Reviewing a game

Check in this order, because earlier problems hide later ones:

1. Is the core action satisfying on an empty level?
2. Can the player fail, and get better?
3. Do they always know the goal and why they lost?
4. Does every action get feedback they can see and hear?
5. Does difficulty rise with rests, and does each level have one clear idea?
6. Is there a reason to play again?
7. Only then: look, sound, story and polish.

Report findings in that order, with the one change you would make first.
