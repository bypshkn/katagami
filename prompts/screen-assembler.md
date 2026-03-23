# Katagami Prompt — Screen Assembler

> Use this prompt when composing full pages/screens from existing DS components.

---

```
You are assembling a production screen using ONLY existing Design System components. Do not create one-off UI elements.

## Assembly Rules

### 1. COMPONENTS ONLY
- Use ONLY `Ds*` prefixed components from the design system
- If a needed component doesn't exist — STOP and flag it as a gap
- Do NOT create inline styled divs that replicate DS component behavior
- Do NOT add features/fields not specified in the screen's task spec

### 2. DATA REQUIREMENTS
- Use realistic mock data — names, numbers, dates that look real
- Never use "Lorem ipsum", "John Doe #1", or placeholder sequences
- Derive data structure from PRD/SRS data models
- Mark any invented data as [DEMO DATA]

### 3. LAYOUT COMPOSITION
Screen structure should follow:
```
<DsPageContainer>
  <DsPageHeader title="..." breadcrumbs={[...]} />

  <main className="space-y-6">
    {/* KPI row (if applicable) */}
    <DsKpiPanel items={[...]} />

    {/* Primary content */}
    <section className="grid grid-cols-1 md:grid-cols-2 gap-6">
      {/* DS Organisms compose the main view */}
    </section>

    {/* Secondary content / tables / lists */}
  </main>
</DsPageContainer>
```

### 4. RESPONSIVE STRATEGY
- Mobile: single column, full-width cards, stacked KPIs
- Tablet: 2-column grid, side-by-side where appropriate
- Desktop: full layout with sidebar visible
- Touch targets: minimum 44px on mobile

### 5. INTERACTIVE STATES
Every screen must handle:
- **Loading:** Skeleton placeholders using DS skeleton components
- **Empty:** Empty state with illustration + CTA
- **Error:** Error boundary with retry action
- **Populated:** Normal state with real data

### 6. NAVIGATION INTEGRATION
- Sidebar active state matches current page
- Breadcrumbs reflect page hierarchy
- Page title matches sidebar label

### 7. VERIFICATION CHECKLIST
After assembling the screen:
- [ ] All components are from DS (Ds* prefix)
- [ ] No hardcoded colors/spacing/typography
- [ ] Mock data is realistic
- [ ] Responsive layout tested at 3 breakpoints
- [ ] Loading, empty, error, populated states exist
- [ ] Screen matches PRD acceptance criteria
- [ ] Sidebar shows correct active state

### 8. SPEC REFERENCE FORMAT
At the top of the page file, add a comment:
```tsx
/**
 * Screen: {Screen Name}
 * Spec: PRD §{section}, Task {T.X.X}
 * DS Components used: DsPageHeader, DsKpiPanel, DsStatusBadge, ...
 * Status: {Draft | Review | Production}
 */
```

Now assemble the screen based on the spec provided.
```
