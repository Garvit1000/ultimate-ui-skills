# Motion Audit And Repair

Use this reference for a broad animation audit, a motion-only critique, or a request to improve motion across an existing project. Use `emil-motion.md` for implementation values and `fluid-interfaces.md` for gesture behavior.

## Recon

Map the motion surface before judging it:

- Identify frameworks, motion libraries, CSS keyframes, view transitions, and gesture handlers.
- Find shared easing, duration, spring, and reduced-motion tokens.
- Note the product personality and existing conventions. Extend coherent local rules instead of creating a parallel system.
- Build a frequency map: constant or keyboard-driven, frequent, occasional, and rare.
- Search for `transition`, `animation`, `@keyframes`, `motion.`, `animate`, `useSpring`, `ease-in`, `transition: all`, `scale(0)`, `transform-origin`, and `prefers-reduced-motion`.

## Audit Categories

Review each confirmed issue against these categories:

1. Purpose and frequency: remove motion that lacks feedback, state, spatial, or explanatory value.
2. Easing and duration: keep repeated UI responsive and reserve longer timing for deliberate sequences.
3. Physicality and origin: make anchored UI originate from its trigger and avoid appearing from nothing.
4. Interruptibility: use transitions or springs for reversible and rapidly repeated interactions.
5. Performance: animate compositor-friendly properties and avoid broad transitions or render-loop state updates.
6. Accessibility: preserve useful feedback while reducing movement.
7. Cohesion: consolidate near-duplicate timing values and match the product personality.
8. Missed opportunities: identify a few jarring state changes or rare moments where motion would clarify behavior.

## Evidence And Priority

- Re-read every cited location before reporting it. Reject findings that are intentional, duplicated, exempt, or already handled by a local convention.
- Cite `file:line`, quote the relevant property or code, and describe the observable effect.
- Rank by leverage: user impact multiplied by frequency, divided by implementation effort.
- Use `High` for feel-breaking, accessibility, or performance failures; `Medium` for noticeable inconsistency; `Low` for optional polish.
- Report missing opportunities separately from defects. A short list of confirmed findings is better than a padded audit.

## Implementation Plan

When the user asks for a plan, make each item executable without conversation history:

- State the exact file paths and current behavior.
- Specify target properties, timing values, origins, tokens, and reduced-motion behavior.
- Name the local convention or exemplar to follow.
- Set boundaries: files not to touch, dependencies not to add, and behavior not to change.
- Include mechanical checks and a feel check.

For the feel check, test rapid interruption, keyboard activation, repeated use, reduced motion, and slow playback. Confirm that motion begins at the correct origin, can reverse without restarting, and never delays input.
