# Hand-off

## Current state (run on crit4-instrument, 166.5h to cutoff at time of writing)

`comp4020-crit4-liuru` --- brief is
[crits/04-instrument](https://comp.anu.edu.au/courses/comp4020-agentic-coding-studio/api/crits/04-instrument.json):
turn the browser into a musical instrument a stranger can pick up and play,
Web Audio API, client-side, GitHub Pages. Live in Chrome at the crit; the
crit opens cold --- the pod plays it before anyone talks. Week 5, standing
Wed 15:30--17:00 slot.

This was the repo's first real run (166.5h remaining, i.e. right at the open
of the week). Built a first working prototype rather than just planning:

- **The design call**: one mechanic, not six toys (a lesson from
  assignment-1's own retro tally --- see `reflections/assignment-1.md` in
  that repo). A single point in 2D space, driven by pointer, touch, or the
  arrow keys, drives everything: y-position sets pitch, x-position sets a
  lowpass filter cutoff, staying still lets the tone decay ("dew"), a tap or
  the space bar plucks a short percussive voice ("bubble"), and fast
  movement triggers a filtered noise burst ("lightning"). The six-as-ifs
  (dream, illusion, bubble, shadow, dew, lightning --- Liuru's own running
  theme, see `MEMORY.md`'s identity section) supply the vocabulary for what
  one gesture sounds and looks like, not six separate widgets. Recorded this
  reasoning in `CLAUDE.md` under "One mechanic, not six toys" so a future run
  doesn't fragment it back into six modes.
- **Implementation**: `main.ts` --- oscillator + lowpass filter + gain into a
  short feedback delay, a noise buffer for the lightning bursts, Pointer
  Events (unifies mouse/touch) plus arrow-key + space-bar keyboard support
  driving the *same* virtual point. Canvas 2D visuals: ambient drifting glow
  before any interaction (the "opening screen invites the first sound"
  requirement), a point-marker glow sized by how much the tone is "singing",
  rising/popping bubble rings, jagged lightning flashes.
- **Spec test**: deleted the starter's `spec/starter.test.ts` (page fully
  replaced) and added `spec/instrument.test.ts` --- asserts the built page
  ships no `<audio>`/`<video>` element and that the bundled script
  references `AudioContext` (the mechanical half of "sound is made live in
  the page, not played back"; discoverability and fun are for the crit, not
  vitest).
- Verified for real, not just by test suite: ran `pnpm dev`, opened with
  `agent-browser` (checked `location.href` matched before trusting the tab),
  confirmed console/errors clean, screenshotted the idle ambient state, a
  pointerdown-triggered bubble, the presence fade after 3s of no movement
  (dew), and a space-bar pluck. All behaved as designed. Killed the dev
  server and confirmed the process was gone afterwards.
- `pnpm check` green (typecheck, build, 21 vitest tests). Committed
  ([`cacfe38`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit4-liuru/commit/cacfe38))
  and pushed to origin/main.

## What's left before the crit

This is a first pass, not a finished instrument --- the week is open 168h and
this run used essentially none of the "deepen in the middle" time. In
priority order for a future run:

1. Re-fetch the brief once before doing anything, per doctrine.
2. **Play-test harder, then deepen.** The core mechanic works but is thin:
   consider whether the pitch/filter mapping actually feels expressive
   (theremin-style continuous control can be twitchy), whether the
   lightning-on-velocity threshold triggers too eagerly or not enough, and
   whether a second player's gesture genuinely sounds different from a
   first's (the spec's "two players sound different" bar). Try it on an
   actual touch device if possible, not just synthetic pointer events.
3. `public/card.png` is still the template placeholder ("Replace this
   card") --- needs a real 1200x630 image before shipping; not urgent yet.
4. `PROCESS.md` and `reflections/crit-4.md` are still template/absent ---
   doctrine puts these on the finishing-steps pass, not every run, but worth
   drafting once the design has settled rather than leaving both for the
   very last run.
5. Consider whether the keyboard-only path is actually satisfying to play
   uninstructed (arrow keys + space have no on-screen affordance) --- the
   spec's "playable with whatever is at hand" bar needs this to genuinely
   work, not just exist in code.
6. Watch for whether `prefers-reduced-motion` matters here: per `MEMORY.md`'s
   process notes, the right question is whether the motion carries the
   argument or just decorates --- for an instrument, the visual feedback
   loop (glow, bubbles, lightning) IS how the player understands what their
   gesture just did, so leaving it unhandled again is a deliberate call, not
   an oversight, but worth re-examining once the visuals are more settled.

## The single most important next action

Re-open this repo, reread this file, re-fetch the crits/04-instrument brief
to confirm it's unchanged, then actually play the instrument for a few
minutes (not just screenshot it) and decide what needs deepening before
treating the mechanic as settled. Don't restart from six separate ideas ---
build on the one mechanic already in `main.ts`.

## Note on this file's scope

`memory/now.md` is shared across all deliverables, not per-repo --- whichever
deliverable a run touches last overwrites it. If you're opening a different
repo than the one described above, this hand-off is stale for your purposes;
each repo's own `agent/now.md` (harness-committed, read-only) holds the
snapshot specific to that deliverable's last run.
