# Hand-off

## Current state (run on crit4-instrument, 160.5h to cutoff at time of writing)

`comp4020-crit4-liuru` --- brief is
[crits/04-instrument](https://comp.anu.edu.au/courses/comp4020-agentic-coding-studio/api/crits/04-instrument.json),
re-fetched and unchanged from the previous run's read: turn the browser into a
musical instrument a stranger can pick up and play, Web Audio API,
client-side, GitHub Pages, crit opens cold (pod plays it before anyone
talks). Week 5, standing Wed 15:30--17:00 slot with Bill McAlister.

This is the second run on this repo. The first run built the whole
prototype from scratch (one point in space drives pitch/filter/pluck/noise
via the bubble/dew/lightning vocabulary --- see `reflections`-style detail in
the previous hand-off, now superseded by this one). This run's job, per its
own hand-off, was: **play-test harder, then deepen** --- not add scope.

- **Playtested for real**, not just screenshotted: ran `pnpm dev`, drove it
  with `agent-browser mouse move/down/up` and `press`, at both 1280x800 and
  390x844 viewports. Found two real bugs, both about the gap between "looks
  right in a screenshot" and "responds right to an uninstructed stranger":
  1. **Mouse hover before the first click did nothing** --- marker didn't
     move, no visual response at all --- because `pointermove` was gated
     behind `if (!audio) return;`, so the exact "theremin driven by the
     mouse" case the brief's own opening line describes was silent. Fixed by
     dropping that guard; pointer tracking (and thus the visual "presence"
     glow) now runs from the very first hover, sound still waits for the
     click/tap that a user gesture needs to unlock `AudioContext`.
  2. **Every fresh page load silently swelled to near-full brightness for a
     few seconds before fading to the calm idle look**, because `lastMoveAt`
     defaulted to `0`: the first ~150ms of frames read `now - 0` as "just
     moved", ramping "presence" up before decaying it back down over the
     idle tau. Fixed by initialising `lastMoveAt = -Infinity`.
  - Both fixes verified by screenshot: idle-immediately-after-load now stays
    small/dim (previously bright), and a bare hover (no prior click) now
    visibly tracks the cursor. Lightning-on-fast-movement and dew-decay
    (presence fading over ~3s of stillness) both re-verified working after
    the fixes. Space-bar pluck re-verified working. Full detail (and the
    generalisable lessons --- don't gate visual state behind an audio-exists
    check; initialise "time since last event" timestamps to `-Infinity` not
    `0`) is in `MEMORY.md`'s process notes.
  - `pnpm check` green (typecheck, build, 21 vitest tests, unchanged count ---
    no new tests added this run, this was a playtest-and-fix pass not a
    feature pass). Committed
    ([`b2a5e6d`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit4-liuru/commit/b2a5e6d))
    and pushed to origin/main.
  - Dev server and browser both confirmed shut down after testing.

## What's still open, in priority order

1. Re-fetch the brief once before doing anything, per doctrine.
2. **Deepen the feel further, now that the "silent hover" and "phantom load
   swell" bugs are out of the way** --- those were the two things most likely
   to make a cold crit's very first few seconds go wrong, but the mechanic
   itself is still only lightly tuned:
   - Is the pitch/filter mapping (exponential frequency by y, exponential
     cutoff by x) actually pleasant to sweep, or twitchy/screechy at the
     extremes? Only ever eyeballed via screenshots and synthetic pointer
     jumps so far, never listened to with real ears.
   - Does the lightning-speed threshold (3.2 normalised units/sec) fire at
     a musically sensible moment, or too eagerly/rarely? Confirmed it fires
     at all, not that the threshold feels right.
   - Does a second player's gesture genuinely sound different from a
     first's (the spec's "two players sound different" bar)? Nothing about
     the current mechanic depends on identity, only current position/speed
     --- worth thinking about whether that bar is met by "different people
     move differently" alone, or whether it wants more.
3. Try it on an actual touch device if one becomes available, not just
   synthetic `agent-browser` pointer events --- touch's own pointerdown-
   before-pointermove ordering means it was never at risk from bug #1 above,
   but real touch latency/jitter is still unverified.
4. `public/card.png` is still the template placeholder --- needs a real
   1200x630 image before shipping; still not urgent, but the week is
   halfway through its 168h now.
5. `PROCESS.md` and `reflections/crit-4.md` are still template/absent.
   Doctrine puts these on the finishing-steps pass (the run the prompt
   calls "last"), not every run --- but worth drafting once the mechanic
   feels settled rather than leaving both for that very last run, since this
   run's two bug fixes are exactly the kind of "moment that mattered" worth
   a `PROCESS.md` citation later.
6. The on-screen keyboard affordance question from the previous hand-off is
   still open and still low-priority: arrow keys + space have no visible
   hint, though they do work globally (the `keydown` listener is on
   `window`, not the canvas, so no focus/tabindex dance is needed). Pointer/
   touch is the primary, sufficiently-discoverable path; whether keyboard
   needs its own visible affordance is a judgement call for the crit, not a
   correctness bug.
7. `prefers-reduced-motion` remains deliberately unhandled --- the visual
   feedback (glow, bubbles, lightning) IS how a player reads what their own
   gesture just did, so snapping it to instant would remove content, not
   just chrome. Revisit only if the visuals change shape enough to change
   that judgement.

## The single most important next action

Re-open this repo, reread this file, re-fetch the crits/04-instrument brief
to confirm it's unchanged, then actually *listen* to the instrument for a
few minutes with real playback (not just screenshot the visuals, which is
all this run did) --- decide whether the pitch/filter mapping and the
lightning threshold feel musical, not just functional, before treating the
mechanic as settled. The two bugs fixed this run were both about the first
few seconds of an uninstructed stranger's experience; the next layer of
"deepen" is about whether the instrument stays satisfying past those first
few seconds.

## Note on this file's scope

`memory/now.md` is shared across all deliverables, not per-repo --- whichever
deliverable a run touches last overwrites it. If you're opening a different
repo than the one described above, this hand-off is stale for your purposes;
each repo's own `agent/now.md` (harness-committed, read-only) holds the
snapshot specific to that deliverable's last run.
