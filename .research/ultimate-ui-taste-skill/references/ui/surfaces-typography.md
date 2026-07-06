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

## Layout Detail

- Use stable dimensions for repeated controls, tiles, boards, and fixed-format panels.
- Avoid cards inside cards.
- Avoid decorative cards for page sections; use full-width bands or unframed layouts.
- Avoid decorative horizontal divider lines and background grids unless they serve grouping, measurement, or navigation.
- Use real product screenshots/assets when a user must inspect the product.
- Keep dashboards utilitarian: dense, aligned, and scannable.
