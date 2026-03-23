# Design Brief — Template

> This document is the "AI build spec". Feed it along with your PRD + UIDD to the AI tool.
> It combines WHAT to build (from PRD) with HOW it should look (from UIDD) into actionable instructions.

---

## 1. Project Context

**Product:** [Name — one-line description]
**Target users:** [Who uses this product]
**Design system status:** [New / Extending existing / Redesigning]

---

## 2. Tech Stack & Constraints

| Aspect | Value |
|--------|-------|
| Framework | [e.g., Next.js 14, App Router] |
| Styling | [e.g., Tailwind CSS v4] |
| Language | [e.g., TypeScript strict] |
| Fonts | [e.g., Inter (headings), System UI (body)] |
| Icons | [e.g., Lucide React] |
| Package Manager | [e.g., pnpm] |
| Build Tool | [e.g., Turbopack] |
| Component Location | [e.g., src/components/ds/] |
| Demo Location | [e.g., src/app/demo/design-system/] |

---

## 3. Token Definitions

> Copy from UIDD §2-4. These are the exact values the AI must use.

### Colors
```css
--color-brand-primary: #______;
--color-surface-page: #______;
--color-surface-card: #______;
--color-text-high-contrast: #______;
--color-text-muted: #______;
/* ... all tokens */
```

### Typography
```
Headings: [Font] — H1: __px bold, H2: __px bold, H3: __px semibold
Body: [Font] — Body: __px regular, Caption: __px regular
```

### Geometry
```
Radius: box=__px, btn=__px, chip=999px
Shadow: 0 4px 20px rgba(0,0,0,0.03)
```

---

## 4. Build Scope

### Phase/Sprint: [Name or number]

### Screens to Build
| # | Screen | Priority | Dependencies | Notes |
|---|--------|----------|-------------|-------|
| 1 | [Screen name] | P0 | None | [Any specific notes] |
| 2 | [Screen name] | P0 | Screen 1 (shared layout) | |
| 3 | [Screen name] | P1 | DS components from Phase 1 | |

### Components Needed
| # | Component | Level | Exists? | Action |
|---|-----------|-------|---------|--------|
| 1 | DsButton | Atom | ✅ Yes | No changes |
| 2 | [DsComponentName] | Molecule | ❌ No | Build new |
| 3 | DsSidebar | Organism | ✅ Yes | Extend variants |

---

## 5. Build Order

> Define the sequence. AI should follow this exactly.

```
Block 1: Tokens (Foundation)
  └─ CSS variables in globals.css
  └─ Tailwind config extensions (map vars to utility classes)
  └─ Font loading setup

Block 2: Atoms [~X components]
  └─ DsButton (primary, secondary, outline, ghost, danger)
  └─ DsInput (text, email, password)
  └─ DsCheckbox, DsRadio, DsToggle
  └─ DsBadge, DsChip, DsTag
  └─ → Build showcase section for Atoms

Block 3: Molecules [~X components]
  └─ DsFormField (atom: Input + Label + Error)
  └─ DsNavItem (atom: Button-like + Icon + Badge)
  └─ DsCard (atom: Surface + Typography + Badge)
  └─ → Build showcase section for Molecules

Block 4: Organisms [~X components]
  └─ DsSidebar (molecule: NavItem × N + Logo)
  └─ DsPageHeader (atom: Typography + molecule: Breadcrumbs)
  └─ → Build showcase section for Organisms

Phase 6: Screen Assembly
  └─ [Screen 1 name] — compose from Blocks 2-4
  └─ [Screen 2 name]
  └─ → Verify against PRD acceptance criteria
```

---

## 6. References & Inspiration

| Reference | URL/File | What to Borrow |
|-----------|----------|----------------|
| [Product name] | [URL or screenshot path] | [Specific patterns: layout, color approach, etc.] |
| [Product name] | [URL or screenshot path] | [What elements to reference] |

### What NOT to borrow
- [Pattern to avoid from Reference 1]
- [Feature that looks cool but is out of scope]

---

## 7. Quality Gates

Before declaring any Block complete:
- [ ] `npm run build` — zero TypeScript errors
- [ ] All components rendered on showcase page with all variants
- [ ] Visual verification in browser matches UIDD tokens
- [ ] No hardcoded colors, spacing, or typography values
- [ ] Responsive layout verified at mobile + desktop
- [ ] Components exported via barrel file

Before declaring a Screen complete:
- [ ] All components are from DS (Ds* prefix)
- [ ] Mock data is realistic (not Lorem ipsum)
- [ ] Loading, empty, error states exist
- [ ] PRD acceptance criteria met
- [ ] Screen classified: EXISTS (polish) or MISSING (build)

---

## 8. Constraints & Anti-Patterns

### DO NOT:
- Add features not in the PRD
- Create one-off styled components outside the DS
- Use hardcoded hex values
- Guess at missing specifications — flag as [GAP] and ask
- Write placeholder copy without marking as [DEMO COPY]

### ALWAYS:
- Trace every element back to PRD or UIDD section
- Mark unsourced decisions as [DESIGN DECISION — not in source docs]
- Extract BOTH paragraphs AND tables from .docx specs
- Use realistic mock data
- Test at mobile breakpoint

---

## 9. Delivery Checklist

- [ ] All Blocks complete with showcase sections
- [ ] All Screens assembled and verified
- [ ] Git: committed to [branch name]
- [ ] No TS errors, no lint warnings
- [ ] README updated with component list
- [ ] Ready for developer review/PR
