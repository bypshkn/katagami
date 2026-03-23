# UI Design Description (UIDD) — Template

> Fill this template to describe your design language. Feed it to the AI along with the PRD.
> Every value must be EXPLICIT — no "use your judgment" placeholders.

---

## 1. Design Philosophy

**Visual direction:** [Describe in 2-3 sentences. E.g., "Clean, corporate, data-forward. Trustworthy navy palette with warm coral accents. Minimal decorative elements — data is the hero."]

**Inspiration:** [List 2-3 reference products/sites with what you borrowed from each]

**Anti-patterns:** [List 2-3 things you explicitly do NOT want. E.g., "No gamification aesthetics. No neon colors. No rounded cartoon illustrations."]

---

## 2. Color Tokens

### Brand Colors
| Token Name | Hex | Usage |
|-----------|-----|-------|
| `--color-brand-primary` | #______ | Primary actions, active states, sidebar accent |
| `--color-brand-secondary` | #______ | Secondary buttons, hover states |

### Surface Colors
| Token Name | Hex | Usage |
|-----------|-----|-------|
| `--color-surface-page` | #______ | Page background |
| `--color-surface-card` | #______ | Card backgrounds |
| `--color-surface-elevated` | #______ | Dropdowns, modals, tooltips |
| `--color-surface-mystic` | #______ | Hero sections, special areas |

### Text Colors
| Token Name | Hex | Usage |
|-----------|-----|-------|
| `--color-text-high-contrast` | #______ | Headings, body text, primary labels |
| `--color-text-muted` | #______ | Secondary text, timestamps, meta info |
| `--color-text-inverted` | #______ | Text on dark backgrounds |

### Status Colors (if applicable)
| Token Name | Hex | Usage |
|-----------|-----|-------|
| `--color-status-success` | #______ | Positive states, completion |
| `--color-status-warning` | #______ | Caution states |
| `--color-status-danger` | #______ | Error states, critical alerts |
| `--color-status-info` | #______ | Informational states |

### Score Band Colors (if applicable)
| Band | Hex | Range |
|------|-----|-------|
| Thriving | #______ | 80-100 |
| Strong | #______ | 60-79 |
| Developing | #______ | 40-59 |
| At Risk | #______ | 20-39 |
| Critical | #______ | 0-19 |
| N/A | #______ | Insufficient data |

---

## 3. Typography

### Font Families
| Role | Font | Source |
|------|------|--------|
| Headings | [Font Name] | [Google Fonts / Local / CDN] |
| Body | [Font Name] | [Google Fonts / Local / CDN] |
| Code/Mono | [Font Name] | [Google Fonts / Local / CDN] |

### Type Scale
| Level | Size | Weight | Line Height | Usage |
|-------|------|--------|-------------|-------|
| H1 | __px | Bold (700) | 1.2 | Page titles |
| H2 | __px | Bold (700) | 1.3 | Section headers |
| H3 | __px | Semi-bold (600) | 1.3 | Card titles, subsections |
| H4 | __px | Semi-bold (600) | 1.4 | Labels, group headers |
| Body Large | __px | Regular (400) | 1.6 | Primary body text |
| Body | __px | Regular (400) | 1.5 | Standard text |
| Caption | __px | Regular (400) | 1.4 | Timestamps, meta, secondary |
| Label | __px | Medium (500) | 1.2 | Button text, form labels |

---

## 4. Spacing & Geometry

### Spacing Scale
| Token | Value | Usage |
|-------|-------|-------|
| `--space-xs` | 4px | Inline gaps, icon-text spacing |
| `--space-sm` | 8px | Tight element spacing |
| `--space-md` | 16px | Standard element spacing |
| `--space-lg` | 24px | Section spacing |
| `--space-xl` | 32px | Page section gaps |
| `--space-2xl` | 48px | Major section breaks |

### Border Radius
| Token | Value | Usage |
|-------|-------|-------|
| `--radius-sm` | 4px | Small elements (chips, tags) |
| `--radius-md` | 8px | Buttons, inputs |
| `--radius-lg` | 12px | Cards, panels |
| `--radius-full` | 999px | Pills, avatars |

### Shadows
| Token | Value | Usage |
|-------|-------|-------|
| `--shadow-card` | 0 4px 20px rgba(0,0,0,0.03) | Card elevation |
| `--shadow-dropdown` | 0 8px 30px rgba(0,0,0,0.08) | Dropdowns, modals |
| `--shadow-focus` | 0 0 0 3px rgba(primary, 0.2) | Focus rings |

---

## 5. Component Inventory

### Atoms
List every base element your product needs:

| # | Component | Variants | States |
|---|-----------|----------|--------|
| A1 | Button | primary, secondary, outline, ghost, danger | default, hover, active, disabled, loading |
| A2 | Input | text, email, password, number, textarea | default, focus, error, disabled |
| A3 | Checkbox | standard, indeterminate | default, checked, disabled |
| A4 | ... | ... | ... |

### Molecules
| # | Component | Composed From | Purpose |
|---|-----------|--------------|---------|
| M1 | FormField | A2 (Input) + Label + Error text | Form input with label and validation |
| M2 | NavItem | A1 (Button-like) + Icon + Badge | Sidebar navigation link |
| M3 | ... | ... | ... |

### Organisms
| # | Component | Composed From | Layout Logic |
|---|-----------|--------------|-------------|
| O1 | Sidebar | M2 (NavItem) × N + Logo + Role selector | Collapsible, 3 states (full/compact/collapsed) |
| O2 | PageHeader | Title + Breadcrumbs + Action buttons | Responsive, sticky optional |
| O3 | ... | ... | ... |

---

## 6. Screen Inventory

List every unique screen in your product:

| # | Screen Name | Role Access | Key Components | Status |
|---|-------------|------------|----------------|--------|
| S1 | Login | All | Form, Logo, Illustration | To build |
| S2 | Dashboard — Employee | Employee | KPI panel, Status badges, Activity feed | To build |
| S3 | Dashboard — Manager | Manager | Team selector, KPI panel, Data grid | To build |
| S4 | ... | ... | ... | ... |

---

## 7. Illustration Style (Optional)

**Style reference:** [e.g., unDraw by Katerina Limpitsouni]

**Characteristics:**
- [e.g., Elongated proportions, flat color, no outlines]
- [Color palette: same as brand tokens]
- [Aspect ratio: 4:3]

**Anti-patterns:**
- [e.g., No cute/kawaii/mascot aesthetics]
- [No 3D renders or gradients]

---

## 8. Responsive Breakpoints

| Breakpoint | Width | Layout Changes |
|-----------|-------|----------------|
| Mobile | < 640px | Single column, bottom nav, full-width cards |
| Tablet | 640-1024px | 2 columns, sidebar collapsed, cards in grid |
| Desktop | > 1024px | Full layout, sidebar expanded, multi-column grids |

---

## 9. Animation & Motion

| Element | Animation | Duration | Easing |
|---------|-----------|----------|--------|
| Page transition | Fade in | 200ms | ease-out |
| Card hover | Scale 1.02 + shadow increase | 150ms | ease-in-out |
| Dropdown open | Slide down + fade | 150ms | ease-out |
| Loading spinner | Rotate | 1000ms | linear |
| Progress ring | Fill arc | 800ms | ease-out |

**Reduced motion:** All animations respect `prefers-reduced-motion: reduce`. Disable animated particles, reduce transitions to instant.

---

## Changelog

| Version | Date | Changes |
|---------|------|---------|
| v1.0 | YYYY-MM-DD | Initial UIDD creation |
