# COMP4020 prototype

Your starter repo for a COMP4020 prototype: a static site in HTML/CSS/TypeScript
that builds to plain HTML/CSS/JS and deploys to GitHub Pages. The deployed site
is what gets marked, not this repo.

The
[course website](https://comp.anu.edu.au/courses/comp4020-agentic-coding-studio/)
publishes this deliverable's brief and spec, and this repo's name tells you
which deliverable applies. Read both before you plan or build.

## How to work in here

- Keep the dev server running (`pnpm dev`) so you see changes as you make them.
- Run `pnpm check` before you push.
- Open the page in a browser and look at it. The rendered page is the truth;
  your mental model of it isn't.
- When a check fails, read its output before you change anything.
- Never commit a red state.

## The link-preview card

`public/card.png` (1200x630) is the image a shared link shows; `index.html`'s
head points at it. Replace it and the `description` meta, and copy the head
block into any new page. The card URL resolves against the page that names it,
like any link --- `./card.png` is wrong one directory down, and nothing in CI
checks it, so look at the deployed head when you add pages.

## The checks

`pnpm check` runs them (`pnpm check:evidence` is the extra gate before you
ship); CI runs the same plus links, secrets and the deploy. Read the failure.

`spec/README.md`, `PROCESS.md` and `reflections/README.md` are in this repo and
say what they are for.

## One mechanic, not six toys

The instrument is one mechanic: a single point in 2D space (from the pointer,
touch, or the arrow keys) drives everything --- its position sets pitch and
filter, staying still lets the tone decay, a tap or the space bar plucks, and
moving fast triggers a noise burst. The six-as-ifs (dream, illusion, bubble,
shadow, dew, lightning) are the vocabulary for what those signals sound and
look like, not six separate widgets bolted together. Before adding a new
"mode" or "voice", check whether it can be a new response to the existing
point-and-gesture signal instead --- assignment-1 already paid for learning
this the hard way (six standalone toys instead of one coherent thing).

`spec/instrument.test.ts` asserts the built page ships no `<audio>`/`<video>`
element and that the bundled script references `AudioContext` --- the
mechanical half of "sound is made live in the page, not played back". It
can't test whether the thing is actually fun or discoverable; that's the crit.

## This file is yours

A starting point, not a rulebook. As you learn what your prototype needs --- a
convention the work has to hold to, a sensor that keeps catching you out (a
linter, say), a fact about the stack that is easy to get wrong --- write it down
here and wire it into `check`. Growing this file is the work.
