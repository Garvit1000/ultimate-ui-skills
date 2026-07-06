# Pattern Rubric And Taste Examples

Use this reference for broad redesigns, vague "make it better" requests, component libraries, AI interfaces, and review-before-fix work.

The goal is to turn inspiration into reusable judgment. Do not copy a source's look blindly. Extract the product pattern, then adapt it to the current app.

Named libraries are evidence, not taste presets. Nexus, Astryx, Watermelon, Componentry, and DESIGN.md examples should teach durable questions: What is the primitive? What state is missing? What does the user need to decide? What motion explains cause and effect? What material direction fits this product? They should not decide the final palette, radius, layout density, type mood, or visual personality.

For a compact pre-build design direction, use `design-system-packet.md`. It turns product type, audience, workflow, risk, and desired feeling into an implementation guide without creating a giant style catalog.

## Taste Calibration

Before using any source example, choose the product's own taste direction.

```yaml
taste_direction:
  product_type:
  audience:
  frequency_of_use:
  desired_feeling:
  density:
  visual_material:
  motion_character:
  must_not_feel_like:
```

Examples:

| Context | Good direction | Bad direction |
| --- | --- | --- |
| Finance operations dashboard | Dense, calm, trustworthy, tabular, conservative motion | Playful bounce, huge hero type, decorative gradients |
| Game companion app | Expressive, tactile, vivid, characterful | Plain SaaS dashboard with gray cards |
| Healthcare intake form | Clear, reassuring, low-friction, accessible | Experimental navigation or flashy motion |
| Developer tool | Fast, keyboard-first, technical, compact | Marketing-card layout that hides the workflow |
| Fashion landing page | Editorial, image-led, spacious, atmospheric | Dense admin UI or generic startup gradients |

Ask "fit for what?" before "does it look good?" A beautiful wrong-style screen is still bad UI.

## UI Taste Scorecard

Score each area from 1 to 5 before a major redesign. Fix 1s and 2s first.

| Area | 1: Weak | 3: Acceptable | 5: Excellent |
| --- | --- | --- | --- |
| Intent | Looks like a generic template | The screen has a task | Every section exists because it changes what the user can decide or do |
| First viewport | Claim-heavy, little product proof | Shows the product somewhere | Product state, action, and proof are visible immediately |
| Information architecture | Feature cards and filler metrics | Clear sections | Workflow, status, controls, and data are organized by user intent |
| Typography | Browser-default bold/small, inconsistent weights | Reasonable type scale | Deliberate type roles, stable line-height, no accidental font shifts |
| Spacing and alignment | Same gap everywhere, loose edges | Mostly aligned | Tight local grouping, larger section rhythm, clean text and control edges |
| Component semantics | Clickable divs and custom controls | Mostly semantic controls | Primitive choice maps to intent: button, link, dialog, popover, table, command |
| State coverage | Only happy path | Some empty/loading/error states | Default, hover, focus, active, loading, empty, error, disabled, long content, mobile, reduced motion |
| Motion | Decorative, bouncy, or slow | Mostly restrained | Cause-and-effect motion, interruptible transitions, quiet exits, reduced-motion variant |
| Distinctiveness | Could belong to any SaaS | Some domain tone | Visual language follows the product's material, era, audience, or workflow |
| Implementation resilience | Broad selectors, layout shift, magic values | Mostly stable | Named slots, scoped selectors, stable dimensions, keyboard and responsive checks |
| Taste fit | Borrowed library aesthetic | Some project-specific choices | The look feels inevitable for this product and audience |

## Pattern: AI Interface Primitives

Source signal: Nexus UI treats AI interfaces as composable primitives: `Thread`, `Message`, `MessageContent`, `MessageMarkdown`, `MessageAvatar`, `MessageActions`, attachments, citations, reasoning, and tools. Learn the compositional structure, not the exact chat styling.

Right:

```tsx
type MessageFrom = "user" | "assistant";

function Message({ from, children }: { from: MessageFrom; children: React.ReactNode }) {
  return (
    <MessageContext.Provider value={{ from }}>
      <article
        data-slot="message"
        aria-label={from === "user" ? "User message" : "Assistant message"}
        className={cn("flex w-full max-w-[90%] items-start gap-2", from === "user" ? "ms-auto" : "me-auto")}
      >
        {children}
      </article>
    </MessageContext.Provider>
  );
}

function MessageStack(props: React.HTMLAttributes<HTMLDivElement>) {
  const ctx = useMessageContext();
  return (
    <div
      data-slot="message-stack"
      className={cn("flex w-full flex-col gap-2", ctx?.from === "user" ? "items-end" : "items-start")}
      {...props}
    />
  );
}
```

Wrong:

```tsx
function ChatBubble({ user, text }: { user: boolean; text: string }) {
  return <div className={user ? "ml-auto bg-blue-600 p-4" : "mr-auto p-4"}>{text}</div>;
}
```

Why: one-off bubbles cannot grow into attachments, tool calls, reasoning, citations, actions, markdown, feedback, or accessible turns.

## Pattern: Primitive Taxonomy By Intent

Source signal: Astryx organizes components by product intent: App Shell, Button, Chat, Command Palette, Dialog, Empty State, Field, Layout, Navigation, Popover, Segmented Control, Table, Status Dot, and more. Learn the taxonomy, not the surface style.

Map intent before styling:

| User intent | Primitive |
| --- | --- |
| Navigate | Link or nav item |
| Submit, save, confirm | Button |
| Icon-only action | IconButton with `aria-label` |
| Choose one mode | Segmented control or radio group |
| Search actions | Command palette |
| Temporary contextual controls | Popover |
| Blocking confirmation | Alert dialog |
| Dense records | Table or list with sorting, selection, keyboard, and loading states |
| Persistent product frame | App shell |
| No data yet | Empty state with explanation and next action |

Wrong:

```tsx
<div onClick={close}>
  <XIcon />
</div>
```

Right:

```tsx
<button type="button" aria-label="Close dialog" onClick={close}>
  <XIcon aria-hidden="true" />
</button>
```

## Pattern: Registry, Live Preview, And Code Access

Source signal: Watermelon uses registry metadata, live rendered variants, raw source access, install commands, responsive preview frames, and code dialogs. Learn the preview architecture, not the exact visual treatment.

Right:

```tsx
type RegistryItem = {
  name: string;
  slug: string;
  category: string;
  description: string;
  component: React.ComponentType;
  code: () => Promise<string>;
  install?: string[];
  dependencies?: string[];
};

function VariantCard({ item }: { item: RegistryItem }) {
  return (
    <section className="grid gap-3">
      <header className="flex items-center justify-between gap-3">
        <h3 className="text-sm font-medium">{item.name}</h3>
        <button type="button" aria-label={`View code for ${item.name}`}>
          <CodeIcon aria-hidden="true" />
        </button>
      </header>
      <div className="min-h-52 overflow-hidden rounded-lg">
        <item.component />
      </div>
    </section>
  );
}
```

Wrong:

```tsx
function Gallery() {
  return screenshots.map((src) => <img src={src} alt="" />);
}
```

Why: screenshots cannot test states, keyboard behavior, responsiveness, source quality, or dependency needs.

## Pattern: Responsive Preview Frame

A real component preview needs real viewport constraints, not a claim that the component is responsive.

Right:

```tsx
const VIEWPORTS = {
  mobile: { width: 390, height: 844 },
  tablet: { width: 767, height: 1024 },
};

function useFrameScale(viewport: "desktop" | "mobile" | "tablet", ref: React.RefObject<HTMLElement>) {
  const [scale, setScale] = React.useState(1);

  React.useLayoutEffect(() => {
    const container = ref.current;
    if (!container || viewport === "desktop") return;

    const resize = () => {
      const target = VIEWPORTS[viewport];
      setScale(Math.min(container.clientWidth / target.width, container.clientHeight / target.height, 1));
    };

    resize();
    const observer = new ResizeObserver(resize);
    observer.observe(container);
    return () => observer.disconnect();
  }, [viewport, ref]);

  return scale;
}
```

Rules:

- Prevent demo navigation and form submission inside previews unless the preview is meant to navigate.
- Sync theme and global styles into iframe previews when using an iframe.
- Show a loading state until the preview is ready.
- Keep mobile and tablet sizes stable.

## Pattern: Expressive Motion Belongs To The Right Lane

Source signal: Componentry is strongest for kinetic text, scroll choreography, hero backgrounds, realistic objects, and playful components. Learn when expressive motion is appropriate, not a default animation style.

Use expressive motion for:

- Brand pages.
- Games and playful tools.
- Demos where the animation is the product.
- Rare first-time explanation moments.
- Component library examples where motion behavior is being taught.

Avoid expressive motion for:

- Dense dashboards.
- Editors.
- Repeated keyboard workflows.
- Basic SaaS settings.
- Every card in a list.

Rule: if the user would see it dozens of times per day, make it fast, quiet, or absent.

## Pattern: DESIGN.md As Material Direction

Source signal: getdesign examples describe a visual world with material, era, color role, typography, and interaction tone. Learn how to form a material direction, not how to copy a specific era.

For a strong design direction, write a compact material brief:

```yaml
design_material:
  era:
  surface_language:
  typography_character:
  color_roles:
  interaction_tone:
  density:
  anti_defaults:
```

Example:

```yaml
design_material:
  era: retro console web
  surface_language: beveled panels, hardware chrome, small status lights
  typography_character: heavy box-art labels plus plain system body text
  color_roles: amber for wayfinding, muted metal for structure
  interaction_tone: tactile and snappy, not soft SaaS
  density: compact
  anti_defaults: no purple gradients, no glass cards, no generic AI hero
```

Use this when the project needs identity. Do not invent decorative chrome without a material brief.

## Patterns To Reject Or Repair

| Pattern | Why it fails | Repair |
| --- | --- | --- |
| `transition-all` | Animates accidental properties | Use `transition-[opacity,transform,box-shadow]` or exact CSS properties |
| Global hidden scrollbars | Removes overflow affordance | Use visible scrollbar, fade mask, or a local class with another cue |
| `whileTap={{ scale: 0.9 }}` | Feels exaggerated | Use `0.96`, or no scale for static/serious controls |
| Clickable card as `div` | Often breaks semantics | Prefer `Link`; if mixed controls exist, make the main action explicit |
| Hero made only of abstract panels | Product proof is weak | Show real state, real action, screenshot, preview, or workflow |
| Component gallery as screenshots | Cannot test behavior | Render live variants and expose source |
| Same gap everywhere | Mechanical rhythm | Use item, group, section, and viewport spacing scales |
| Decorative grid background | Common AI tell | Use only when it helps measurement, layout, or brand material |

## Review Before Fix Prompt

Use this mini-protocol for existing projects:

```text
1. Identify the lane and material direction.
2. Score the page with the UI Taste Scorecard.
3. Name the top 3 defects, with source selectors or components.
4. Patch the smallest coherent area.
5. Verify: lint/build, responsive, keyboard, long content, reduced motion.
6. Report before/after in a compact table.
```
