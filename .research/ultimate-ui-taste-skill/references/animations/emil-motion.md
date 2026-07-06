# Animation And Motion Taste

Use this reference for motion systems, transitions, gestures, popovers, drawers, toasts, hover states, icon swaps, loaders, and animation reviews.

## Motion Decision Framework

Before writing animation code, answer:

1. How often will the user see this?
2. Did the user initiate it with keyboard?
3. What is the purpose: feedback, state indication, spatial continuity, explanation, or softening a jarring change?
4. Is this interactive and interruptible, or a staged one-shot sequence?

| Frequency | Decision |
| --- | --- |
| Hundreds/day | No animation, especially keyboard actions |
| Tens/day | Minimal motion only |
| Occasional | Standard UI motion |
| Rare/first-time | Delight is allowed if it supports the story |

## Easing And Duration

```css
:root {
  --ease-out-strong: cubic-bezier(0.23, 1, 0.32, 1);
  --ease-in-out-strong: cubic-bezier(0.77, 0, 0.175, 1);
  --ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);
  --ease-icon: cubic-bezier(0.2, 0, 0, 1);
}
```

| Motion | Duration |
| --- | --- |
| Button press | 100-160ms |
| Tooltip/popover | 125-200ms |
| Dropdown/select | 150-250ms |
| Modal/drawer | 200-500ms |
| Marketing explanation | Longer only when useful |

Avoid `ease-in` for normal UI entrance. It hides movement at the moment users are watching.

## Right: Origin-Aware Popover

```css
.popover-content {
  transform-origin: var(--radix-popover-content-transform-origin);
  opacity: 1;
  transform: scale(1) translateY(0);
  transition:
    opacity 160ms var(--ease-out-strong),
    transform 160ms var(--ease-out-strong);
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

Why: popovers are anchored to triggers; `scale(0)` appears from nowhere; `ease-in` feels delayed; `transition: all` is imprecise.

## Right: Press Feedback

```css
.button {
  transition: transform 150ms var(--ease-out-strong);
}

.button:active {
  transform: scale(0.96);
}
```

Use a static/no-motion variant for controls where press scale would distract.

## Right: Contextual Icon Swap

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

Why: instant icon swapping looks mechanical. Keeping both icons in the DOM creates smooth enter and exit motion without a new dependency.

## Gestures And Drawers

Use direct transforms during drag:

```tsx
function onDrag(distance: number, drawer: HTMLElement) {
  drawer.style.transform = `translateY(${Math.max(distance, 0)}px)`;
}
```

Avoid inherited CSS variable updates during high-frequency gestures:

```tsx
drawer.style.setProperty("--swipe-amount", `${distance}px`);
```

Add velocity-based dismissal. A fast flick should dismiss even when distance is below threshold.

## Reduced Motion

Reduced motion means less movement, not broken state communication:

```tsx
const shouldReduceMotion = useReducedMotion();

const variants = {
  hidden: shouldReduceMotion ? { opacity: 0 } : { opacity: 0, y: 16, filter: "blur(4px)" },
  visible: shouldReduceMotion ? { opacity: 1 } : { opacity: 1, y: 0, filter: "blur(0px)" },
};
```

## Review Checklist

- No animation for keyboard-triggered frequent actions.
- No `transition: all`.
- No `scale(0)` entrances.
- Popovers use trigger origin; modals stay centered.
- Enter/exit durations are asymmetric when needed.
- Transitions are used for interruptible UI; keyframes are reserved for staged one-shot sequences.
- Motion is removed or softened under `prefers-reduced-motion`.
