# Context And Design Direction

Use this reference before broad UI creation, redesigns, landing pages, dashboards, or taste audits.

## Context Packet

Infer or create this packet before choosing style:

```yaml
product_context:
  audience:
  primary_task:
  lane: brand | product | dashboard | docs | chat | editor | game | component-library
  brand_voice:
  anti_references:
  existing_design_system:
  implementation_constraints:
```

## Lane Rules

| Lane | Primary Goal | Design Posture |
| --- | --- | --- |
| Brand | Create desire and memory | Expressive, image-led, distinctive, restrained copy |
| Product | Help users complete work | Familiar controls, clear hierarchy, fast interactions |
| Dashboard | Scan, compare, decide | Dense, quiet, tabular, low ornament |
| Docs | Teach and unblock | Searchable, structured, code-forward |
| Chat/AI | Manage conversation and tools | Composable message primitives, visible reasoning/tool state |
| Editor | Repeated precision work | Minimal animation, keyboard-first, stable layout |
| Component library | Teach behavior and implementation | Live previews, source access, variants, responsive test frames |

## Questions To Ask Internally

1. What should the user notice first, second, and third?
2. Is the hierarchy made by typography, spacing, alignment, and contrast, or by decoration?
3. What state is changing, and how should the user understand it?
4. Would this feel annoying after 100 uses?
5. Which part looks AI-generated, and why?
6. What real states are missing: empty, loading, error, disabled, long content, permission denied, offline?

## Workflow

1. Inspect existing app files and dependencies.
2. Identify available UI libraries, icon libraries, animation libraries, and routing conventions.
3. Decide the lane and write the design intent in one or two sentences.
4. Choose a small set of visual principles: density, contrast, tone, radii, motion character, imagery.
5. Implement the smallest complete version with real states and responsive constraints.
6. Verify at desktop and mobile sizes.

## Anti-Generic Direction

Avoid defaulting to:

- Purple/blue "AI app" palettes.
- Beige/cream "tasteful" pages.
- Glassmorphism as decoration.
- Big hero text with no product proof.
- Three statistic cards that do not drive a decision.
- Vague copy like "supercharge your workflow."
