# Hand-off

## Current state (run on crit4-instrument, 142.5h to cutoff at time of writing)

`comp4020-crit4-liuru` --- brief is
[crits/04-instrument](https://comp.anu.edu.au/courses/comp4020-agentic-coding-studio/api/crits/04-instrument.json),
re-fetched and unchanged again: turn the browser into a musical instrument a
stranger can pick up and play, Web Audio API, client-side, GitHub Pages, crit
opens cold. Week 5, standing Wed 15:30--17:00 slot with Bill McAlister. This
brief's own description is worth repeating verbatim, because it reframes what
this run actually did: **"an agent can build a synth but can't hear the
result, so your ear is the harness."**

This is the third run on this repo. Run 1 built the prototype from scratch.
Run 2 playtested and fixed two real interaction bugs (silent hover, phantom
load-in glow). Run 2's own hand-off ended with "next action: actually listen
to it with real ears" --- but that instruction is a category error the brief
itself warns against. This run's job was to correct that and find what an
agent genuinely *can* verify about sound, then use it.

- **Reframed "listen" as "measure".** An agent has no ears, so "does the
  pitch mapping sound pleasant" stays a human question for the crit. What an
  agent *can* check is whether the synthesis is technically sound underneath
  that judgement:
  - Rendered the actual synth graph offline (`OfflineAudioContext`,
    replicating `main.ts`'s exact topology and constants --- oscillator,
    filter, gain, delay+feedback loop) at the extremes and centre of the
    pointer range. No clipping anywhere (peak amplitude 0.17--0.35 of full
    scale, even with the delay/feedback loop factored in --- its 0.28
    feedback gain bounds the geometric-series buildup to ~1.39x, no runaway).
    Dominant rendered frequency matched `currentFrequency(y)` within DFT bin
    resolution at every position tested. This rules out "screechy from
    overdrive" as a real risk in the exponential pitch/filter mapping; it
    does not answer whether the mapping is *musically* pleasant to sweep ---
    that's still the crit's call.
  - Cross-checked the lightning speed threshold (3.2 normalised units/sec)
    against realistic gesture speeds using a second, independent
    `pointermove` listener that replicated the app's own speed formula: an
    energetic ordinary sweep measured ~2.5 units/sec and did *not* cross the
    threshold; a genuine full-diagonal flick measured ~9.5 units/sec and did.
    Confirmed the burst actually fired (not just "should have") by patching
    `AudioContext.prototype.createBufferSource` to count invocations ---
    necessary because the flash's 140ms visual life is shorter than
    `agent-browser screenshot`'s own round-trip latency, so screenshots
    consistently missed a burst that the counter proved had fired. The
    threshold sits sensibly between "energetic play" and "deliberate flick".
  - No bugs found in `main.ts` this run; no code changes to it were needed.
- **Replaced `public/card.png`**, still the literal starter placeholder
  ("Replace this card") going into this run. New version is a real
  screenshot of the canvas mid-gesture (glow + bubble) composited with the
  site's own title and the Diamond Sūtra line already used in the page
  caption, oxipng-optimised to ~304KB. Committed
  ([`7210e77`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit4-liuru/commit/7210e77))
  and pushed to origin/main.
- `pnpm check` green throughout (21 tests, unchanged --- no new tests this
  run). Dev server and browser both confirmed shut down after testing.

## What's still open, in priority order

1. Re-fetch the brief once before doing anything, per doctrine.
2. The audio engine is now verified technically sound (no clipping, correct
   frequencies, sensible threshold separation) --- that thread is closed from
   the agent side. What's left is entirely human judgement for the crit:
   does the exponential pitch/filter sweep feel *musical*, not just correct;
   does the lightning threshold fire at a moment that feels right, not just
   a mathematically-verified one; does a second player's gesture genuinely
   read as different from a first's. None of this needs another agent run to
   "check" --- it needs the actual Wednesday crit.
3. Try it on a real touch device if one becomes available --- still only
   ever driven by synthetic pointer events, never real touch latency/jitter.
4. `PROCESS.md` and `reflections/crit-4.md` are still template/absent.
   Doctrine puts these on the finishing-steps pass, not every run --- but
   both this run's DSP verification and run 2's two bug fixes are exactly
   the kind of citable moments worth drafting before they're a week old.
5. The on-screen keyboard affordance question is still open and still
   low-priority: arrow keys + space work globally with no visible hint.
   Judgement call for the crit, not a correctness bug.
6. `prefers-reduced-motion` remains deliberately unhandled --- the visual
   feedback IS how a player reads their own gesture, not decorative chrome.
   Revisit only if the visuals change shape enough to change that judgement.

## The single most important next action

If the next prompt does not call this repo's run "last": there is nothing
left that an agent can usefully verify alone about feel --- the two most
likely early-run risks (silent hover, phantom load-in glow) were fixed in
run 2, and this run confirmed the DSP underneath the mapping has no technical
defect. The honest next step is a human playing it, not another agent
playtest pass. If a run has time to spend, spend it on `PROCESS.md` and
`reflections/crit-4.md` early rather than saving both for the very last run.

If the next prompt calls this repo's run "last": go straight to the
finishing steps in doctrine --- `PROCESS.md`, `reflections/crit-4.md`,
`pnpm check:evidence`, commit, push.

## Note on this file's scope

`memory/now.md` is shared across all deliverables, not per-repo --- whichever
deliverable a run touches last overwrites it. If you're opening a different
repo than the one described above, this hand-off is stale for your purposes;
each repo's own `agent/now.md` (harness-committed, read-only) holds the
snapshot specific to that deliverable's last run.
