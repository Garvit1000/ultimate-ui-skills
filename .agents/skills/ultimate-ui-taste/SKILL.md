---
name: ultimate-ui-taste
description: Research-backed UI, UX, and animation design-engineering skill for creating, reviewing, or improving high-taste interfaces in new or existing projects. Use when building or polishing landing pages, dashboards, SaaS/product screens, AI chat interfaces, component libraries, motion systems, interaction details, design-system rules, or when the user asks to make an interface feel premium, less generic, less AI-generated, more polished, more usable, or more like top-tier product design.
---

# Ultimate UI Taste

Use this skill to design, implement, or review interfaces with strong product context, precise interaction behavior, and disciplined animation taste.

## Operating Loop

1. Identify the lane: `brand`, `product`, `dashboard`, `docs`, `chat`, `editor`, `game`, or `component-library`.
2. Read the local app before making broad changes. Infer its framework, primitives, tokens, visual language, and constraints.
3. Calibrate taste before styling: product category, audience, brand tone, density, desired emotion, and what would feel inappropriate for this project.
4. Establish intent before styling: audience, primary workflow, first-screen hierarchy, expected frequency of use, and failure states.
5. Select references only when needed:
   - Context setup: `references/context.md`
   - Animation and motion: `references/animations/emil-motion.md`
   - Component choice and AI UI primitives: `references/ui/components.md`
   - Surfaces, typography, and visual detail: `references/ui/surfaces-typography.md`
   - Dashboards and AI/product screens: `references/ui/dashboards-ai.md`
   - UX states, accessibility, and resilience: `references/ux/states-accessibility.md`
   - AI slop detection: `references/anti-slop/generated-ui-tells.md`
   - Source examples from Nexus UI, Astryx, and Watermelon: `references/examples/component-libraries.md`
   - Pattern scoring and taste examples: `references/examples/pattern-rubric.md`
6. Build or review with evidence. Prefer existing project primitives and libraries over new abstractions.
7. Verify responsive layout, keyboard behavior, reduced motion, long content, empty/loading/error states, and visual hierarchy.

## Existing Project Review And Repair

Use this mode when improving an existing project, app route, dashboard, landing page, or component set.

1. Inspect the project before judging: routes, global CSS, design tokens, component primitives, icon and motion libraries, and existing conventions.
2. Identify the target screens and current failure modes. When possible, compare screenshots or browser output against source code.
3. Review before editing. List the highest-impact issues first: typography inconsistency, selector leakage, spacing rhythm, state coverage, hierarchy, accessibility, motion intent, and responsive risk.
4. Patch the smallest coherent area. Preserve the existing product language and system primitives instead of replacing the whole design.
5. Verify with lint, build, route checks, and visual inspection when available.
6. If a visible defect comes from CSS, check for broad selectors before changing markup. Decorative elements must use named classes or `data-slot`; never let generic `span`, `strong`, `small`, or `div` rules style semantic text by accident.
7. For broad redesigns or vague "make it better" requests, score the current UI with `references/examples/pattern-rubric.md` before editing. Fix the lowest scores first.

## Default Judgment

Treat taste as trained precision, not personal preference. Good UI is a chain of small correct decisions:

- The screen has a clear job.
- The first viewport reveals the product or workflow, not filler.
- Controls match familiar semantics.
- Motion explains cause and effect.
- Text, spacing, alignment, and state handling are resilient.
- Visual flourish never hides weak hierarchy or missing behavior.

Good taste is not one visual style. A banking dashboard, game lobby, AI chat, fashion landing page, devtool, healthcare form, and retro console site should not look the same. The shared standard is fitness: the interface should match its audience, material direction, workflow, risk level, and frequency of use.

## Hard Rules

- Do not create generic AI/SaaS slop: purple-blue gradients, decorative glass cards, gradient headings, nested cards, random glow, filler metric trios, icon-card grids, huge radii, or bouncy motion without reason.
- Do not make every project look like a named component library or inspiration source. Use references for principles, not aesthetic cloning.
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
- Keep spacing internally consistent, but not mechanical. Use a deliberate spacing scale, align related edges, and avoid adding divider lines when spacing and grouping are enough.
- Avoid broad descendant selectors for mixed content. Prefer named slots such as `.workflow-dot`, `.workflow-status`, `[data-slot="status"]`, and `[data-slot="icon"]` so decorative styles cannot leak into copy.

## Review Format

When reviewing or explaining changes, lead with concrete fixes. Use tables for before/after detail when multiple issues exist:

| Area | Before | After | Why |
| --- | --- | --- | --- |
| Motion | `transition: all 300ms ease-in` | `transition: opacity 160ms var(--ease-out), transform 160ms var(--ease-out)` | Faster, intentional, and avoids accidental layout animation |

Keep summaries short. Cite local files when possible.
