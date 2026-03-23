# Quickstart — 7 Steps from Idea to Screens

> No philosophy. No "why". Just do this → get this.

---

## Step 1 → PRD

**Input:** Your idea — features, user roles, business rules.
**Action:** Write a PRD in any chat AI. Cover: feature list, user roles, acceptance criteria, data rules.
**Output:** `PRD.md` — the single source of truth for what gets built.

**Rule:** WHAT and WHY only. No component names, no CSS, no routes.

---

## Step 2 → Visual References

**Input:** Your PRD + taste.
**Action:** Collect 3–5 screenshots of products you like. For each one, note what to borrow (layout, colors, spacing) and what to skip.
**Output:** A folder of annotated screenshots.

---

## Step 3 → UIDD

**Input:** PRD + references.
**Action:** Feed both to the [Miyabi agent](../agents/miyabi.md). It generates 3 design concepts. Pick one.
**Output:** `UIDD.md` — your complete design language: color tokens (hex), typography scale, spacing system, component inventory, screen list.

**Alternative:** Fill the [UIDD template](../templates/uidd-template.md) manually.

---

## Step 4 → Design Brief

**Input:** PRD + UIDD.
**Action:** Merge into one document using the [Design Brief template](../templates/design-brief.md). Copy token values, list screens to build, define build order.
**Output:** `design-brief.md` — the only document your AI coding tool needs.

---

## Step 5 → Build Components

**Input:** Design Brief + [ds-architect prompt](../prompts/ds-architect.md).
**Action:** Feed both to an AI coding tool (Claude Code / Cursor / Cowork). Build layer by layer:

```
Session 1: Tokens → CSS variables + Tailwind config         → commit
Session 2: Atoms → Button, Input, Badge, etc.               → commit
Session 3: Molecules → FormField, NavItem, Card              → commit
Session 4: Organisms → Sidebar, PageHeader, DataPanel        → commit
```

**Output:** `src/components/ds/` — production React components + showcase page at `/demo/design-system`.

**Rule:** One session = one block. Don't fix small issues mid-flow — note them, batch-fix later.

---

## Step 6 → Assemble Screens

**Input:** Design Brief + [screen-assembler prompt](../prompts/screen-assembler.md) + built DS components.
**Action:** Feed to AI coding tool. It composes full pages using ONLY `Ds*` components. 1–3 screens per session.
**Output:** Complete pages with realistic mock data, verified against PRD acceptance criteria.

**Rule:** If a screen needs a component that doesn't exist — go back to Step 5 and build it. No one-off styling.

---

## Step 7 → Review

**Input:** Built screens + [design-reviewer prompt](../prompts/design-reviewer.md).
**Action:** Fresh AI session. Reviewer audits every screen against PRD + UIDD. Flags only spec-traceable issues.
**Output:** Fix list. Batch-apply fixes in one session → done.

---

## Cheat Sheet

| Step | You Do | AI Does | Time |
|------|--------|---------|------|
| 1. PRD | Write | Helps structure | 1–2h |
| 2. References | Collect + annotate | — | 30m |
| 3. UIDD | Pick from 3 concepts | Generates concepts | 1–2h |
| 4. Design Brief | Merge docs | Helps format | 30m |
| 5. Components | Review in browser | Writes code | 3–5h |
| 6. Screens | Review + approve | Assembles pages | 2–4h |
| 7. Review | Apply fixes | Audits against spec | 1–2h |

**Total: ~1–2 days for a complete design system + screens.**
