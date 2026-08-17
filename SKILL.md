---
name: creator-script-engine
description: >-
  Turn reference clips from a creator or trend into a reusable shot-list template
  and a whole bank of ready-to-shoot short-form scripts. Decodes what the
  reference actually does beat by beat, isolates the ONE variable that changes
  per video, freezes everything else into a fixed reveal, then mass-produces
  numbered scripts with burned-text overlays, timings, and a batch shooting
  order. Use when the user gives reference videos / a creator handle / a trend
  and wants scripts, hooks, a hook bank, a content template, or a batch of UGC
  videos planned for TikTok, Reels, or Shorts.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash(ffprobe:*), Bash(ffmpeg:*), Bash(ls:*), AskUserQuestion, WebSearch, WebFetch
tags:
  - ugc
  - short-form
  - scriptwriting
  - social-media
  - creator
---

# Creator Script Engine

Reference clips in → a **template** + a **bank of shootable scripts** out.

The whole method is one idea:

> **Isolate the one thing that changes. Freeze everything else. Then mass-produce.**

A short-form format that works is never a pile of unique videos. It is one fixed
payoff beat plus a swappable hook. Once you find that seam, a hook bank of 15
becomes 15 videos from a single afternoon of filming — because you shoot the
fixed beat *once*.

Two artifacts come out of every run, and they are different documents on purpose:

| File | What it is | Who reads it |
|---|---|---|
| `TEMPLATE.md` | The **system** — decode, format spec, the one rule, hook bank | strategist / whoever briefs the creator |
| `SCRIPTS.md` | The **output** — numbered, ready-to-shoot scripts | the creator, on set, on their phone |

Never merge them. The template is argued and explains *why*; the scripts are
scannable and explain *what to do next*. A creator holding a phone will not read
a rationale.

---

## Core rules (do not violate)

- **Decode before you invent.** You do not get to write scripts until you have a
  beat-by-beat table of the reference clips and can state what makes the format
  work. Guessing the format produces on-brand-looking scripts that flop.
- **Find the invariant first.** Every template has exactly one variable part.
  If you think two things change, you have not found the seam yet — keep cutting.
- **The fixed beat is filmed once.** Design it so it is literally reusable
  footage, not "similar each time." This is where the leverage is; protect it.
- **Quantify confidence honestly.** When you decode a reference, say how sure you
  are (`~95%`, `~60% — audio unclear`). Never present a guess as a read.
- **Overlay text is the script.** For silent formats, the burned-in line IS the
  writing. Write it exactly as it should be burned — final, not paraphrased.
- **Present real choices** with AskUserQuestion for creative forks (hook angle,
  which product to feature, hard vs soft CTA). Always include an
  "I'll write my own" option.
- **Match the reference's length, don't improve on it.** If the references are
  9–14s, ship 9–14s. Adding explanation is the single most common way these die.
- **One creator per run.** A template that serves two creators serves neither.
  Check the roster in `references/creator-lanes.md` and stay out of taken lanes.

---

## Step 1 — Intake

Infer from the user's message; ask only for what is missing. You need four things:

1. **Reference material** — 1–3 clips (local files, links, or a creator handle).
   Two is the sweet spot: one is a coincidence, two proves the pattern, three
   confirms it. If you only get one, say so and lower your stated confidence.
2. **The creator** — who is shooting this, and what is their existing lane?
3. **The thing being featured** — product, app, skill, service. There must be
   exactly one, and it must be visually demonstrable in a few seconds.
4. **Volume + CTA posture** — how many scripts, and soft (URL on screen) or hard
   (comment keyword). Default: 10 scripts, soft CTA.

Make a working folder `./<creator-slug>/` with `samples/` for the reference clips.

If clips are local, `ffprobe` them for exact duration — the length spec must come
from measurement, not vibes:

```bash
ffprobe -v error -show_entries format=duration -of csv=p=0 samples/1.mp4
```

## Step 2 — Decode the references

Read `references/template-anatomy.md` and fill the decode table for **every**
reference clip, side by side. Columns are the beats; rows are the clips. You are
looking for the columns where the clips **agree** — agreement is the template,
disagreement is the variable.

Record for each clip: beat timings, what is on screen, overlay text verbatim,
whether there is a voiceover, audio type, and how the product is named.

Then write the **"three things that make this work"** list — the non-negotiables.
Be specific and physical ("you can see the keyboard and a little shake"), never
abstract ("it feels authentic"). Abstract notes cannot be shot.

State your confidence. If a reference is ambiguous, say which part and why.

## Step 3 — Find the seam

Name the one variable part and the one fixed part in a single sentence:

> "The **____** changes every video; the **____** stays the same."

Sanity-check it against the leverage test: **can the fixed part be filmed once
and cut into all N videos without anyone noticing?** If no, it is not fixed
enough — tighten it (lock the outfit, the location, the framing, the pan).

## Step 4 — Lane check

Open `references/creator-lanes.md`. Add a row for this creator and confirm the
new format does not collide with an existing one on **both** format and energy.
If it collides, change the energy (talking vs silent, hype vs deadpan,
teaching vs reacting) — not the payoff.

Say in one line why this format maps onto the thing being featured. If you can't,
the format is wrong for the product.

## Step 5 — Write TEMPLATE.md

Copy `templates/TEMPLATE.md` into the working folder and fill every section:

1. Decode table + the three non-negotiables (from Step 2)
2. Lane table (from Step 4)
3. Format spec — aspect, audio, length, beat count, CTA posture
4. Architecture diagram — the ASCII box showing variable vs fixed
5. The fixed beat, specified as a timed shot table so it can be filmed blind
6. Hook bank — read `references/hook-formulas.md`, pick the formula, then write
   15+ variants grouped by angle
7. Production checklist

## Step 6 — Generate SCRIPTS.md

Copy `templates/SCRIPTS.md` and render the hook bank into numbered scripts.

Each script is four lines, no more:

```
## B2 · ~10s · Reveal A
**HOOK (0–3s):** hand over mouth, looking away shy-giggle.
`[overlay: I could KISS the graphic designer who showed me this]`
→ **FIXED REVEAL A**.
```

Rules for this file:
- Numbered `B1, B2, B3…` so the team can say "shoot B4" in Slack.
- The fixed beat is written out **once**, at the top, and referenced by name
  after that. Never repeat it per script — repetition hides the leverage.
- Lead with the single best script, flagged (`⟵ send this one first`).
- Group by angle: hero variants → alt-reveal variants → experiments.
- End with a **shooting order** optimized for batching, not for script order:
  fixed beat first, then all hooks back-to-back, then stitch.

## Step 7 — Deliver

Hand back both files plus a two-line summary: the one rule, and which script to
shoot first. Do not summarize the whole template in chat — the document is the
deliverable.

---

## Adapting to other formats

The engine is not tied to silent reaction videos. The seam just moves:

| Format | Variable (swaps) | Fixed (film once) |
|---|---|---|
| Silent swoon-reaction | hook overlay | the reveal / payoff shot |
| Talking-head hack | the problem stated in line 1 | the demo + CTA outro |
| Listicle / "3 things" | the items | the intro framing + outro |
| Before/after | the "before" | the transition + after reveal |
| POV skit | the setup line | the punchline reaction |

Same seven steps. Only the decode table's beat names change.

---

## Failure modes to watch for

- **Two variables.** The scripts stop being batch-shootable and you have lost the
  entire point. Re-cut until there is one.
- **The fixed beat drifts.** If the reveal is re-shot per script "for variety,"
  you have built 15 individual videos, not a template.
- **Explaining.** Adding a clarifying line to a silent format is the #1 killer.
- **Hooks that are variations of wording, not angle.** Fifteen synonyms for the
  same sentence is a bank of one. Group by *angle* and force each group to earn
  its place.
- **Hard CTA on a discovery format.** If the format's premise is "someone let me
  in on a secret," a comment-keyword ask breaks the fiction. Keep it soft.
