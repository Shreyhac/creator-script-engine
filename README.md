# Creator Script Engine

Turn reference clips into a reusable shot-list template and a whole bank of
ready-to-shoot short-form scripts.

It is packaged as a **Claude Code skill**, so running it is one sentence in
Claude rather than a meeting. The method underneath is one idea:

> **Isolate the one thing that changes. Freeze everything else. Then mass-produce.**

A short-form format that works is never a pile of unique videos. It is one fixed
payoff beat plus a swappable hook. Once you find that seam, a bank of 15 hooks
becomes 15 videos out of a single afternoon of filming — because the fixed beat
is shot **once** and cut into all of them.

---

## What you get out of a run

Two documents, deliberately kept separate:

| File | What it is | Who reads it |
|---|---|---|
| `TEMPLATE.md` | The **system** — decode, non-negotiables, format spec, hook bank | strategist / whoever briefs the creator |
| `SCRIPTS.md` | The **output** — numbered, four-line, ready-to-shoot scripts | the creator, on set, on their phone |

The template argues and explains *why*. The scripts are scannable and say *what
to do next*. Someone holding a phone on set will not read a rationale, which is
why these never get merged.

See [`examples/brenda/`](examples/brenda/) for a complete real run — 2 reference
clips in, 11 shootable scripts out, filmable in one afternoon.

---

## Using it

Drop the repo into your skills directory:

```bash
git clone <this-repo> ~/.claude/skills/creator-script-engine
```

Then in Claude Code:

```
Here are two reference clips from @creatorhandle — build me a template
and a script bank for <product>.
```

Claude reads `SKILL.md` and runs the seven steps. Or invoke it directly with
`/creator-script-engine`.

**It needs four things.** Claude will ask for whatever you leave out:

1. **Reference material** — 1–3 clips. Two is the sweet spot: one is a
   coincidence, two proves the pattern.
2. **The creator** — who's shooting, and their existing lane.
3. **The thing being featured** — one product, visually demonstrable in seconds.
4. **Volume + CTA posture** — how many scripts, soft or hard CTA.
   Default: 10 scripts, soft.

Working files land in `./<creator-slug>/` with the reference clips in `samples/`.

---

## How it works

| Step | What happens |
|---|---|
| 1. Intake | Gather references, creator, product, volume |
| 2. Decode | Beat-by-beat table of every reference, side by side, with stated confidence |
| 3. Find the seam | Name the one variable and the one fixed part |
| 4. Lane check | Confirm the format doesn't collide with another creator on the roster |
| 5. Write `TEMPLATE.md` | Format spec, architecture, fixed-beat shot table, hook bank |
| 6. Generate `SCRIPTS.md` | Numbered scripts + batch shooting order |
| 7. Deliver | Both files, plus which script to shoot first |

The load-bearing step is **2**. You don't get to write scripts before you can
state, in physical and observable terms, what makes the reference work.

---

## Repo layout

```
SKILL.md                        the process, as a runnable skill
references/
  template-anatomy.md           how to decode a reference clip
  hook-formulas.md              building a hook bank by angle, not wording
  creator-lanes.md              the shared roster — keep this updated
templates/
  TEMPLATE.md                   blank template doc
  SCRIPTS.md                    blank script bank
examples/brenda/                a complete worked run
```

---

## Team conventions

- **`references/creator-lanes.md` is shared state.** Claim a lane there *before*
  writing a template, so two people don't build the same format the same week.
  It's the file most likely to conflict — keep changes to it in their own commit.
- **One creator per run.** A template serving two creators serves neither.
- **Scripts are numbered** (`B1`, `B2`, …) so "shoot B4" is unambiguous in Slack.
- **Reference clips stay out of git** — other people's videos, and they bloat the
  repo. `.gitignore` covers `samples/` and common video extensions. The decode
  table captures everything the process needs from them anyway.
- **Refreshing a bank ≠ re-running the skill.** If hooks decay but the reveal
  still works, write new hooks inside the winning *angle* and reuse the footage.
  Only re-run the whole thing when the formula itself stops landing.

---

## It's not only for reaction videos

The seven steps don't change; only the seam moves.

| Format | Variable (swaps) | Fixed (film once) |
|---|---|---|
| Silent swoon-reaction | hook overlay | the reveal / payoff shot |
| Talking-head hack | the problem stated in line 1 | the demo + CTA outro |
| Listicle / "3 things" | the items | the intro framing + outro |
| Before/after | the "before" | the transition + after reveal |
| POV skit | the setup line | the punchline reaction |

---

## The five ways this dies

1. **Two variables.** The scripts stop being batch-shootable and the whole point
   is gone. Re-cut until there's one.
2. **The fixed beat drifts.** Re-shot per script "for variety" → you built 15
   individual videos, not a template.
3. **Explaining.** Adding a clarifying line to a silent format is the #1 killer.
4. **Hooks that vary wording, not angle.** Fifteen synonyms is a bank of one.
5. **Hard CTA on a discovery format.** If the premise is "someone let me in on a
   secret," a comment-keyword ask breaks the fiction.
