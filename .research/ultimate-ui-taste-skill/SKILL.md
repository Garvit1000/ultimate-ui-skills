---
name: ultimate-ui-taste
description: Research-backed UI, UX, and animation design-engineering skill for creating or reviewing high-taste interfaces. Use when building landing pages, dashboards, SaaS/product screens, AI chat interfaces, component libraries, motion systems, interaction details, design-system rules, or when the user asks to make an interface feel premium, less generic, less AI-generated, more polished, more usable, or more like top-tier product design.
---

# Ultimate UI Taste

Use this skill to design, implement, or review interfaces with strong product context, precise interaction behavior, and disciplined animation taste.

## Operating Loop

1. Identify the lane: `brand`, `product`, `dashboard`, `docs`, `chat`, `editor`, `game`, or `component-library`.
2. Read the local app before making broad changes. Infer its framework, primitives, tokens, visual language, and constraints.
3. Establish intent before styling: audience, primary workflow, first-screen hierarchy, expected frequency of use, and failure states.
4. Select references only when needed:
   - Context setup: `references/context.md`
   - Animation and motion: `references/animations/emil-motion.md`
   - Component choice and AI UI primitives: `references/ui/components.md`
   - Surfaces, typography, and visual detail: `references/ui/surfaces-typography.md`
   - Dashboards and AI/product screens: `references/ui/dashboards-ai.md`
   - UX states, accessibility, and resilience: `references/ux/states-accessibility.md`
   - AI slop detection: `references/anti-slop/generated-ui-tells.md`
   - Source examples from Nexus UI, Astryx, and Watermelon: `references/examples/component-libraries.md`
5. Build or review with evidence. Prefer existing project primitives and libraries over new abstractions.
6. Verify responsive layout, keyboard behavior, reduced motion, long content, empty/loading/error states, and visual hierarchy.

## Default Judgment

Treat taste as trained precision, not personal preference. Good UI is a chain of small correct decisions:

- The screen has a clear job.
- The first viewport reveals the product or workflow, not filler.
- Controls match familiar semantics.
- Motion explains cause and effect.
- Text, spacing, alignment, and state handling are resilient.
- Visual flourish never hides weak hierarchy or missing behavior.

## Hard Rules

- Do not create generic AI/SaaS slop: purple-blue gradients, decorative glass cards, gradient headings, nested cards, random glow, filler metric trios, icon-card grids, huge radii, or bouncy motion without reason.
- Do not use emojis or em dashes in UI copy, documentation, labels, or generated content unless the user explicitly asks for them. Use commas, periods, colons, parentheses, or a plain hyphen instead.
- Do not add decorative horizontal divider lines, background grids, or technical linework by reflex. Add a line only when it clarifies grouping, hierarchy, or measurement.
- Do not animate keyboard-initiated high-frequency actions.
- Do not use `transition: all`; specify exact properties.
- Do not animate layout properties for normal UI motion. Prefer `transform`, `opacity`, and sometimes `filter` or `clip-path`.
- Do not use `scale(0)` for UI entrance. Start near `scale(0.95)` with opacity.
- Use links for navigation and buttons for actions.
- Icon-only buttons require accessible names.
- Product dashboards should be dense, quiet, scannable, and stateful. Landing pages may be more expressive, but still need real product signal.
- Keep typography internally consistent. Metadata rows, labels, card titles, and small text should use the same font family, deliberate weights, and stable line-height.

## Review Format

When reviewing or explaining changes, lead with concrete fixes. Use tables for before/after detail when multiple issues exist:

| Area | Before | After | Why |
| --- | --- | --- | --- |
| Motion | `transition: all 300ms ease-in` | `transition: opacity 160ms var(--ease-out), transform 160ms var(--ease-out)` | Faster, intentional, and avoids accidental layout animation |

Keep summaries short. Cite local files when possible.
