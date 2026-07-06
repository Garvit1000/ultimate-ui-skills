# Ultimate UI Taste Skill Research Memory

Date: 2026-07-05

Purpose: durable research notes for building future Codex skills for UI, UX, and animation taste. This file exists so context compaction does not erase the research direction.

## Source Map

- Emil Kowalski local skill: `C:\Users\garvi\.agents\skills\emil-design-eng\SKILL.md`
- Emil writing: `https://emilkowal.ski/ui/good-vs-great-animations`, `https://emilkowal.ski/ui/great-animations`, `https://emilkowal.ski/ui/building-a-drawer-component`, `https://emilkowal.ski/ui/agents-with-taste`
- Impeccable: `https://impeccable.style/`, `https://impeccable.style/designing/`, `https://impeccable.style/docs/`, `https://impeccable.style/slop/`
- Jakub Krehel skill repo: `.research/make-interfaces-feel-better`
- Watermelon UI repo: `.research/watermelon-platform`
- Nexus UI docs: `https://nexus-ui.dev/`, `https://nexus-ui.dev/docs/installation`, `https://nexus-ui.dev/docs/components/message`
- Astryx docs: `https://astryx.atmeta.com/components`, `https://astryx.atmeta.com/themes`
- Vercel Web Interface Guidelines: `https://vercel.com/design/guidelines`
- Componentry: `https://componentry.dev/docs`
- Onur bookmarks: `https://onur.dev/bookmarks`, especially `/reading`
- getdesign Nintendo 2001 DESIGN.md: `https://getdesign.md/nintendo-2001/design-md`

## Core Thesis

Great AI-generated UI needs a judgment system, not a bag of visual tricks.

The future skills should make the agent pause and ask:

1. What is the product context?
2. Is this brand, product UI, dashboard, editor, chat, docs, or game?
3. What user action or state change does the interface support?
4. How often will this interaction be seen?
5. What should move, what should stay still, and why?
6. Which existing primitive should be used before inventing a custom control?
7. What slop tells must be removed before shipping?
8. How does the design survive long content, empty states, loading, errors, keyboard use, mobile, dark mode, and reduced motion?

## Proposed Skill Folder Structure

```text
skills/
  ultimate-ui-taste/
    SKILL.md
    references/
      context.md
      ui/
        layout.md
        typography.md
        surfaces.md
        color.md
        components.md
        dashboards.md
        ai-interfaces.md
      ux/
        flows.md
        states.md
        copy.md
        accessibility.md
        resilience.md
      animations/
        emil-motion.md
        interaction-motion.md
        gesture-motion.md
        performance.md
      anti-slop/
        generated-ui-tells.md
        review-checklist.md
      examples/
        nexus-ui.md
        astryx.md
        watermelon.md
```

## Non-Negotiable Taste Rules

- Start with context. Write or read `PRODUCT.md` and `DESIGN.md` before broad UI work.
- Separate brand pages from product screens. Landing pages can be expressive; dashboards must be task-first, dense, and scannable.
- Use native semantics and known primitives before custom divs.
- No generic AI look: purple-blue gradients, glassmorphism-by-default, nested cards, gradient text, random glow, repeated icon-card grids, oversized rounded cards, and motion without purpose.
- No emojis or em dashes in generated UI copy, labels, docs, or skill content unless the user explicitly asks for them.
- No decorative horizontal divider lines, background grids, or technical linework unless they clarify grouping, measurement, or navigation.
- Typography must be internally consistent. Avoid default-looking bold/small pairings inside cards and metadata rows.
- UI animation must have a purpose: feedback, state indication, spatial continuity, explanation, or jarring-change prevention.
- Never animate keyboard-initiated frequent actions.
- Prefer CSS transitions for interruptible UI. Use keyframes for staged one-shot entrances, not rapidly toggled states.
- Animate `transform` and `opacity` first. Avoid layout property animation.
- Use `transition-property` explicitly. No `transition: all`.
- Origin-aware popovers scale from the trigger. Modals remain centered.
- Do not enter from `scale(0)`. Start around `scale(0.95)` with opacity.
- Pressable controls need tactile feedback around `scale(0.96)` or `0.97`, unless disabled for a static/serious context.
- Use `text-wrap: balance` for headings and `text-wrap: pretty` for short body text.
- Dynamic numbers use tabular numbers.
- Nested radii are concentric: `outer radius = inner radius + padding`.
- Images get subtle neutral outlines when edge definition matters.
- Reduced motion is a variant, not an afterthought.

## Source Pattern: Nexus UI

Nexus UI is valuable because it treats AI interfaces as a first-class product domain. It has primitives for messages, prompt input, tools, reasoning, citations, attachments, suggestions, feedback, and toasts. This is the right mental model: build a vocabulary of AI interaction slots instead of one giant chat component.

### Right Pattern: Composable Message Slots

Source concept: `https://nexus-ui.dev/docs/components/message`

```tsx
type MessageFrom = "user" | "assistant";

type MessageProps = React.HTMLAttributes<HTMLDivElement> & {
  from: MessageFrom;
};

function Message({ from, children, ...props }: MessageProps) {
  return (
    <MessageContext.Provider value={{ from }}>
      <div
        data-slot="message"
        role="article"
        aria-label={from === "user" ? "User message" : "Assistant message"}
        className={cn(
          "group/message flex w-full max-w-[90%] items-start gap-2",
          from === "user" ? "ms-auto" : "me-auto",
        )}
        {...props}
      >
        {children}
      </div>
    </MessageContext.Provider>
  );
}

function MessageStack(props: React.HTMLAttributes<HTMLDivElement>) {
  const ctx = useMessageContext();
  return (
    <div
      data-slot="message-stack"
      className={cn(
        "flex w-full flex-col gap-2",
        ctx?.from === "user" ? "items-end" : "items-start",
      )}
      {...props}
    />
  );
}
```

Why it is right:

- `from` is behavioral state, not just a CSS class.
- The context lets child slots align correctly without repeating conditionals everywhere.
- `role="article"` and `aria-label` give chat turns meaning.
- `data-slot` makes styling, debugging, and automated review easier.
- The primitive supports attachments, avatars, actions, markdown, and future composition.

### Wrong Pattern: One-Off Chat Bubble

```tsx
function ChatBubble({ user, text }: { user: boolean; text: string }) {
  return (
    <div className={user ? "ml-auto rounded-2xl bg-blue-600 p-4" : "mr-auto p-4"}>
      {text}
    </div>
  );
}
```

Why it is wrong:

- No semantic role or accessible label.
- No slots for avatar, attachments, actions, citations, or tool state.
- Alignment logic will be duplicated when the component grows.
- It produces a demo bubble, not a system primitive.

### Skill Rule To Encode

When building AI chat or agent UI, start with composable primitives:

- `Thread`
- `Message`
- `MessageStack`
- `MessageContent`
- `MessageActions`
- `AttachmentList`
- `Citation`
- `Reasoning`
- `ToolCall`
- `PromptInput`
- `FeedbackBar`

Do not build a single monolithic `Chat.tsx` unless the product is truly disposable.

## Source Pattern: Astryx

Astryx is valuable for taxonomy. It does not present components as decorations; it maps them to product categories: Action, Chat, Container, Content, Data Input, Feedback, Layout, Navigation, Overlay, Table/List, Utility.

Source concept: `https://astryx.atmeta.com/components`

### Right Pattern: Choose The Primitive By Intent

```tsx
// Action: use Button or IconButton.
<Button type="submit">Pay now</Button>
<IconButton aria-label="Close chat">
  <XIcon />
</IconButton>

// Overlay: use Dialog, Popover, Tooltip, Toast, or Command Palette.
<CommandPalette open={open} onOpenChange={setOpen}>
  <CommandPaletteInput placeholder="Search components" />
  <CommandPaletteList />
</CommandPalette>

// Layout: use AppShell, Section, Grid, HStack, VStack, or LayoutPanel.
<AppShell>
  <SideNav />
  <LayoutContent>{children}</LayoutContent>
</AppShell>
```

Why it is right:

- The control choice comes from task intent.
- Accessibility behavior is inherited from the primitive.
- Product screens become consistent because the same intent maps to the same control family.

### Wrong Pattern: Custom Interaction With Divs

```tsx
<div className="icon" onClick={close}>
  <XIcon />
</div>

<div className="fake-menu">
  <div onClick={runAction}>Run</div>
</div>
```

Why it is wrong:

- No keyboard behavior.
- No focus management.
- No accessible name.
- The visual design may look acceptable, but the behavior is fake.

### Skill Rule To Encode

Before designing a custom component, map the job to a known primitive:

| User Intent | Use |
| --- | --- |
| Submit, save, confirm | Button |
| Icon-only action | IconButton with `aria-label` |
| Toggle binary setting | Switch or Checkbox |
| Choose one of a few modes | Segmented Control or Radio Group |
| Navigate pages | Link or Nav Item |
| Search commands | Command Palette |
| Temporary contextual controls | Popover |
| Blocking confirmation | Alert Dialog |
| Persistent app frame | App Shell |
| Dense records | Table/List with keyboard and selection behavior |

## Source Pattern: Watermelon UI

Watermelon is valuable for open source component registry architecture: live previews, code dialogs, categories, dashboard templates, responsive preview iframes, and concrete component variants.

Local source:

- `.research/watermelon-platform/src/pages/component-category.tsx`
- `.research/watermelon-platform/src/components/preview/responsive-preview-frame.tsx`
- `.research/watermelon-platform/src/index.css`
- `.research/watermelon-platform/src/components/ui/button.tsx`
- `.research/watermelon-platform/src/components/landing/hero.tsx`

### Right Pattern: Registry Metadata Drives The UI

```tsx
type Variant = {
  id: string;
  title: string;
  component: React.ComponentType;
  colSpan?: number;
};

function VariantCard({
  variant,
  onCodeClick,
}: {
  variant: Variant;
  onCodeClick: (variant: Variant) => void;
}) {
  return (
    <section className="flex h-full flex-col gap-3">
      <header className="flex items-center justify-between border-b py-3">
        <h3 className="text-sm font-medium">{variant.title}</h3>
        <button
          type="button"
          aria-label={`View code for ${variant.title}`}
          onClick={() => onCodeClick(variant)}
          className="grid size-8 place-items-center rounded-md"
        >
          <CodeIcon aria-hidden="true" />
        </button>
      </header>
      <div className="relative flex min-h-52 items-center justify-center overflow-hidden">
        <variant.component />
      </div>
    </section>
  );
}
```

Why it is right:

- Component examples are real rendered components, not screenshots.
- Code access is attached to the exact variant.
- `aria-label` names the icon button.
- Variant metadata supports grids, categories, and search without hardcoding every page.

### Wrong Pattern: Static Gallery

```tsx
const screenshots = ["/button.png", "/tabs.png", "/dialog.png"];

function Gallery() {
  return screenshots.map((src) => <img src={src} alt="" />);
}
```

Why it is wrong:

- Static images cannot test states, keyboard behavior, responsiveness, or code quality.
- The user cannot copy or inspect the implementation.
- The gallery teaches visuals, not behavior.

### Right Pattern: Responsive Preview Frame

Distilled from Watermelon’s `ResponsivePreviewFrame`.

```tsx
const VIEWPORTS = {
  mobile: { width: 390, height: 844 },
  tablet: { width: 767, height: 1024 },
};

function useFrameScale(viewport: "desktop" | "mobile" | "tablet", ref: RefObject<HTMLElement>) {
  const [scale, setScale] = useState(1);

  useLayoutEffect(() => {
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

Why it is right:

- The preview has real viewport constraints.
- The scale is computed from available space instead of guessed.
- `ResizeObserver` keeps the preview correct as the shell changes.
- This is better than “looks responsive” claims.

### Watermelon Patterns To Reject Or Improve

#### Wrong: `transition-all`

Source: `.research/watermelon-platform/src/components/ui/button.tsx`

```tsx
const buttonClass = "transition-all duration-300";
```

Better:

```tsx
const buttonClass =
  "transition-[background-color,color,box-shadow,transform] duration-150 ease-out active:scale-[0.96]";
```

Why:

- `transition-all` can animate layout-affecting properties accidentally.
- Exact properties are easier to review and optimize.
- Buttons need crisp press feedback.

#### Wrong: Global Scrollbar Hiding

Source concept: `.research/watermelon-platform/src/index.css`

```css
* {
  scrollbar-width: none;
}

*::-webkit-scrollbar {
  display: none;
}
```

Better:

```css
.scroll-fade-x {
  overflow-x: auto;
  scrollbar-width: thin;
  mask-image: linear-gradient(to right, transparent, black 32px, black calc(100% - 32px), transparent);
}

.chrome-hidden-scrollbar {
  scrollbar-width: none;
}

.chrome-hidden-scrollbar::-webkit-scrollbar {
  display: none;
}
```

Why:

- Global hidden scrollbars remove a core affordance.
- Hide scrollbars only where the design provides another cue: fade mask, pagination, visible drag affordance, or explicit overflow control.

#### Wrong: Generic Image Hover Scale

Source concept: Watermelon landing hero image collage.

```tsx
<motion.div whileHover={{ scale: 1.05, zIndex: 50 }}>
  <img src={url} alt="" />
</motion.div>
```

Better:

```tsx
<motion.figure
  whileHover={{ y: -4 }}
  transition={{ duration: 0.18, ease: [0.23, 1, 0.32, 1] }}
>
  <img className="outline outline-1 -outline-offset-1 outline-black/10" src={url} alt={alt} />
  <figcaption>{label}</figcaption>
</motion.figure>
```

Why:

- Image hover scale is an AI-generated UI tell when it does not support inspection or selection.
- Lifting the entire figure preserves image legibility and feels more product-like.
- If the image is the product, keep it still unless hover reveals useful detail.

#### Missing: Reduced Motion Variant

Better:

```tsx
const shouldReduceMotion = useReducedMotion();

const itemVariants = {
  hidden: shouldReduceMotion
    ? { opacity: 0 }
    : { opacity: 0, y: 16, filter: "blur(4px)" },
  visible: shouldReduceMotion
    ? { opacity: 1 }
    : { opacity: 1, y: 0, filter: "blur(0px)" },
};
```

Why:

- Reduced motion is not “no design”; it keeps state comprehension while removing movement.

## Source Pattern: Impeccable

Impeccable is valuable for system workflow and anti-slop language.

### Right Process

```text
1. Init context
   - audience
   - product lane or brand lane
   - voice
   - anti-references
   - design system/tokens

2. Shape or craft
   - brief before build
   - use visual references for blank slate work

3. Refine by named discipline
   - typeset
   - layout
   - colorize
   - animate
   - polish

4. Pre-ship gauntlet
   - audit
   - clarify
   - harden

5. Maintain system
   - extract repeated intent into components/tokens
   - document DESIGN.md
```

### Skill Rule To Encode

Every design skill should ask for or infer:

```yaml
product_context:
  audience:
  task:
  lane: brand | product | dashboard | docs | chat | game
  voice:
  anti_references:
  existing_design_system:
```

### Anti-Slop Rules To Encode

Reject:

- Purple/violet gradient default palette.
- Cyan-on-dark “AI app” palette unless the brand requires it.
- Gradient text on headings or metrics.
- Nested cards inside cards.
- Same icon-card repeated across a whole page.
- Hero metric trio as filler.
- Monotonous spacing.
- Cream/beige “tasteful” background by reflex.
- Bounce/elastic easing on normal UI elements.
- Layout property animation.
- Image hover scale without purpose.
- Generic SaaS copy: streamline, empower, supercharge, world-class, enterprise-grade.
- Skipped heading levels.
- Tiny body text.
- Tight body line-height.
- Wide tracking on body text.

## Source Pattern: Emil Motion

Emil is the animation source of truth.

### Motion Decision Function

```ts
type InteractionFrequency = "hundreds_per_day" | "tens_per_day" | "occasional" | "rare";

function shouldAnimate(frequency: InteractionFrequency, initiatedByKeyboard: boolean) {
  if (initiatedByKeyboard) return false;
  if (frequency === "hundreds_per_day") return false;
  if (frequency === "tens_per_day") return "minimal";
  if (frequency === "occasional") return true;
  return "can_delight";
}
```

### Easing Decision Function

```ts
const easings = {
  out: "cubic-bezier(0.23, 1, 0.32, 1)",
  inOut: "cubic-bezier(0.77, 0, 0.175, 1)",
  drawer: "cubic-bezier(0.32, 0.72, 0, 1)",
  icon: "cubic-bezier(0.2, 0, 0, 1)",
};

function chooseEasing(context: {
  enteringOrExiting?: boolean;
  movingOnScreen?: boolean;
  hoverOrColor?: boolean;
  constantMotion?: boolean;
}) {
  if (context.constantMotion) return "linear";
  if (context.hoverOrColor) return "ease";
  if (context.movingOnScreen) return easings.inOut;
  if (context.enteringOrExiting) return easings.out;
  return easings.out;
}
```

### Right: Origin-Aware Popover

```css
.popover-content {
  transform-origin: var(--radix-popover-content-transform-origin);
  opacity: 1;
  transform: scale(1) translateY(0);
  transition:
    opacity 160ms cubic-bezier(0.23, 1, 0.32, 1),
    transform 160ms cubic-bezier(0.23, 1, 0.32, 1);
}

.popover-content[data-starting-style],
.popover-content[data-ending-style] {
  opacity: 0;
  transform: scale(0.96) translateY(-2px);
}
```

Wrong:

```css
.popover-content {
  transform-origin: center;
  transition: all 300ms ease-in;
  transform: scale(0);
}
```

Why:

- Popovers are anchored to triggers.
- `scale(0)` appears from nowhere.
- `ease-in` delays the moment the user is watching.
- `transition: all` is imprecise.

### Right: Drawer With Gesture Performance

```tsx
function onDrag(distance: number, drawer: HTMLElement) {
  drawer.style.transform = `translateY(${Math.max(distance, 0)}px)`;
}
```

Wrong:

```tsx
function onDrag(distance: number, drawer: HTMLElement) {
  drawer.style.setProperty("--swipe-amount", `${distance}px`);
}
```

Why:

- CSS variables inherit, causing style recalculation across children.
- Direct transform updates only the dragged element.

## Source Pattern: Jakub Details

Jakub is the source for exact visual detail implementation.

### Right: Contextual Icon Swap

```tsx
function CopyButton({ copied }: { copied: boolean }) {
  return (
    <button className="relative grid size-8 place-items-center transition-transform duration-150 ease-out active:scale-[0.96]">
      <span
        aria-hidden={!copied}
        className={cn(
          "absolute transition-[opacity,scale,filter] duration-300 [transition-timing-function:cubic-bezier(0.2,0,0,1)]",
          copied ? "scale-100 opacity-100 blur-0" : "scale-[0.25] opacity-0 blur-[4px]",
        )}
      >
        <CheckIcon />
      </span>
      <span
        aria-hidden={copied}
        className={cn(
          "transition-[opacity,scale,filter] duration-300 [transition-timing-function:cubic-bezier(0.2,0,0,1)]",
          copied ? "scale-[0.25] opacity-0 blur-[4px]" : "scale-100 opacity-100 blur-0",
        )}
      >
        <CopyIcon />
      </span>
    </button>
  );
}
```

Wrong:

```tsx
<button>{copied ? <CheckIcon /> : <CopyIcon />}</button>
```

Why:

- Instant swapping looks mechanical.
- Keeping both icons in DOM gives enter and exit motion without adding Motion.
- Scale/opacity/blur creates a smooth contextual transition.

### Right: Concentric Radius

```css
.card {
  padding: 8px;
  border-radius: 20px;
}

.card-inner {
  border-radius: 12px;
}
```

Wrong:

```css
.card {
  padding: 8px;
  border-radius: 12px;
}

.card-inner {
  border-radius: 12px;
}
```

Why:

- Same radius on parent and child creates visual pinching.
- The correct outer radius equals inner radius plus padding.

### Right: Shadow As Border For Elevated Surfaces

```css
.surface {
  box-shadow:
    0 0 0 1px rgb(0 0 0 / 0.06),
    0 1px 2px -1px rgb(0 0 0 / 0.06),
    0 2px 4px rgb(0 0 0 / 0.04);
  transition: box-shadow 150ms cubic-bezier(0.23, 1, 0.32, 1);
}
```

Wrong:

```css
.surface {
  border: 1px solid #e5e7eb;
}
```

Why:

- Layered transparent shadows adapt better across surfaces.
- Hard borders can look pasted on.
- Keep real borders for dividers, inputs, table boundaries, and accessibility outlines.

## Source Pattern: Vercel Interface Guidelines

Vercel provides the production hardening layer.

Skill rules:

- Keyboard works everywhere.
- Focus is visible with `:focus-visible`.
- Links are links; buttons are actions.
- Icon-only buttons have accessible names.
- Loading buttons keep the original label.
- Skeletons mirror final content to prevent layout shift.
- URLs should hold shareable state for filters, tabs, pagination, and expanded panels.
- Forms do not block typing; validate with feedback.
- Never disable browser zoom.
- Minimum mobile target is 44px.
- Content handles long names, localization, huge numbers, empty states, error states, and offline states.
- Large lists should be virtualized or use `content-visibility`.

## Future Skill Writing Plan

### Phase 1: Create Base Skill

Create `ultimate-ui-taste/SKILL.md` with:

- trigger rules
- research-grounded philosophy
- mandatory context scan
- brand vs product lane
- output format
- review format
- source references

### Phase 2: Create Modular References

Create references for:

- `animations/emil-motion.md`
- `ui/components.md`
- `ui/surfaces.md`
- `ui/typography.md`
- `ui/dashboards.md`
- `ui/ai-interfaces.md`
- `ux/states.md`
- `ux/accessibility.md`
- `anti-slop/generated-ui-tells.md`

### Phase 3: Add Example Library

Create example files:

- `examples/nexus-ui.md`: composable AI interface primitives.
- `examples/astryx.md`: taxonomy and primitive selection by intent.
- `examples/watermelon.md`: registry architecture, live preview, and what to fix.

### Phase 4: Use On Current Baseline

After installing/activating the new skill, run it against:

- `ui-taste/app/page.tsx`
- `ui-taste/app/dashboard/page.tsx`
- `ui-taste/app/globals.css`

Expected before/after focus:

- remove warm cream reflex if not intentional
- refine motion timings/easing
- replace generic decorative panels with clearer product/brand intent
- add stronger dashboard density and states
- add reduced-motion variants
- remove any accidental AI slop tells

## Questions The Skill Must Ask Itself

1. Does this screen have a reason to exist beyond looking impressive?
2. What is the fastest path to user value?
3. What should the user notice first, second, and third?
4. Is the visual hierarchy created by type, spacing, contrast, and alignment, or by decoration?
5. Is each animation tied to cause and effect?
6. Is the component primitive correct for the intent?
7. Would this survive keyboard-only use?
8. Would this survive long German text?
9. Would this survive 10,000 rows or many messages?
10. Would this feel annoying after 100 uses?
11. Does the interface use real content, real states, and real affordances?
12. Which part looks AI-generated, and why?

## Current Verdict On The Baseline We Built

The current `ui-taste` baseline is useful as a before-state. It has visual energy and a working landing/dashboard structure, but it still lacks the strict research-backed system:

- It uses a warm paper palette that may read as the newer “tasteful AI” default unless justified.
- Motion exists, but it is not yet tied tightly enough to user intent.
- Dashboard cards are attractive, but not yet operationally dense.
- Reduced motion exists globally, but motion variants are not purpose-designed.
- It does not yet encode real product state: empty, loading, error, long labels, keyboard, large data.
- It needs a clearer separation between brand expression and product utility.

This is good. It gives us a visible before/after test for the future skill.
