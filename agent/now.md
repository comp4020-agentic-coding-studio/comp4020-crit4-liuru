# Hand-off

## Current state (run on crit4-instrument, 118.5h to cutoff at time of writing)

`comp4020-crit4-liuru` --- brief is
[crits/04-instrument](https://comp.anu.edu.au/courses/comp4020-agentic-coding-studio/api/crits/04-instrument.json),
re-fetched and unchanged: turn the browser into a musical instrument a
stranger can pick up and play, Web Audio API, client-side, GitHub Pages, crit
opens cold. Week 5, standing Wed 15:30--17:00 slot with Bill McAlister.

This is the sixth run on this repo. Working tree was already clean and
matched run 5's hand-off exactly (same commits, `PROCESS.md` and
`reflections/crit-4.md` already drafted, `pnpm check` still 21/21 green).
Not called "last" by this prompt, so per doctrine this wasn't a
finishing-steps run. Third run in a row (4, 5, 6) to confirm the same thing:
there is nothing left for an agent to build, fix, or verify alone here until
the crit happens. Left the repo untouched rather than inventing busywork.

## What's still open, in priority order

1. Re-fetch the brief once before doing anything, per doctrine.
2. Nothing left for an agent to verify alone about feel or DSP --- closed in
   run 3, reconfirmed runs 4--6. The open question (does the mapping feel
   musical, does the lightning threshold land right, do two players sound
   different) is entirely the Wednesday crit's to answer.
3. Try it on a real touch device if one becomes available --- still only
   ever driven by synthetic pointer events.
4. `PROCESS.md` and `reflections/crit-4.md` are drafted, not absent --- but
   if the crit surfaces something concrete (a bug found live, a design
   choice explained differently than `PROCESS.md` currently states), the
   final run should still revise both rather than treat them as locked.
5. The on-screen keyboard affordance question is still open and
   low-priority: arrow keys + space work globally with no visible hint.
   Judgement call for the crit, not a correctness bug.
6. `prefers-reduced-motion` remains deliberately unhandled --- the visual
   feedback IS how a player reads their own gesture, not decorative chrome.
   Revisit only if the visuals change shape enough to change that judgement.

## The single most important next action

If the next prompt does not call this repo's run "last": there is genuinely
nothing left for an agent to build, fix, or verify alone here until the crit
happens. A run landing here with time to spend should treat that as real
information (confirmed three times now, across runs 4, 5 and 6), not a
prompt to invent busywork: skim for anything the crit itself surfaced, and
otherwise leave the repo as-is. If a run keeps landing here pre-crit with
nothing to do, that's expected --- don't escalate effort just because a run
happened to land during the dead time between "built" and "critted".

If the next prompt calls this repo's run "last": go straight to the
finishing steps in doctrine. `PROCESS.md` and `reflections/crit-4.md`
already exist and passed `check:evidence`, but re-read both against
whatever the actual crit revealed before treating them as done --- render
the site fresh in a browser end to end, confirm every page and link, shut
servers down, commit, push.

## Note on this file's scope

`memory/now.md` is shared across all deliverables, not per-repo --- whichever
deliverable a run touches last overwrites it. If you're opening a different
repo than the one described above, this hand-off is stale for your purposes;
each repo's own `agent/now.md` (harness-committed, read-only) holds the
snapshot specific to that deliverable's last run.
