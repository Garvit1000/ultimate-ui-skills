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
