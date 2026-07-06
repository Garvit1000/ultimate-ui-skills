# Design System Packet

Use this reference when a project needs a new visual direction, a broad redesign, a landing page, a dashboard, or a vague "make it better" request.

The packet is a short reasoning artifact. It should guide design decisions before implementation. It is not a theme preset, palette dump, or font-pairing catalog.

## When To Create A Packet

Create a design system packet before editing when:

- The user asks for a new page, major redesign, or premium polish.
- The project lacks an obvious brand or product direction.
- The current UI feels generic, AI-generated, or copied from a component library.
- Multiple visual directions could be valid.
- The work touches typography, color, layout density, motion, and component behavior together.

Skip the packet for small bug fixes, single-component repairs, copy edits, or narrow accessibility fixes.

## Packet Template

Keep the packet compact. Fill only what helps the current task.

```yaml
design_system_packet:
  work_mode:
  product_type:
  audience:
  primary_workflow:
  frequency_of_use:
  risk_level:
  desired_feeling:
  structure:
    first_viewport:
    sections:
    primary_action:
    proof_or_feedback:
    product_archetypes:
  taste_direction:
    visual_material:
    density:
    typography_mood:
    color_roles:
    motion_character:
  component_behavior:
    navigation:
    controls:
    data_display:
    empty_loading_error:
  anti_patterns:
  delivery_checks:
```

## Decision Rules

Use product context to shape the packet:

| Product context | Direction that usually fits | Direction to question |
| --- | --- | --- |
| Finance, insurance, legal | Calm, dense, trustworthy, restrained motion, clear tables | Playful bounce, neon color, vague hero claims |
| Healthcare, education, public service | Clear, reassuring, accessible, plain language, strong state handling | Experimental navigation, low contrast, decorative motion |
| Developer tools and operations | Compact, keyboard-friendly, fast, precise labels, visible system state | Marketing-style feature cards that hide the workflow |
| Creative, fashion, music, culture | Editorial, expressive, image-led, distinctive rhythm | Generic SaaS grids, default gray cards, weak art direction |
| Games and playful tools | Tactile, characterful, vivid, responsive feedback | Plain enterprise dashboard styling |
| AI agent products | Transparent state, tool feedback, citations or evidence, interruptible actions | Chat bubbles only, no tool state, no recovery path |

These are starting points, not laws. A product can intentionally break its category if the brand, audience, and workflow justify it.

## Example

```yaml
design_system_packet:
  product_type: finance operations dashboard
  audience: analysts reviewing daily exceptions
  primary_workflow: scan exceptions, compare risk, open a case, resolve or escalate
  frequency_of_use: many times per day
  risk_level: high
  desired_feeling: calm control, speed, trust
  structure:
    first_viewport: filters, status summary, exception table, current risk trend
    sections: summary strip, queue, detail drawer, audit trail
    primary_action: open selected case
    proof_or_feedback: last refresh time, source coverage, resolution state
    product_archetypes: exception queue, sortable table, audit trail, risk trend
  taste_direction:
    visual_material: quiet operational system, not marketing page
    density: high but scannable
    typography_mood: plain system text, tabular numbers, restrained weights
    color_roles: neutral base, one primary action, semantic risk colors only
    motion_character: minimal, instant for keyboard actions, subtle for drawers
  component_behavior:
    navigation: persistent app shell with active route
    controls: buttons for actions, links for navigation, segmented controls for modes
    data_display: sortable table with loading, empty, error, and long-content states
    empty_loading_error: explicit recovery path and source status
  anti_patterns:
    - decorative gradients
    - bouncy card animations
    - filler metrics without denominators
    - hidden keyboard focus
  delivery_checks:
    - contrast meets WCAG AA for text and controls
    - focus states are visible
    - reduced motion is respected
    - table works at mobile and desktop widths
    - long labels and empty states are handled
```

## How To Use It

1. Draft the packet before choosing colors, fonts, animation, or layout decoration.
2. Compare the current UI to the packet.
3. Name the biggest mismatches.
4. If the concept is wrong, replace the surface archetype before polishing style.
5. Patch the smallest coherent area that moves the UI toward the packet.
6. Re-check the packet after implementation. If the product context changed, revise the packet instead of forcing the original direction.

## What Not To Do

- Do not output a large style encyclopedia.
- Do not pick a named aesthetic because it sounds premium.
- Do not assign palettes or font pairings without explaining their role.
- Do not invent fake live data, fake status, or fake operational details to make the packet feel specific.
- Do not use the same preview/card archetype for every product proof unless every proof has the same job.
- Do not let the packet replace real UI verification.
- Do not apply category rules mechanically when the product has a clear reason to differ.
