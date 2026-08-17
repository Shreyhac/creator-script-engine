# Template Anatomy — how to decode a reference clip

The job in this stage is forensic, not creative. You are reverse-engineering a
format that already works. Everything you invent later is constrained by what you
find here, so do not skip ahead.

---

## 1. The decode table

Build one table per creator, with **one column per reference clip**. Rows are the
beats. Fill it in verbatim — quote the overlay text exactly as burned, including
capitalization and emoji.

| Beat | Sample 1 | Sample 2 |
|---|---|---|
| **0–Xs — [beat name]** | what is physically on screen; overlay text verbatim | same |
| **Xs → end — [beat name]** | what is physically on screen | same |
| Length | measured, in seconds | measured |
| Voice | VO / none | VO / none |
| Audio | trending sound / original / music bed | |
| How the product is named | on-screen URL / spoken / caption / never | |
| CTA | none / soft / hard keyword | |

**Read the columns where the clips agree.** That agreement is the template. The
one row where they differ is your variable.

If a row is ambiguous (muffled audio, cropped overlay), write `unclear` rather
than filling it in with a plausible guess. A wrong "fact" here propagates into
every script you write.

---

## 2. Measure, don't estimate

Length is the spec people break first. Get it from the file:

```bash
ffprobe -v error -show_entries format=duration -of csv=p=0 samples/1.mp4
```

Beat boundaries: step through the cut and note the timestamp of every hard cut.
The number of hard cuts is the number of beats. Most working short-form formats
have **two**. Three is already a stretch. If your decode has five beats, you are
describing a video, not a template.

---

## 3. The three non-negotiables

After the table, write exactly three bullets: **the things that, if broken, kill
the format.** Three is the right number — one is lazy, six is a wish list.

Each must be:
- **Physical and observable** — "you can see the keyboard, the ceiling, and a
  little handheld shake," not "it feels authentic."
- **Falsifiable** — someone could look at a rough cut and say yes or no.
- **Explained** — one clause on *why* it works, so the team can make the right
  call in a situation you didn't anticipate.

Bad: *"Keep it real and relatable."*
Good: *"The reveal is deliberately NOT a clean screen recording — keyboard and
room in frame, slight shake. That's what sells 'a real person just found this.'
A polished screen-cap kills it."*

---

## 4. Common non-negotiable categories

Most working formats have one from each of these. Use as a checklist against
your decode:

- **A withholding rule** — something deliberately NOT said or shown. (Silence.
  No voiceover. Product name never spoken.) This is usually the hardest one for
  a team to hold onto and the first one to erode.
- **A texture rule** — the deliberate roughness that signals "not an ad."
  Handheld, phone-films-screen, unlit room, one take.
- **A payoff rule** — how the product actually lands. On-screen URL, a wall of
  results, a number, a before/after. Almost never a logo card.

---

## 5. Confidence

End the decode with a stated confidence and what would raise it:

> *Decoded at ~95%. Both clips are the same template with no meaningful
> divergence. Remaining 5%: the trending audio on sample 2 is unidentified, so
> the exact comedic timing of the giggle beat is inferred from the visual, not
> the sound.*

Confidence below ~70% means **get more references before writing scripts.**

---

## 6. Beat naming

Name beats by function, not by content — function is what transfers to the next
script, content is what changes.

| Good (function) | Bad (content) |
|---|---|
| HOOK | "girl giggling" |
| REVEAL | "laptop with logos" |
| PROOF | "the price tag" |
| PUNCH | "she yells" |

The names you choose here become the vocabulary in `SCRIPTS.md`, so the creator
will read them on set. Make them short and unambiguous.

---

## 7. The leverage test

Before you leave this stage, answer out loud:

> **Can the fixed beat be filmed once and cut into all N scripts without anyone
> noticing it is the same footage?**

- **Yes** → the seam is real. Proceed.
- **Almost** → tighten the constraints (lock outfit, framing, location, the exact
  pan) until it is yes.
- **No** → you have found the wrong seam. Go back to the decode table and look
  for a row you assumed was fixed but actually varies.

This one question is the difference between a template and a mood board.
