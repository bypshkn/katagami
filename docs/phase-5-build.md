# Phase 5: Build the Design System

> This is where code gets written. You feed the Design Brief + UIDD to an AI tool and build components layer by layer.

---

## Prerequisites

Before starting Phase 5, you must have:
- [ ] PRD finalized (Phase 1)
- [ ] Visual references collected (Phase 2)
- [ ] UIDD written with ALL tokens defined (Phase 3)
- [ ] Design Brief prepared (Phase 4)
- [ ] Project initialized (Next.js/React + Tailwind + TypeScript)
- [ ] Git branch created for DS work

---

## Session Strategy: Momentum Over Perfection

This is the most important operational advice in the entire methodology.

**AI tools degrade over long sessions.** Context gets saturated, instructions get ignored, hallucinations increase. Your job is to maximize output while the AI is "fresh."

### The Rules

1. **One session = one Block.** Build all Atoms in one session. Start fresh for Molecules. Don't try to build the entire DS in one mega-session.

2. **While it's generating well — don't stop.** If the AI is producing good components, keep pushing. Note minor issues (padding off by 4px, wrong shade of grey) but don't interrupt the flow. Fix them in a polish pass later.

3. **Better 80% of 10 screens than 100% of 2.** Broad strokes first. Get all screens to "looks right at arm's length" before any pixel-perfect work.

4. **Batch corrections.** After a build session, review everything and collect fixes into a list. Then run a dedicated fix session with ONLY the fix list — no new features.

5. **Know when to restart.** If the AI starts ignoring your DS tokens, inventing components, or producing inconsistent output — don't fight it. Start a new session with fresh context. Copy-paste only the relevant tokens and the specific task.

6. **Polish is Phase 6.5.** After all screens exist (Phase 6), do a dedicated polish pass. This is where the Design Reviewer prompt shines — systematic QA with a fresh context.

### Session Template

```
Session 1: Tokens + Atoms (Block 1)       → commit
Session 2: Core Molecules (Block 2)        → commit
Session 3: Complex Molecules (Block 3)     → commit
Session 4: Organisms (Block 4)             → commit
Session 5-N: Screen Assembly (1-3 screens per session) → commit each
Session N+1: Polish pass (review + batch fixes)        → commit
```

---

## Step 1: Initialize Tokens

Create your token layer first. Everything else depends on it.

**File: `globals.css` (or `tokens.css`)**
```css
:root {
  /* Paste ALL tokens from UIDD §2-4 here */
  /* Colors, spacing, radius, shadows, etc. */
}
```

**File: `tailwind.config.ts`**
```ts
// Extend Tailwind with your tokens
// Map CSS variables to Tailwind utility classes
```

**File: `src/fonts/` setup**
```ts
// Load fonts via next/font/local (or your framework's method)
// Export font class names for use in layout
```

**Verification:** Create a minimal page that displays all tokens visually — color swatches, type samples, spacing rulers.

---

## Step 2: Build Atoms

Atoms are indivisible elements. Build them ALL before moving to molecules.

### Typical Atom Set
| Component | Variants | Priority |
|-----------|----------|----------|
| DsButton | primary, secondary, outline, ghost, danger × sm, md, lg | P0 |
| DsInput | text, email, password, number, textarea | P0 |
| DsCheckbox | standard, indeterminate | P0 |
| DsRadio | standard | P0 |
| DsToggle | standard | P1 |
| DsBadge | default, success, warning, danger, info | P0 |
| DsChip | default, removable, selectable | P1 |
| DsTag | color-coded | P1 |
| DsLink | inline, standalone | P0 |
| DsIcon | wrapper for icon library (sizing, coloring) | P0 |

### AI Prompt Pattern for Atoms
```
Build [DsButton] as a design system Atom.

Token source: [paste relevant UIDD section]
Variants: primary, secondary, outline, ghost, danger
Sizes: sm (32px height), md (40px), lg (48px)
States: default, hover, active, disabled, loading

Requirements:
- TypeScript strict, no `any`
- All colors via CSS variables
- Export props interface
- Add to showcase page after building
```

### Showcase After Atoms
Create `/demo/design-system/page.tsx` with a section per atom showing all variants and states in a grid.

---

## Step 3: Build Molecules

Molecules combine 2-3 atoms into functional units.

### Typical Molecule Set
| Component | Composed From | Purpose |
|-----------|--------------|---------|
| DsFormField | DsInput + Label + Error | Form input with validation |
| DsNavItem | DsIcon + Label + DsBadge | Sidebar link |
| DsPageHeader | Typography + DsBadge + Breadcrumbs | Page top section |
| DsCard | Surface + Typography + DsBadge | Content container |
| DsSearchBar | DsInput + DsButton | Search interface |

### AI Prompt Pattern for Molecules
```
Build [DsFormField] as a design system Molecule.

Composed from: DsInput (atom), Label text, Error text
Props: label, type, value, onChange, error, required, disabled, helperText
Behavior: Error shows below input in red when provided. Label floats or stays above.

Use ONLY existing Ds atoms. Do not create new base elements.
If a needed atom doesn't exist, flag it as [GAP].
```

---

## Step 4: Build Organisms

Organisms are complex blocks that compose DIFFERENT molecule types.

### The Organism Rule
An organism MUST pass this test:
1. Does it compose multiple DIFFERENT molecule types? → Yes = organism
2. Does it add layout logic OR state management? → Yes = organism
3. Is it just `items.map(molecule)`? → Yes = THIN WRAPPER → **DELETE IT**

### Typical Organism Set
| Component | Composed From | Layout Logic |
|-----------|--------------|-------------|
| DsSidebar | DsNavItem × N + Logo + Role selector | 3 states: full (240px), compact (88px), collapsed (64px) |
| DsKpiPanel | DsCard + DsStatusBadge + DsChip | Responsive grid, 2-4 columns |
| DsDashboardNavPanel | DsNavItem + DsIndicator | Tab-style navigation with active indicator |

### AI Prompt Pattern for Organisms
```
Build [DsSidebar] as a design system Organism.

Composed from: DsNavItem (molecule) × N, Logo, DsBadge (atom)
States: full (240px), compact (88px), collapsed (64px)
Active indicator: 4px left bar + background tint (full), pill (compact), icon tint (collapsed)
Role-based: different nav items per role (Employee, Manager, HR, Executive)

Layout logic: Collapsible via toggle button. Transitions between states.
State management: activeScreen prop, collapsed prop.

This is a REAL organism because:
- Composes NavItems + Logo + RoleSelector (different molecules)
- Adds collapse/expand state management
- Has responsive layout logic (not just a list)
```

---

## Step 5: Showcase-Driven Validation

After each Block, verify on the showcase page:

### Showcase Structure
```
/demo/design-system
├── Block 1: Tokens — Color swatches, type samples, spacing rulers
├── Block 2: Atoms — All atoms with all variants
├── Block 3: Molecules — All molecules with all variants
└── Block 4: Organisms — All organisms with all states
```

### Validation Checklist Per Block
- [ ] All components render without errors
- [ ] `npm run build` passes with zero TS errors
- [ ] Colors match UIDD tokens exactly
- [ ] Typography uses defined scale
- [ ] Spacing follows grid system
- [ ] Components look correct at 375px (mobile) and 1440px (desktop)
- [ ] Interactive states visible (hover, active, disabled)

---

## Common Problems & Solutions

| Problem | Cause | Fix |
|---------|-------|-----|
| Colors look "off" | Hardcoded hex instead of CSS variable | Find-replace all hex values with `var(--color-*)` |
| Body text too grey | Used `text-muted` for body text | Body = `text-high-contrast`. Only meta/timestamps = muted |
| Cards stretch to equal height | Default grid behavior | Add `items-start` to grid container |
| Organism is a thin wrapper | Just `items.map(molecule)` | Delete it. Use the molecule directly in pages |
| Showcase broken after deletion | Component numbering off | Renumber showcase sections after any deletion |
| Git commit fails | virtiofs mount limitation | Use git worktree on local disk |

---

## File Boundary Discipline

Only touch these directories in DS branch:
```
src/components/ds/    ← Component code
src/app/demo/         ← Showcase pages
globals.css           ← Token definitions (carefully)
tailwind.config.*     ← Token extensions (carefully)
```

**Why?** Other developers work in `src/app/`, `src/lib/`, `src/api/`. Staying within DS boundaries guarantees zero merge conflicts.

---

## Git Discipline

### Commit Convention
```
feat(ds): add date picker molecule — 3 variants
fix(ds): correct status badge colors per UIDD §4.2
refactor(ds): remove thin wrapper organisms
chore(ds): update showcase page layout
```

### Commit Frequency
- After completing each Block (tokens, atoms, molecules, organisms)
- After fixing a batch of review issues
- Before ending any work session

### Branch Strategy
```
main → dev → concept/design-system
```
DS changes live in `concept/design-system`. Merge to `dev` via PR review.
