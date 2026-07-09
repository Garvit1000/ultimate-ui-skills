# Ultimate UI Taste

## Before And After

### Landing Page

| Before | After |
| --- | --- |
| ![Landing page before skill training](media/Screenshot%202026-07-06%20132047.png) | ![Landing page after skill training](media/Screenshot%202026-07-06%20132848.png) |

### Dashboard

| Before | After |
| --- | --- |
| ![Dashboard before skill training](media/Screenshot%202026-07-06%20132104.png) | ![Dashboard after skill training](media/Screenshot%202026-07-06%20132906.png) |

### Ecommerce Dashboard

| Before | After |
| --- | --- |
| ![Ecommerce dashboard before skill training](media/Screenshot%202026-07-07%20123258.png) | ![Ecommerce dashboard after skill training](media/Screenshot%202026-07-07%20123353.png) |

Ultimate UI Taste is an agent instruction pack for reviewing, designing, and improving high-taste user interfaces. It focuses on product intent, visual hierarchy, typography, motion, component semantics, accessibility, state coverage, and implementation resilience.

It is built to improve both new and existing projects. It does not force one visual style. Instead, it calibrates the right taste direction for each product, then applies durable UI, UX, and animation principles.

## What It Helps With

- Landing pages and product websites
- SaaS dashboards and operational tools
- AI chat and agent interfaces
- Component libraries and preview systems
- Motion systems, transitions, drawers, popovers, and icon states
- Fluid gesture UI: sheets, drawers, swipe, drag, carousels, springs, and translucent chrome
- Existing project audits and design repair
- Actionable `file:line` UI reviews with severity, issue, and fix
- Inspiration-site analysis without copying source visuals or code
- Perceptual color discipline for contrast, palettes, and dark mode
- Detecting generic AI-generated UI patterns

## Current Focus

The skill now has sharper rules for three common failure points:

- Color: use perceptual color thinking when creating new palettes. OKLCH is preferred when the project supports it, with contrast fixed through lightness before changing hue or chroma.
- Review output: existing project audits should cite `file:line` when source code is available, then name severity, issue, and fix.
- Inspiration sources: reference sites should be reduced to primitives such as color roles, type roles, spacing, radius, shadows, density, motion character, and product patterns. They are not permission to clone a page or treat one screen as a full design system.
- Gesture motion: drag, swipe, sheet, and carousel interactions should track the pointer, inherit release velocity, remain interruptible, and provide reduced-motion and reduced-transparency fallbacks.

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
Use the Ultimate UI Taste instructions to audit the current UI. Identify what looks generic or AI-generated, cite file:line findings when source is available, explain the highest-impact issues, then patch the smallest coherent area.
```

## Recommended Workflow

1. Ask for review before fixes.
2. Let the agent inspect the codebase, routes, global CSS, primitives, and screenshots.
3. Require a taste calibration for the product category and audience.
4. Fix the lowest-scoring areas first.
5. Verify responsive layout, keyboard behavior, reduced motion, long content, and empty/loading/error states.

This workflow prevents blind restyling. The goal is not to make every project look the same. The goal is to make each project feel intentional, usable, and fit for its own audience.

## Install

From Skills.sh:

```text
npx skills add Garvit1000/ultimate-ui-skills
```

Use the folder in whatever format your agent supports:

- As a project-local instruction pack at `.agents/skills/ultimate-ui-taste`
- As a reusable global instruction folder
- As copied context, starting with `SKILL.md` and loading references only as needed

Agents that support skill folders can register the folder directly. Agents that do not support skill folders can still read `SKILL.md` and the reference files as normal Markdown.

## Acknowledgements

This project is an original instruction pack shaped by studying strong design engineering work, public writing, open source interfaces, and component documentation. The goal is to learn durable principles, not to copy a specific visual style, brand, component library, or author's work.

Primary inspirations and references include:

- Emil Kowalski's writing and design engineering philosophy around motion, polish, and interface feel
- Emil Kowalski's `apple-design` skill on fluid interfaces and Apple-style motion foundations
- Jakub Krehel's interface-detail writing, including [Details that make interfaces feel better](https://jakub.kr/writing/details-that-make-interfaces-feel-better)
- [Impeccable Style](https://impeccable.style/)
- [Onur's design and engineering bookmarks](https://onur.dev/bookmarks)
- [Nexus UI](https://nexus-ui.dev/)
- [Componentry documentation](https://componentry.dev/docs)
- [Astryx design system](https://astryx.atmeta.com/components)
- [WatermelonCorp/watermelon-platform](https://github.com/WatermelonCorp/watermelon-platform)
- [google-labs-code/design.md](https://github.com/google-labs-code/design.md)
- [Recent.design skills directory](https://recent.design/skills)
- [extract-design-system](https://github.com/arvindrk/extract-design-system)
- [oklch-skill](https://github.com/jakubkrehel/oklch-skill)
- [userinterface-wiki](https://github.com/raphaelsalaja/userinterface-wiki)
- [Vercel agent skills](https://github.com/vercel-labs/agent-skills)
- [Design.md Nintendo 2001 case study](https://getdesign.md/nintendo-2001/design-md)
- The public [`ui-ux-pro-max` skill page on Skills.sh](https://www.skills.sh/nextlevelbuilder/ui-ux-pro-max-skill/ui-ux-pro-max)

## Copyright And Source Use

No third-party brand, website, component, image, or codebase is claimed as original work here. External materials are credited as inspiration and research sources. This repository should not be treated as a mirror, clone, or substitute for any referenced project.

When this skill discusses patterns from public sources, it should paraphrase the principle and apply it to the user's project. Do not copy proprietary text, assets, layouts, screenshots, or source code from referenced projects unless their license explicitly allows that use and the copied material is attributed according to that license.

Open source references remain governed by their own licenses. Before reusing code from any linked repository or component library, check that project's license and attribution requirements.

## Design Principles

- Calibrate taste before styling.
- Use references for principles, not aesthetic cloning.
- Prefer semantic controls over decorative markup.
- Make motion explain cause and effect.
- Keep typography deliberate and consistent.
- Avoid generic AI/SaaS visual habits.
- Preserve project identity when improving existing work.
- Treat reference sites as research inputs, not clone targets.
- Prefer actionable review findings over vague taste commentary.
- Verify behavior, not just screenshots.
