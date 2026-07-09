# Surfaces, Typography, Color, And Detail

Use this reference for visual polish, spacing, type, cards, panels, image edges, and general UI taste.

## Typography

```css
html {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

h1,
h2,
h3 {
  text-wrap: balance;
}

p,
li,
figcaption {
  text-wrap: pretty;
}

.tabular {
  font-variant-numeric: tabular-nums;
}
```

Rules:

- Use `text-wrap: balance` for headings and short hero copy.
- Use `text-wrap: pretty` for short-to-medium body text.
- Use tabular numbers for changing counters, prices, timers, scores, dashboard values, and table numeric columns.
- Avoid wide letter spacing on body text.
- Avoid tiny text in dashboards unless it is secondary metadata.
- Avoid browser-default-looking `strong` and `small` pairings in cards. Style title, metadata, and secondary text deliberately with a shared font family, clear line-height, and restrained weights.
- Do not use emojis or em dashes in UI copy unless the user explicitly asks for them.
- Define a small type scale per surface before styling details. For example: page title, section title, card title, label, metadata, body, numeric value.
- Keep font families consistent inside a product surface. Use weight, size, color, and spacing for hierarchy before introducing another font.
- Avoid arbitrary weight jumps. Prefer a restrained set such as 400, 500, 600 or 650, and 700 for compact product UI.
- Do not rely on raw `strong`, `small`, `span`, or `b` defaults for hierarchy. Give repeated roles named classes or slots.
- Test long labels and metadata. Text should wrap or truncate intentionally without changing card height unexpectedly.

## Concentric Radius

Correct nested radius:

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

Rule: `outer radius = inner radius + padding` when surfaces are close together.

## Shadows As Borders

For elevated cards, buttons, and panels:

```css
.surface {
  box-shadow:
    0 0 0 1px rgb(0 0 0 / 0.06),
    0 1px 2px -1px rgb(0 0 0 / 0.06),
    0 2px 4px rgb(0 0 0 / 0.04);
  transition: box-shadow 150ms cubic-bezier(0.23, 1, 0.32, 1);
}
```

Keep real borders for dividers, inputs, tables, and explicit separation.

## Image Outlines

```tsx
<img
  className="outline outline-1 -outline-offset-1 outline-black/10 dark:outline-white/10"
  src={src}
  alt={alt}
/>
```

Use pure black/white opacity for image outlines. Do not use tinted slate/zinc/brand outlines.

## Color Discipline

Avoid one-note palettes. A good palette usually has:

- A neutral foundation.
- One primary action color.
- One or two semantic/status colors.
- Enough contrast for text and controls.
- A reason for warmth, darkness, vibrancy, or restraint.

Do not default to purple-blue gradients, beige "premium" pages, or cyan-on-dark "AI" surfaces.

When creating a new palette, prefer perceptual color decisions over hand-picked hex ramps. OKLCH is a good default when the project supports it: keep hue stable across ramps, adjust lightness first to fix contrast, clamp high chroma to the target gamut, and avoid dark-mode colors that are unrelated to the light palette. If the project already uses hex, RGB, HSL, or named tokens, preserve the local format unless changing it is part of the task.

## Layout Detail

- Use stable dimensions for repeated controls, tiles, boards, and fixed-format panels.
- Avoid cards inside cards.
- Avoid decorative cards for page sections; use full-width bands or unframed layouts.
- Avoid decorative horizontal divider lines and background grids unless they serve grouping, measurement, or navigation.
- Use real product screenshots/assets when a user must inspect the product.
- Keep dashboards utilitarian: dense, aligned, and scannable.
- Use a deliberate spacing scale. Related items should share tighter gaps than unrelated groups.
- Avoid one repeated gap everywhere. Pages need different spacing for item gaps, group gaps, section gaps, and viewport margins.
- Align text, controls, and data edges. A polished UI often comes from clean alignment more than decoration.
- Align optically when geometry looks wrong. Icons, play triangles, asymmetric glyphs, and icon-plus-text buttons may need adjusted padding, margin, or SVG viewBox so they feel centered.
- In icon-plus-text buttons, reduce the padding on the icon side only when the icon's visual weight makes the content look off-center.
- Fit diagrams to their containers. Beams, connector lines, gauges, charts, topology maps, and timelines should use container-relative units, stable aspect ratios, and bounded line lengths.
- Never let a visual proof overflow a fixed-height card. Increase the card height, simplify the diagram, or change the archetype.
- Give mobile views a real layout, not a shrunken desktop diagram. Use stacked timelines, compact lists, simplified gauges, or horizontal scroll with a visible affordance.
- Check sets together. Repeated cards can look acceptable one by one and still fail as a monotonous collection.

```css
.button-with-icon {
  gap: 8px;
  padding-inline: 14px 16px;
}

.button-with-icon svg {
  margin-left: -1px;
}
```

Use these adjustments only after checking the rendered result. Optical alignment is a correction, not a default decoration.

## Selector Safety

Use semantic slots for mixed content:

```tsx
<span className="workflow-dot" aria-hidden="true" />
<b className="workflow-status">Shipping</b>
```

Avoid broad descendant styling:

```css
.workflow li span {
  width: 9px;
  height: 9px;
  border-radius: 50%;
  background: green;
}
```

Why: broad selectors can turn real text into decorative shapes when markup changes. Scope decorative rules to named classes such as `.workflow-dot`, `.status-pill`, `.icon`, or `[data-slot="indicator"]`.
