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
- Containers that add no grouping, hierarchy, comparison, interaction, or state.
- Repeated icon-card grids.
- Hero metric trio as filler.
- Beige/cream "tasteful" palette by reflex.
- Same spacing rhythm throughout the page.
- Stock-like atmospheric images where product proof is needed.
- Decorative horizontal lines between sections when spacing alone would separate them.
- Background grids or technical linework used as automatic decoration.
- Inconsistent font families or default-looking bold text inside small cards.
- A set of cards where every item has the same shape, same icon position, same metric treatment, and no distinct product artifact.
- Initials used as icons, such as two-letter tiles for people, products, vendors, or features.
- Generic glyphs where a recognizable entity needs a real mark, product screenshot, seal, file type, or domain-specific artifact.

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
- Pulsing "live" dots on static content.
- Auto-refresh, online, connected, verified, or all-healthy motion when there is no real live state.

## Authenticity Tells

Reject or reframe:

- Fake hostnames, IP addresses, ticket IDs, incident IDs, user IDs, or environment names invented only to look technical.
- Fake live counts such as "3 healthy / 2 issues" when the page is not connected to data.
- Static mockups that claim "Live", "Online", "Verified", "Auto-refresh", or "All healthy" without a real source or state.
- Security, compliance, finance, or operations dashboards that show decorative status theater instead of a real artifact: incident timeline, health board, SLA gauge, audit log, queue, comparison table, policy matrix, topology, or source coverage.

Allowed:

- Representative aggregate numbers when the UI clearly frames them as sample, demo, forecast, or placeholder data.
- Plausible product states when they support the workflow and are not pretending to be live infrastructure.
- Real logos or marks only when their license and context allow use. Otherwise use text labels, file badges, product screenshots, or neutral domain artifacts.

Rule: invented specificity is worse than honest abstraction.

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
Wrong: Shipping - no issue, if the separator is only decorative.
Better: Shipping: no issue.
Better: Shipping, no issue.
```

Use concrete product language:

```text
Weak: Supercharge your workflow with AI.
Better: Review agent-built interfaces before they ship.
```

## Structural Tells

Container slop is not fixed by changing the radius. Remove a box when spacing, alignment, a list, a table, an inline row, a sidebar, a timeline, or an unframed section communicates the structure more clearly. Keep a container when it creates a real region, interaction boundary, comparison unit, or stateful surface.

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

## Concept Tells

Restyling does not fix a weak concept. Before changing palette, radius, shadows, or animation, ask what the surface should honestly show.

Weak:

```text
Three identical cards with icons and vague statuses.
```

Better:

```text
One incident timeline, one SLA gauge, and one health board because each answers a different operational question.
```

Rule: if the component is trying to look important but does not change what the user can decide, replace the concept.

## Collection Variety

When a page shows multiple proof cards, dashboard modules, or product previews, vary the archetype by job:

- Status page: uptime, outage state, region, affected service.
- Incident timeline: timestamp, actor, event, resolution.
- Health board: system, status, owner, last check.
- SLA gauge: target, actual, breach risk, time window.
- Comparison table: rows, tradeoffs, decision criteria.
- Queue: priority, assignee, age, next action.
- Audit log: event, actor, source, evidence.
- Topology or beam diagram: relation, path, dependency, direction.

If three cards share the same visual grammar, check whether the product actually has three different concepts or just one repeated template.

## Audit Questions

1. Could this screen belong to any startup?
2. Does the first viewport show the product/workflow or only claims?
3. Is any card decorative rather than functional?
4. Are icons doing semantic work or just filling space?
5. Would removing the gradient make the hierarchy collapse?
6. Is motion explaining a state change or merely decorating?
7. Would removing decorative lines make the layout cleaner?
8. Does any text look like browser-default bold rather than an intentional type style?
9. Could a broad selector such as `.card span` or `.row strong` accidentally style semantic copy as decoration?
10. Is any data pretending to be live, connected, verified, or operational without a real source?
11. Are repeated modules using the same card shape because it is correct, or because no better archetype was chosen?
12. Could the same layout belong to any other product with only text swapped?
