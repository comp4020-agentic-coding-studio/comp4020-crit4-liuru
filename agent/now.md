# Hand-off

## Current state (run on crit4-instrument, 136.5h to cutoff at time of writing)

`comp4020-crit4-liuru` --- brief is
[crits/04-instrument](https://comp.anu.edu.au/courses/comp4020-agentic-coding-studio/api/crits/04-instrument.json),
re-fetched and unchanged: turn the browser into a musical instrument a
stranger can pick up and play, Web Audio API, client-side, GitHub Pages, crit
opens cold. Week 5, standing Wed 15:30--17:00 slot with Bill McAlister.

This is the fourth run on this repo. Run 1 built the prototype. Run 2
playtested and fixed two interaction bugs (silent hover, phantom load-in
glow). Run 3 replaced the placeholder card and verified the synth's DSP is
technically sound offline (no clipping, correct frequencies, sensible
threshold separation), closing what an agent alone can check about the sound.
This run had nothing left to build or verify from the agent side --- the
brief's own next step is the human crit, not another agent pass --- so it did
the one thing still genuinely useful this early: drafted the two
finishing-step documents ahead of the actual final run, while the citable
moments were still fresh.

- **`PROCESS.md`** now cites three real moments with resolving commit links:
  the one-mechanic design call
  ([`cacfe38`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit4-liuru/commit/cacfe38)),
  the silent-hover/phantom-glow bug fixes
  ([`b2a5e6d`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit4-liuru/commit/b2a5e6d)),
  and the "listen" → "measure" DSP-verification reframe, cited against the
  memory-tick commit that recorded it since no `main.ts` diff resulted
  ([`e867052`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit4-liuru/commit/e867052)).
- **`reflections/crit-4.md`** written, 300 words, both standing prompts
  answered: the breakthrough was naming "go listen to it" as a category
  error rather than repeating it, and finding what *is* verifiable
  underneath a human ear instead.
- `pnpm check:evidence` confirmed all three citations resolve and the
  reflection file is named correctly, before committing.
- `pnpm check` green (21 tests, unchanged). Committed
  ([`88a3b56`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit4-liuru/commit/88a3b56))
  and pushed to origin/main. Working tree clean.

## What's still open, in priority order

1. Re-fetch the brief once before doing anything, per doctrine.
2. Nothing left for an agent to verify alone about feel or DSP --- that
   thread closed in run 3. The open question (does the mapping feel musical,
   does the lightning threshold land right, do two players sound different)
   is entirely the Wednesday crit's to answer, not another agent pass.
3. Try it on a real touch device if one becomes available --- still only
   ever driven by synthetic pointer events.
4. `PROCESS.md` and `reflections/crit-4.md` are now drafted, not absent ---
   but if the crit surfaces something concrete (a bug found live, a design
   choice explained differently than PROCESS.md currently states), the final
   run should still revise both rather than treat them as locked. The
   finishing-steps pass is where they get their last read-through, not
   necessarily their first draft.
5. The on-screen keyboard affordance question is still open and low-priority:
   arrow keys + space work globally with no visible hint. Judgement call for
   the crit, not a correctness bug.
6. `prefers-reduced-motion` remains deliberately unhandled --- the visual
   feedback IS how a player reads their own gesture, not decorative chrome.
   Revisit only if the visuals change shape enough to change that judgement.

## The single most important next action

If the next prompt does not call this repo's run "last": there is genuinely
nothing left for an agent to build, fix, or verify alone here until the crit
happens --- both docs are drafted, both bug classes from run 2 are fixed, and
the DSP is verified. A run landing here with time to spend should treat that
as real information, not a prompt to invent busywork: skim for anything the
crit itself surfaced (check for new commits/notes if this is genuinely a
later week), and otherwise leave the repo as-is rather than churning it.

If the next prompt calls this repo's run "last": go straight to the finishing
steps in doctrine. `PROCESS.md` and `reflections/crit-4.md` already exist and
passed `check:evidence`, but re-read both against whatever the actual crit
revealed before treating them as done --- render the site fresh in a browser
end to end, confirm every page and link, shut servers down, commit, push.

## Note on this file's scope

`memory/now.md` is shared across all deliverables, not per-repo --- whichever
deliverable a run touches last overwrites it. If you're opening a different
repo than the one described above, this hand-off is stale for your purposes;
each repo's own `agent/now.md` (harness-committed, read-only) holds the
snapshot specific to that deliverable's last run.
