# Process overview

A reading-guide to how the work came together --- a map to your process, not an
essay about it. Markers read this file and follow its citations; they don't
trawl the repo for evidence you didn't point at, so if a moment mattered, cite
it.

## What I built

An instrument driven by one mechanic: a single point in 2D space --- pointer,
touch, or the arrow keys --- sets an oscillator's pitch and a filter's cutoff,
decays to a resting drone (dew) when it stops moving, plucks a bubble on a tap
or the space bar, and cracks like lightning when it moves fast enough. The
six-as-ifs (dream, illusion, bubble, shadow, dew, lightning) name what
different derived properties of that one signal sound and look like, rather
than being six separate voices bolted together.

## The moments that mattered

1. **One mechanic, not six toys.** The obvious reading of "dream, illusion,
   bubble, shadow, dew, lightning" is six widgets, one per simile ---
   assignment-1 already built that shape once and it read as six disconnected
   toys, not one instrument. Instead of six voices I built one continuous
   signal (pointer position + velocity) and mapped each simile to a different
   derived property of it: stillness is dew, a tap is a bubble, speed past a
   threshold is lightning. I knew it held together because
   `spec/instrument.test.ts` asserts the mechanical half --- no `<audio>`
   element, `AudioContext` present, one playing surface, no score or fail
   state --- and because playtesting the built page showed a single gesture
   driving every voice, not a menu of separate ones
   ([`cacfe38`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit4-liuru/commit/cacfe38)).

2. **A silent hover is the exact failure the brief warns about.** Playtesting
   the first build found the pointer marker did nothing until the first click
   --- the audio-unlock gate on `pointermove` was also gating the *visual*
   position tracking, so hovering before ever clicking (the natural first
   move for "a theremin driven by the mouse", the brief's own opening example)
   produced zero feedback. The obvious fix would have been to just unlock
   audio earlier; instead I split the gate so pointer tracking runs
   unconditionally and only the `AudioContext.resume()` stays behind a user
   gesture, matching the autoplay policy the brief itself cites. The same pass
   also caught a `lastMoveAt` initialised to `0` rather than `-Infinity`,
   which made every fresh page load read as "just moved" and swell to near-
   full brightness before decaying --- a phantom glow with no gesture behind
   it. I confirmed both by scripting `agent-browser` to move the pointer
   *before* any click and screenshotting within the first couple of seconds of
   a real navigation, since by the time a human looks the decay has already
   settled
   ([`b2a5e6d`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit4-liuru/commit/b2a5e6d)).

3. **Reframing "listen to it" as "measure it".** A later run's own hand-off
   ended with "next action: actually listen to it with real ears" --- a
   category error, since an agent has no ears and the brief says so directly
   ("an agent can build a synth but can't hear the result, so your ear is the
   harness"). Rather than repeating that instruction, the next run asked what
   an agent genuinely *can* verify about sound underneath a human's musical
   judgement: it rebuilt `main.ts`'s exact synth graph in an
   `OfflineAudioContext` and rendered it at the extremes and centre of the
   pointer range, checking for clipping and confirming the dominant rendered
   frequency matched `currentFrequency(y)`; and it cross-checked the lightning
   speed threshold against realistic gesture speeds with an independent
   `pointermove` listener, then proved the burst actually fired (not just
   "should have") by counting real `AudioContext.prototype.createBufferSource`
   calls, since the flash's 140ms visual life is shorter than a screenshot
   round-trip. No clipping and no bugs turned up, so `main.ts` didn't change ---
   the artefact of that run is the record of what was checked and why it
   stopped there, not a diff
   ([`e867052`](https://github.com/comp4020-agentic-coding-studio/comp4020-crit4-liuru/commit/e867052)).

## Before you ship

`pnpm check:evidence` verifies your citations resolve to real commits, that a
reflection entry the marker reads is in `reflections/`, and that your
`CLAUDE.md` is there --- before a marker ever opens the file. It checks that
your map is traceable, not that it is good: the marker judges whether your
small, deliberately chosen set of moments shows real judgement and reflection. A
green check is not a substitute for that curation.

Images aren't checked: whether one renders is visible the moment you look. Open
this file on GitHub and look at it before you ship.
