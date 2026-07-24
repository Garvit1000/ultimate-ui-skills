# Component Intent And Primitives

Use this reference when choosing controls, building component libraries, or designing AI/product interfaces.

## Primitive Selection

Map user intent to a known primitive before inventing custom UI.

| Intent | Use |
| --- | --- |
| Submit, save, confirm | Button |
| Navigate | Link/Nav item |
| Icon-only action | IconButton with `aria-label` |
| Binary setting | Switch or Checkbox |
| Choose one of few modes | Segmented control or Radio Group |
| Choose from many options | Select, Combobox, Command Palette |
| Temporary contextual actions | Popover |
| Blocking confirmation | Alert Dialog |
| Supplemental explanation | Tooltip or Hover Card |
| Persistent application frame | App Shell |
| Dense records | Table/List with sorting, selection, keyboard behavior |

Wrong:

```tsx
<div className="icon" onClick={close}>
  <XIcon />
</div>
```

Right:

```tsx
<button type="button" aria-label="Close dialog" onClick={close}>
  <XIcon aria-hidden="true" />
</button>
```

## Library Selection

Choose by task, not by brand recognition.

1. Check the dependency manifest and existing primitives first.
2. Reuse an installed library when it solves the task adequately.
3. Recommend one clear option. Do not dump a menu of interchangeable packages.
4. Do not replace a working competitor unless the user asks or the current choice creates a concrete accessibility, performance, or maintenance problem.
5. Use CSS for simple hover, press, color, and opacity transitions. Use a motion library for springs, gestures, layout transitions, and coordinated enter/exit behavior.

Treat these as current defaults, not permanent requirements:

| Task | Good default |
| --- | --- |
| Accessible unstyled dialogs, popovers, menus, and selects | Base UI |
| Existing Radix-based project | Keep Radix unless migration has a clear benefit |
| General springs, gestures, layout, and enter/exit motion | Motion |
| Toasts | Sonner |
| Animated changing numbers | NumberFlow |
| Standard dashboard charts | Recharts |
| Streaming time-series charts | Liveline |
| Drag and drop | dnd-kit |
| Large lists and tables | Virtuoso |
| Shared client state | Zustand |
| Conditional class strings | clsx |
| Typed component variants | CVA |

Verify maintenance status, framework compatibility, accessibility behavior, bundle cost, and license before adding a package. If the project already has a coherent alternative, preserve it.

## AI Interface Primitives

Do not build one monolithic `Chat.tsx` for serious agent UI. Use composable slots:

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

Right:

```tsx
type MessageProps = React.HTMLAttributes<HTMLDivElement> & {
  from: "user" | "assistant";
};

function Message({ from, children, ...props }: MessageProps) {
  return (
    <MessageContext.Provider value={{ from }}>
      <article
        data-slot="message"
        aria-label={from === "user" ? "User message" : "Assistant message"}
        className={cn(
          "group/message flex w-full max-w-[90%] items-start gap-2",
          from === "user" ? "ms-auto" : "me-auto",
        )}
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

Why: the right version creates semantic turns, styling slots, context-aware child alignment, and room for attachments/actions/tools.

## Component Library Pattern

Component libraries should teach behavior, not just visuals.

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

Why: static screenshots cannot test keyboard behavior, states, responsiveness, or implementation quality.

## Control Detail Rules

- Minimum target size: 40x40px, preferably 44x44px.
- Keep hit areas from overlapping.
- Use `:focus-visible`.
- Keep labels during loading; do not replace the label with only a spinner.
- Use familiar icons instead of text when the symbol is universal, but add tooltips for unfamiliar icons.
- Add `data-slot` where building reusable primitives.
