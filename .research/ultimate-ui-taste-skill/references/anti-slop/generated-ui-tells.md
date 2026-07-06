# Generated UI Slop Tells

Use this reference when a UI feels generic, AI-generated, too template-like, or superficially polished.

## Visual Tells

Reject or justify:

- Purple/blue gradients by default.
- Cyan-on-dark "AI app" palette.
- Gradient text on headings, metrics, or CTA labels.
- Glassmorphism cards without material logic.
- Random glow, blur, or bokeh backgrounds.
- Oversized rounded cards everywhere.
- Cards inside cards.
- Repeated icon-card grids.
- Hero metric trio as filler.
- Beige/cream "tasteful" palette by reflex.
- Same spacing rhythm throughout the page.
- Stock-like atmospheric images where product proof is needed.
- Decorative horizontal lines between sections when spacing alone would separate them.
- Background grids or technical linework used as automatic decoration.
- Inconsistent font families or default-looking bold text inside small cards.

## Motion Tells

Reject or justify:

- Bouncy/elastic motion on normal business UI.
- Hover scale on every card.
- Image zoom on hover when inspection is not the purpose.
- Slow dropdowns.
- `ease-in` entrances.
- `transition: all`.
- Layout property animation.
- Page-load animation on elements that should be stable.
- Keyboard-triggered animation.

## Copy Tells

Avoid:

- Supercharge
- Empower
- Streamline
- Seamless
- Unlock potential
- World-class
- Enterprise-grade
- Revolutionize
- Effortlessly
- Emojis unless the user explicitly asks for them.
- Em dashes in UI copy, documentation, labels, or generated content unless the user explicitly asks for them.

Use plain punctuation:

```text
Wrong: Shipping - no issue.
Better: Shipping: no issue.
Better: Shipping - no issue.
```

Use concrete product language:

```text
Weak: Supercharge your workflow with AI.
Better: Review agent-built interfaces before they ship.
```

## Structural Tells

Weak AI page:

```tsx
<Hero />
<ThreeStats />
<FeatureCards />
<Testimonials />
<CTA />
```

Better page:

```tsx
<HeroWithProductProof />
<PrimaryWorkflow />
<LiveExample />
<DecisionDashboard />
<PricingOrAdoptionPath />
```

## Audit Questions

1. Could this screen belong to any startup?
2. Does the first viewport show the product/workflow or only claims?
3. Is any card decorative rather than functional?
4. Are icons doing semantic work or just filling space?
5. Would removing the gradient make the hierarchy collapse?
6. Is motion explaining a state change or merely decorating?
7. Would removing decorative lines make the layout cleaner?
8. Does any text look like browser-default bold rather than an intentional type style?
