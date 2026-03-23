# Getting Started — Developer

> You receive a Design Brief (PRD + UIDD merged) and build the design system as production React code.

---

## Your Checklist

- [ ] Receive Design Brief from PM (or create your own via [templates](../templates/design-brief.md))
- [ ] Set up project: Next.js + Tailwind + TypeScript strict
- [ ] Create git branch `concept/design-system`
- [ ] **Block 1:** Initialize tokens (CSS variables + Tailwind config)
- [ ] **Block 2:** Build Atoms — paste [component-builder prompt](../prompts/component-builder.md) + token section
- [ ] **Block 3:** Build Molecules — compose from atoms
- [ ] **Block 4:** Build Organisms — compose from molecules + add layout logic
- [ ] **Phase 6:** Assemble screens from DS components
- [ ] Run review with [design-reviewer prompt](../prompts/design-reviewer.md)

---

## Before You Start

You need these inputs:

| Input | Source | Contains |
|-------|--------|----------|
| Design Brief | PM / yourself | Token values, component list, screen inventory, build order |
| UIDD | PM / Miyabi agent | Full design language spec — every hex, every font size |
| PRD | PM | Feature specs, acceptance criteria, role definitions |

If you don't have these → ask the PM, or create them yourself using [templates/](../templates/).

---

## Build Workflow

### Session Discipline

One AI session = one Block. Start fresh for each block. AI context degrades over long sessions.

```
Session 1: Tokens (Block 1)                         → commit
Session 2: Atoms (Block 2)                          → commit
Session 3: Molecules (Block 3)                      → commit
Session 4: Organisms (Block 4)                      → commit
Session 5-N: Screen Assembly (1-3 screens each)     → commit each
Session N+1: Polish pass (review + batch fixes)     → commit
```

**Momentum Rule:** While AI is generating well — don't stop for small fixes. Note issues, push forward. Batch corrections into a dedicated fix session.

→ Full build guide: [docs/phase-5-build.md](phase-5-build.md)

---

## Prompts — What to Use When

| Prompt | When | What It Does |
|--------|------|-------------|
| [ds-architect.md](../prompts/ds-architect.md) | Starting a new DS from scratch | Master prompt — sets up Atomic Design rules, token system, showcase pattern |
| [component-builder.md](../prompts/component-builder.md) | Building individual components | Strict rules for props, styling, TypeScript, variants |
| [screen-assembler.md](../prompts/screen-assembler.md) | Composing full pages | DS-only composition, realistic mock data, no one-off styling |
| [design-reviewer.md](../prompts/design-reviewer.md) | QA / polish pass | Spec-only feedback, token verification, screen classification |
| [illustration-gen.md](../prompts/illustration-gen.md) | Generating illustrations | 6 style presets, brand color integration |

---

## Technical Standards

**TypeScript:** Strict mode. No `any`. Explicit return types. Props interfaces for every component.

**Styling:** Two-layer token system. Define as CSS variables in `globals.css` → consume via Tailwind classes mapped in `tailwind.config.ts`. Never use raw `var(--color-*)` in JSX. Never hardcode hex values.

**Components:** `Ds*` prefix (DsButton, DsCard). Props-driven variants. Barrel exports via `index.ts`.

**Showcase:** Every component renders on `/demo/design-system` with all variants. This is your Storybook.

**Quality gate:** `npm run build` = zero errors. All variants on showcase. Colors match UIDD. Responsive at 375px and 1440px.

---

## Git Workflow

```
main → dev → concept/design-system
```

Only touch: `src/components/ds/`, `src/app/demo/`, `globals.css`, `tailwind.config.*`

Commit convention: `feat(ds): add date picker molecule — 3 variants`

→ Full git guide: [docs/git-workflow.md](git-workflow.md)

---

## Files You Need

| File | What It Is |
|------|-----------|
| [prompts/ds-architect.md](../prompts/ds-architect.md) | Master prompt — start here |
| [prompts/component-builder.md](../prompts/component-builder.md) | Per-component build prompt |
| [prompts/screen-assembler.md](../prompts/screen-assembler.md) | Screen composition prompt |
| [prompts/design-reviewer.md](../prompts/design-reviewer.md) | QA review prompt |
| [docs/phase-5-build.md](phase-5-build.md) | Detailed build guide with AI prompt patterns |
| [docs/zero-hallucination.md](zero-hallucination.md) | Anti-hallucination rules (include in every prompt) |
| [docs/git-workflow.md](git-workflow.md) | Branch strategy, commit conventions, PR workflow |

**Templates and agents are for PMs.** You may never need them.
