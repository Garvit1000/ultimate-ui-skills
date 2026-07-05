# Source Pattern Examples: Nexus UI, Astryx, Watermelon

Use this reference when building component libraries, AI interfaces, preview systems, or code examples.

For broader review scoring, live-preview architecture, component-library rubrics, or source-pattern comparison, also read `pattern-rubric.md`.

These sources are not visual themes. Do not copy their palette, radius, density, type mood, spacing, or animation personality unless it genuinely fits the current project. Use them to learn structure: primitive choice, slot design, source access, live preview, state coverage, accessibility, and interaction behavior.

Before applying a pattern, answer:

1. What principle is useful here?
2. What parts are only that library's taste?
3. What should change to match this product's audience, density, and material direction?

## Nexus UI: AI Interfaces As Primitives

Nexus UI teaches that AI interfaces need domain-specific slots, not one-off bubbles. The lesson is composability, not the exact bubble shape or typography.

Right:

```tsx
function Message({ from, children, ...props }: MessageProps) {
  return (
    <MessageContext.Provider value={{ from }}>
      <article
        data-slot="message"
        aria-label={from === "user" ? "User message" : "Assistant message"}
        className={cn("group/message flex w-full max-w-[90%] gap-2", from === "user" ? "ms-auto" : "me-auto")}
        {...props}
      >
        {children}
      </article>
    </MessageContext.Provider>
  );
}
```

Wrong:

```tsx
function ChatBubble({ user, text }: { user: boolean; text: string }) {
  return <div className={user ? "ml-auto bg-blue-600 p-4" : "mr-auto p-4"}>{text}</div>;
}
```

Takeaway: encode role, slot, and behavioral state. Leave room for attachments, citations, tool calls, feedback, and actions.

## Astryx: Taxonomy By Intent

Astryx teaches primitive selection by product category: Action, Chat, Container, Content, Data Input, Feedback, Layout, Navigation, Overlay, Table/List, Utility. The lesson is intent mapping, not a mandatory component look.

Right:

```tsx
<IconButton aria-label="Close chat">
  <XIcon aria-hidden="true" />
</IconButton>

<CommandPalette open={open} onOpenChange={setOpen}>
  <CommandPaletteInput placeholder="Search components" />
  <CommandPaletteList />
</CommandPalette>
```

Wrong:

```tsx
<div onClick={close}>
  <XIcon />
</div>
```

Takeaway: choose controls by intent first; style second.

## Watermelon: Registry, Live Preview, Code Access

Watermelon teaches component-library architecture: registry metadata, live rendered variants, code dialogs, categories, and responsive preview frames. The lesson is proof through live behavior, not a reusable visual skin.

Right:

```tsx
type Variant = {
  id: string;
  title: string;
  component: React.ComponentType;
  colSpan?: number;
};

function VariantCard({ variant, onCodeClick }: { variant: Variant; onCodeClick: (v: Variant) => void }) {
  return (
    <section className="flex h-full flex-col gap-3">
      <header className="flex items-center justify-between border-b py-3">
        <h3 className="text-sm font-medium">{variant.title}</h3>
        <button type="button" aria-label={`View code for ${variant.title}`} onClick={() => onCodeClick(variant)}>
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

Wrong:

```tsx
const screenshots = ["/button.png", "/tabs.png", "/dialog.png"];
function Gallery() {
  return screenshots.map((src) => <img src={src} alt="" />);
}
```

Takeaway: component libraries should teach behavior through live previews and source access.

## Watermelon Improvements To Encode

Do not copy these habits blindly.

Wrong:

```tsx
className="transition-all duration-300"
```

Better:

```tsx
className="transition-[background-color,color,box-shadow,transform] duration-150 ease-out active:scale-[0.96]"
```

Wrong:

```css
* {
  scrollbar-width: none;
}
```

Better:

```css
.scroll-fade-x {
  overflow-x: auto;
  scrollbar-width: thin;
  mask-image: linear-gradient(to right, transparent, black 32px, black calc(100% - 32px), transparent);
}
```

Takeaway: learn architecture and examples from libraries, but still enforce motion, accessibility, and affordance rules.
