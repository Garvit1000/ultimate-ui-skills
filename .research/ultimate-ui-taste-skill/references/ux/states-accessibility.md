# UX States, Accessibility, And Resilience

Use this reference before shipping product UI, dashboards, forms, navigation, overlays, and AI workbenches.

## State Checklist

Every meaningful component or screen should define:

- Default
- Hover/focus/active
- Loading
- Empty
- Error
- Success
- Disabled
- Permission denied
- Long content
- Mobile
- Reduced motion

## Accessibility Rules

- Links navigate; buttons perform actions.
- Icon-only buttons need `aria-label`.
- Inputs need labels, not only placeholders.
- Menus, dialogs, comboboxes, and tooltips should use proven primitives where possible.
- Focus must be visible through `:focus-visible`.
- The user must be able to complete the main workflow by keyboard.
- Do not disable browser zoom.
- Keep touch targets at least 40x40px, preferably 44x44px.
- Announce async updates with appropriate live regions when needed.

## Loading

Wrong:

```tsx
<button disabled>{loading ? <Spinner /> : "Save"}</button>
```

Right:

```tsx
<button disabled={loading} aria-busy={loading}>
  {loading ? <Spinner aria-hidden="true" /> : null}
  <span>Save</span>
</button>
```

Why: preserving the label keeps intent visible while loading.

## Empty States

Empty states should answer:

1. What happened?
2. Why is it empty?
3. What can the user do next?

```tsx
<EmptyState
  title="No reviews yet"
  description="Reviews will appear here after an agent submits an interface for critique."
  action={<Button>Run first review</Button>}
/>
```

## Long Content And Localization

Test with:

- Long names.
- Long German-like strings.
- Very large numbers.
- Multiple lines in buttons/cards.
- Missing images.
- Time zones and date formats.

Use wrapping, truncation, tooltips, and stable dimensions intentionally.

## URL And App State

For dashboards and tools, keep shareable state in the URL when useful:

- Search query
- Filters
- Active tab
- Pagination
- Selected entity
- Expanded panel

Avoid losing the user’s working state on refresh.
