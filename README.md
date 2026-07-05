# Ultimate UI Taste

Ultimate UI Taste is an agent instruction pack for reviewing, designing, and improving high-taste user interfaces. It focuses on product intent, visual hierarchy, typography, motion, component semantics, accessibility, state coverage, and implementation resilience.

It is built to improve both new and existing projects. It does not force one visual style. Instead, it calibrates the right taste direction for each product, then applies durable UI, UX, and animation principles.

## What It Helps With

- Landing pages and product websites
- SaaS dashboards and operational tools
- AI chat and agent interfaces
- Component libraries and preview systems
- Motion systems, transitions, drawers, popovers, and icon states
- Existing project audits and design repair
- Detecting generic AI-generated UI patterns

## Repository Structure

The instruction pack lives here:

```text
.agents/skills/ultimate-ui-taste/
  SKILL.md
  references/
    animations/
    anti-slop/
    examples/
    ui/
    ux/
```

`SKILL.md` is the main instruction file. The `references` folder contains focused guidance for motion, typography, dashboard design, AI interfaces, state coverage, component-library patterns, and design audits.

## Use With Any Agent

Point your agent at the instruction pack and give it this prompt:

```text
Read .agents/skills/ultimate-ui-taste/SKILL.md first. Follow its operating loop. Load files from references/ only when relevant to the task.
```

For a dashboard:

```text
Use the Ultimate UI Taste instructions to improve this dashboard. Keep the existing product language, but fix hierarchy, spacing, typography, motion, accessibility, and empty states.
```

For a landing page:

```text
Use the Ultimate UI Taste instructions to redesign this landing page. First calibrate the taste direction for the product, then critique the current page before editing.
```

For an existing app:

```text
Use the Ultimate UI Taste instructions to audit the current UI. Identify what looks generic or AI-generated, explain the highest-impact issues, then patch the smallest coherent area.
```

## Recommended Workflow

1. Ask for review before fixes.
2. Let the agent inspect the codebase, routes, global CSS, primitives, and screenshots.
3. Require a taste calibration for the product category and audience.
4. Fix the lowest-scoring areas first.
5. Verify responsive layout, keyboard behavior, reduced motion, long content, and empty/loading/error states.

This workflow prevents blind restyling. The goal is not to make every project look the same. The goal is to make each project feel intentional, usable, and fit for its own audience.

## Install

Use the folder in whatever format your agent supports:

- As a project-local instruction pack at `.agents/skills/ultimate-ui-taste`
- As a reusable global instruction folder
- As copied context, starting with `SKILL.md` and loading references only as needed

Agents that support skill folders can register the folder directly. Agents that do not support skill folders can still read `SKILL.md` and the reference files as normal Markdown.

## Design Principles

- Calibrate taste before styling.
- Use references for principles, not aesthetic cloning.
- Prefer semantic controls over decorative markup.
- Make motion explain cause and effect.
- Keep typography deliberate and consistent.
- Avoid generic AI/SaaS visual habits.
- Preserve project identity when improving existing work.
- Verify behavior, not just screenshots.
