# Katagami Methodology — Full Deep Dive

> This document covers the complete methodology in detail. For a quick overview, see the [README](../README.md). For role-specific paths, see [Getting Started](getting-started-pm.md).

---

## The Pipeline

```
Phase 1        Phase 2        Phase 3          Phase 4           Phase 5          Phase 6
┌──────────┐  ┌──────────┐  ┌────────────┐  ┌───────────────┐  ┌────────────┐  ┌──────────┐
│   PRD    │→ │ Visual   │→ │   UIDD     │→ │ Design Brief  │→ │  Build DS  │→ │  Screen  │
│ (What)   │  │ Research │  │ (How it    │  │ (Spec for AI) │  │ (Code)     │  │ Assembly │
│          │  │ (Mood)   │  │  looks)    │  │               │  │            │  │          │
└──────────┘  └──────────┘  └────────────┘  └───────────────┘  └────────────┘  └──────────┘
   You            You         AI + You          You              AI + You         AI + You
  write         collect       generates       combine           builds           assembles
  the spec     references     3 concepts     into brief        components        screens
```

---

## Phase 1: PRD — Define What You're Building

A Product Requirements Document covering: feature inventory, user roles, acceptance criteria, data rules, business logic.

The PRD describes **WHAT** and **WHY**, never **HOW** (no component names, no CSS classes, no routes).

**Katagami-specific:** The PRD becomes the truth anchor — every design decision must trace back to a PRD section. If a feature isn't in the PRD, it doesn't exist in the design system.

---

## Phase 2: Visual Research — Find Your Aesthetic

Collect 3-5 references: competitor products, aspirational designs, anything that captures the visual direction you want.

For each reference, annotate what to borrow (layout pattern, color approach, spacing) and what to skip. References inform style, not features — never add features to your PRD just because a competitor has them.

---

## Phase 3: UIDD — UI Design Description

The key document that replaces Figma. The UIDD is a written specification of your design language: color tokens (exact hex values), typography (font families, size scale, weight rules), spacing system, component inventory with variants and states, screen inventory, and illustration style.

**Why written, not visual?** AI tools read text specifications perfectly but struggle to interpret Figma screenshots consistently. A written UIDD gives AI unambiguous instructions.

**How to create it:** Use the [Miyabi agent](../agents/miyabi.md) (recommended) — it takes PRD + references, generates 3 concepts, you pick one, and it outputs a complete UIDD. Or fill the [UIDD template](../templates/uidd-template.md) manually.

---

## Phase 4: Design Brief — The AI Build Spec

Combine PRD + UIDD into a single document that tells the AI exactly what to build, in what order, with what tokens. This is the ONLY document the AI coding tool needs.

→ [templates/design-brief.md](../templates/design-brief.md)

---

## Phase 5: Build the Design System

Feed the Design Brief to an AI coding tool and build components layer by layer following Atomic Design.

### Build Order

```
Block 1: Tokens (Foundation)
  └─ CSS variables (globals.css / Tailwind config)
  └─ Font loading, spacing scale, color palette

Block 2: Atoms
  └─ Button, Input, Checkbox, Radio, Toggle, Badge, Chip, Tag, Link
  └─ Showcase page for all atoms with all variants

Block 3: Molecules
  └─ PageHeader, FormField, NavItem, Card variants
  └─ Domain-specific composites (StatusBadge, MetricCard, etc.)

Block 4: Organisms
  └─ Sidebar, Dashboard panels, Full-page layouts
  └─ Must compose DIFFERENT molecule types + add layout logic or state
  └─ If an organism is just `items.map(molecule)` — delete it
```

### The Momentum Rule

> While it's generating well — don't stop for small fixes. Push design forward while the AI has momentum. Iterations, polish, and pixel-perfect tweaks come later.

AI tools lose context quality over long sessions. Every minor correction mid-flow "dilutes" the creative focus.

1. **Build in broad strokes first.** Get 10 screens at 80% quality rather than 2 screens at 100%.
2. **Batch your corrections.** Note issues but don't interrupt the flow. Fix them in a dedicated polish session.
3. **Session discipline.** One session = one Block. Start fresh for the next. Don't do everything in one mega-session.
4. **Know when to restart.** If AI starts producing inconsistent output — start a new session with fresh context.

→ Detailed build guide: [phase-5-build.md](phase-5-build.md)

### The Showcase Pattern

Every component gets rendered on an interactive demo page (`/demo/design-system`). This page IS your Storybook, your Figma, and your test suite — all in one. Always in sync because it IS the code.

### Component Rules

1. The component file IS the spec. No Figma equivalent needed.
2. All states expressed via TypeScript props, not separate components.
3. Zero hardcoded hex values. Everything references CSS variables via Tailwind.
4. Barrel exports via central `index.ts`.
5. Strict TypeScript. No `any`. Explicit return types.

### Quality Gates

Before any component is "done": `npm run build` = zero errors, all variants on showcase, colors match UIDD, responsive at mobile + desktop.

---

## Phase 6: Screen Assembly

Take a screen spec from the PRD, map required data to existing DS components, compose the page using ONLY DS components (no one-off styling), fill with realistic mock data, verify against PRD acceptance criteria.

**Key rule:** If a screen needs a component that doesn't exist, go back to Phase 5 and build it. Never create one-off components inside pages.

---

## The Zero Hallucination Rule

AI tools will confidently add features, fields, and design patterns that don't exist in your spec. This is the #1 source of design system bloat and scope creep.

Every design element must trace to a source document. If something "sounds reasonable" but has no doc source — it's a hallucination. Flag it, don't build it.

→ Full rules: [zero-hallucination.md](zero-hallucination.md)

---

## Styling Strategy: CSS Variables + Tailwind

Two-layer approach to tokens:

1. **Define** tokens as CSS variables in `globals.css` (`:root { --color-brand-primary: #HEX; }`)
2. **Consume** tokens via Tailwind utility classes mapped in `tailwind.config.ts` (`colors: { brand: { primary: 'var(--color-brand-primary)' } }`)

This gives CSS variables as the single source of truth (easy to theme, override, inspect) and Tailwind classes for rapid composition in JSX. Never use raw `var(--color-*)` in JSX. Never hardcode hex values.

---

## Document Extraction Protocol

When working with specification documents (.docx, .xlsx), AI tools often miss critical data stored in tables. Always extract BOTH paragraphs AND tables from .docx files, and read ALL sheets from .xlsx files.

→ See [zero-hallucination.md](zero-hallucination.md#document-extraction-protocol) for code examples.

---

## Illustration Generation (Optional)

Katagami includes a universal prompt template with 6 style presets (corporate flat, friendly outline, minimal abstract, isometric, organic, bold geometric). Pick a style, plug in your brand colors, generate a consistent batch.

Key learnings: name a specific artist or library for style anchoring, use hex codes not color names, and negative prompts are mandatory.

→ See [prompts/illustration-gen.md](../prompts/illustration-gen.md)

---

## Origin & Transparency

This methodology was extracted from 100+ real AI-assisted design sessions — building 40+ components, 20+ screens, and a complete design system from scratch without a designer.

The prompts are based on actual working instructions refined through iteration: ~60% extracted from real sessions, ~40% systematized into reusable templates. The templates capture patterns that worked in production.
