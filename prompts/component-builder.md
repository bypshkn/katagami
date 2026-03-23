# Katagami Prompt — Component Builder

> Use this prompt when building individual components within an existing design system session.

---

```
Build the following component for the design system. Follow these rules exactly:

## Component Requirements
- **Name:** Ds{ComponentName}
- **Level:** {Atom | Molecule | Organism}
- **Composed from:** {list parent Ds components used}

## Implementation Rules

### TypeScript
- Define `{ComponentName}Props` interface with explicit types
- No `any` type. Ever.
- Explicit return type on the component function
- All optional props have default values

### Styling
- Use ONLY CSS variables from `globals.css` (tokens)
- Zero hardcoded hex values, pixel values for spacing, or font sizes
- Use Tailwind utility classes that reference the token system
- Responsive: mobile-first, breakpoints at sm/md/lg/xl

### Variants
- Express ALL variants through props (not separate components)
- Include: size (sm/md/lg), variant (primary/secondary/outline/ghost), state (default/hover/disabled/active/error)
- Use discriminated unions for mutually exclusive variants

### Accessibility
- Include `aria-label` where applicable
- Respect `prefers-reduced-motion` for animations
- Keyboard navigation support
- Color contrast minimum: 4.5:1 for text, 3:1 for large text

### File Structure
```tsx
// src/components/ds/{level}/Ds{ComponentName}.tsx

import React from 'react';

export interface Ds{ComponentName}Props {
  // ... typed props
}

export const Ds{ComponentName}: React.FC<Ds{ComponentName}Props> = ({
  // ... destructured with defaults
}) => {
  return (
    // ... JSX
  );
};

export default Ds{ComponentName};
```

### Showcase Section
After building the component, add a showcase section to the demo page:
```tsx
{/* ── Ds{ComponentName} ─────────────────────────── */}
<section className="space-y-4">
  <h2 className="text-2xl font-bold">Ds{ComponentName}</h2>
  <p className="text-sm text-text-muted">Level: {level} | Composed from: {parents}</p>
  <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
    {/* Default */}
    <Ds{ComponentName} />
    {/* Size variants */}
    <Ds{ComponentName} size="sm" />
    <Ds{ComponentName} size="lg" />
    {/* State variants */}
    <Ds{ComponentName} disabled />
    {/* Theme variants */}
    <Ds{ComponentName} variant="secondary" />
  </div>
</section>
```

### Barrel Export
Add to `src/components/ds/index.ts`:
```tsx
export { Ds{ComponentName} } from './{level}/Ds{ComponentName}';
export type { Ds{ComponentName}Props } from './{level}/Ds{ComponentName}';
```

## Quality Gate
Before declaring done:
- [ ] `npm run build` — zero TS errors
- [ ] Showcase renders all variants
- [ ] Browser visual check passed
- [ ] Colors = tokens only (no hex)
- [ ] Typography = scale classes only (no arbitrary px)
- [ ] Spacing = token system (no magic numbers)
- [ ] Exported via barrel file
- [ ] Props documented via TypeScript interface

Now build the component.
```
