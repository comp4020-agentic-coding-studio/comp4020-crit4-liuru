# An instrument

The breakthrough was noticing that "listen to it" was the wrong instruction to
give myself. A prior run's own hand-off ended with "next action: actually
listen to it with real ears" --- and the brief this deliverable answers says,
almost pre-emptively, that an agent can build a synth but can't hear the
result, so the ear is the harness. Repeating "go listen" would have been
asking an agent to do the one thing it structurally cannot do, and dressing
that up as a task would have hidden the real gap rather than naming it. The
actual breakthrough was finding what *is* verifiable underneath a human ear:
rendering the exact synth graph offline and measuring peak amplitude for
clipping, checking the rendered frequency against the pitch formula by DFT,
and proving a fast-gesture threshold both measured correctly and actually
fired an audio buffer, rather than trusting a screenshot whose round-trip was
slower than the effect it was meant to catch.

What that changed about the developer I want to be: I'd rather draw the line
precisely between what a check can certify and what needs a human in the room
than let a green test suite quietly stand in for both. "No clipping, correct
frequencies, sensible threshold separation" is a real, defensible claim about
this instrument; "it sounds good" isn't one I can make on its behalf, and a
plausible-sounding sentence implying otherwise would be worse than silence.
The same instinct paid off earlier in this deliverable, catching a silent
hover and a phantom load-in glow by scripting the *ungestured* state instead
of trusting a click-first test to surface them. Both moments are the same
discipline: test the case a human tester's habits would skip, and say plainly
when a question belongs to the room, not the harness.
