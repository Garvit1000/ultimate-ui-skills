# Fluid Interfaces

Use this reference for gesture-driven UI: sheets, drawers, swipe cards, sliders, carousels, draggable panels, touch-heavy controls, translucent chrome, and Apple-like product motion.

The standard is direct manipulation. The interface should feel like it is under the user's hand, not like it is playing a canned animation.

## Core Rules

- Respond on pointer down, not only on click or release.
- During drag, move the object 1:1 with the pointer.
- Respect the grab offset. Do not snap the object center to the pointer.
- Capture the pointer so tracking continues outside the element bounds.
- Track recent position and time samples so release velocity is available.
- Never lock input while a gesture animation is running.
- Gesture-driven motion should be interruptible and reversible mid-flight.
- Start an interrupted animation from the current visible transform, not stale state.
- Hand release velocity into the settling animation so drag and settle have no visible seam.
- Choose snap targets from projected momentum, not only from release position.
- Use soft resistance at boundaries. A hard stop feels broken.

## Spring Defaults

Use springs for things the user can drag, flick, reverse, or interrupt.

| Interaction | Default |
| --- | --- |
| Ordinary reposition | Critically damped, no bounce |
| Sheet or drawer settle | Fast spring, slight bounce only if release carried momentum |
| Flick or throw | Momentum-aware spring with release velocity |
| Keyboard or high-frequency action | No movement animation |

Bounce must come from user energy. A menu that opens by click should not bounce just because the animation library can.

## Projection

For flickable UI, estimate where the object is going before choosing the snap point:

```text
projected_position = current_position + projected_distance_from_release_velocity
target = nearest_snap_point(projected_position)
settle_to(target, release_velocity)
```

Do not use projected motion for serious dashboard controls, dense tables, or keyboard workflows unless the interaction is truly drag-based.

## Spatial Consistency

- Enter and exit along the same path.
- A sheet dismissed downward should appear from that same edge.
- Popovers, menus, and sheets should visually originate from the trigger or edge that caused them.
- If an interaction is reversible, the return path should feel physically related to the departure path.
- Intermediate frames should hint at the destination, not just interpolate blindly.

## Boundaries

Use rubber-band style resistance when the user drags beyond an edge:

- Follow the pointer less as overshoot grows.
- Preserve continuity while communicating "there is no more content here."
- Snap back with release velocity when the gesture ends.

Avoid fake physics. If there is no draggable boundary, do not add rubber-banding as decoration.

## Translucent Materials

Use glass or blur only when it creates functional hierarchy.

- Floating chrome may be translucent when content moves beneath it.
- Larger surfaces need stronger separation than small chips.
- Do not stack light translucent surfaces on other light translucent surfaces.
- Prefer scroll-edge fades or masks where floating UI overlaps content, instead of reflexive hard dividers.
- Pair modal tasks with dimming. Use non-blocking panels without a full scrim when the background remains part of the workflow.
- Provide fallbacks for reduced transparency and high contrast.

## Accessibility

Reduced motion means a gentler equivalent, not missing feedback.

- For `prefers-reduced-motion`, replace slides, parallax, and elastic motion with short opacity or color transitions.
- For `prefers-reduced-transparency`, raise background opacity or remove blur.
- For `prefers-contrast`, use more solid surfaces and clearer borders.
- Avoid full-viewport moving backgrounds, slow looping motion, and abrupt brightness changes.

## Review Questions

1. Does feedback happen at the moment of input?
2. Can the user interrupt or reverse the motion?
3. Does drag motion track the pointer 1:1?
4. Does the release animation inherit velocity?
5. Is bounce earned by user momentum?
6. Do enter and exit paths preserve spatial logic?
7. Is translucency doing hierarchy work, or is it decoration?
8. Are reduced-motion, reduced-transparency, and high-contrast users handled?
