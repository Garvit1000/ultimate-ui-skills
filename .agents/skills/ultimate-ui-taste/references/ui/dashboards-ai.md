# Dashboards And AI Product Screens

Use this reference for SaaS, admin tools, analytics dashboards, agent consoles, and AI chat/workbench interfaces.

## Dashboard Taste

Dashboards should feel operational, not like landing pages.

Prioritize:

- Dense but readable information.
- Clear grouping and alignment.
- Tables/lists when comparison matters.
- Filters and controls that look like controls.
- Metrics with trend, denominator, time window, and caveat when relevant.
- Empty/loading/error/permission states.
- Stable layouts that do not shift when values change.

Avoid:

- Oversized hero sections.
- Decorative metric cards with no decision value.
- Random illustrations.
- Gradient backgrounds.
- Repeated card grids when a table would scan better.
- Tiny low-contrast labels.
- Fake live status badges, pulsing dots, auto-refresh labels, or invented operational data.
- Three or more modules with the same card shape when they represent different decisions.

## Product Surface Archetypes

Pick the archetype that matches the user decision. Do not default to metric cards or icon rows.

| User needs to know | Strong archetype | Weak substitute |
| --- | --- | --- |
| What happened and when | Incident timeline or audit log | A static "recent activity" card with icons |
| Whether the system is healthy | Health board or status page | "All systems online" badge |
| Whether a target is at risk | SLA gauge with target and window | Big percentage with no denominator |
| What needs action | Queue with priority, age, owner, next step | Three generic task cards |
| What changed across groups | Table, matrix, or comparison view | Repeated feature cards |
| What depends on what | Topology, beam, graph, or dependency map | Decorative connected lines |
| Whether sources are trustworthy | Source coverage panel | "Verified" pill |

Use different archetypes across a set when the concepts differ. A landing page may show several product previews, but each preview should prove a different capability or decision.

## Honest Data And Status

Operational UI can use sample data, but it must be honest about its role.

Good:

- "Sample incident timeline"
- "Last 7 days"
- "12 of 18 checks passing"
- "Representative workspace"
- "Demo data"

Bad:

- Fake hostnames, IP addresses, or ticket IDs invented to look real.
- "Live", "Online", "Auto-refresh", "Verified", or "All healthy" on static mockups.
- Ticking counters without a real source.
- Compliance or security claims without evidence or context.

## Metric Card Requirements

Good metric:

```tsx
<MetricCard
  label="Activation rate"
  value="42.8%"
  delta="+3.1 pp"
  window="Last 7 days"
  denominator="2,184 eligible users"
  status="above target"
/>
```

Weak metric:

```tsx
<Card>
  <p>Growth</p>
  <h2>+128%</h2>
</Card>
```

Why: the weak metric lacks definition, time window, denominator, and decision context.

## AI Workbench Requirements

Agent/UI screens need visible system state:

- Current task or objective.
- Input composer with attachments/tool affordances.
- Message turns with user/assistant distinction.
- Tool calls and results.
- Reasoning or progress when appropriate.
- Citations/sources for claims.
- Feedback controls.
- Retry, edit, stop, continue, and copy actions.
- Error recovery and rate-limit states.

## AI Component Structure

```tsx
<Thread>
  <Message from="user">
    <MessageContent />
    <MessageActions />
  </Message>
  <Message from="assistant">
    <Reasoning />
    <ToolCall />
    <CitationList />
    <MessageContent />
    <FeedbackBar />
  </Message>
  <PromptInput />
</Thread>
```

This is better than a single chat bubble list because it can grow with product behavior.

## Responsive Product Layout

- Preserve primary actions above the fold.
- Collapse navigation intentionally; do not hide essential state.
- Tables need mobile alternatives: compact rows, column picker, horizontal scroll with visible affordance, or summary cards.
- Avoid text overlap by setting min/max widths and allowing wrapping.
- Do not scale font size with viewport width.
- Size diagrams, beams, gauges, and charts with container-relative dimensions. They must not overflow fixed-height cards.
- Give mobile states a minimum usable height and a simpler layout instead of shrinking complex diagrams until they break.
