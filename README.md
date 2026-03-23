# Katagami 型紙

> Build production-ready UI without a designer.
> A methodology for creating scalable design systems using AI + Atomic Design + Spec-Driven Development.

### Why "Katagami"?

**型紙 (katagami)** — traditional Japanese stencils used for dyeing kimono fabric. Artisans would cut intricate patterns into sheets of handmade paper treated with persimmon juice, creating stencils of extraordinary precision and beauty. One stencil, once crafted, could stamp a consistent design across meters of silk — turning a single act of mastery into infinite reproduction.

This is exactly what Katagami methodology does: you invest effort once into creating the design system (the stencil), and then every screen you build from it inherits the same visual consistency, the same tokens, the same proportions — without re-inventing anything. The stencil IS the specification.

*Katagami is part of an agent family: Satori (悟り) for discovery, Toranaga for strategy, Miyabi (雅) for design, Kiwari (木割) for architecture, Takumi (匠) for implementation.*

---

## How It Works (2 minutes)

You describe what your product does and how you want it to look. AI builds the actual interface components. You review the result in the browser and say "yes" or "fix this." No Figma. No designer. No coding skills required.

**The process:**

1. **You write what you're building** — features, user roles, business rules (a PRD)
2. **You collect visual inspiration** — screenshots of products you like, with notes on what to borrow
3. **AI generates your design language** — colors, fonts, spacing, component list (a UIDD document). You pick from 3 concepts, like choosing a restaurant from a menu.
4. **You combine it into one brief** — "here's what to build and here's how it should look"
5. **AI builds the components** — you paste a prompt, AI writes production code. You watch the result appear in the browser.
6. **You assemble screens** — AI composes full pages from the components it already built. You review.

**That's it.** The magic is in the quality of the documents you prepare (steps 1-4) and the prompts you give the AI (steps 5-6). This repo gives you templates for the documents and battle-tested prompts for the AI.

---

## Your Role Depends on Who You Are

**If you're a PM or founder:** Your job is Phases 1-4 (documents) and reviewing the result. You don't write code — AI does that. You write specs, pick visual direction, and say "approved" or "not quite, fix the header." The prompts in `/prompts/` are instructions you copy-paste into Claude/Cursor — you don't need to understand the code inside them.

**If you're a developer:** You get structured prompts that produce consistent, token-based components following Atomic Design. The methodology enforces TypeScript strict mode, CSS variable tokens, barrel exports, showcase-driven development, and zero hallucination rules. Read `/docs/` for the technical details.

**If you're both (solo founder who codes):** You get the full picture — documents drive the design, prompts drive the code, quality gates keep everything consistent.

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

## Prerequisites: What You Need Before Building

Katagami works when you feed AI **quality documentation**. The methodology doesn't prescribe how you create these documents — use your own process, your PM tools, your AI agents. What matters is that the documents exist and are detailed enough.

### Phase 1: PRD — Define What You're Building

You need a Product Requirements Document that covers: feature inventory, user roles, acceptance criteria, data rules, and business logic. The PRD describes WHAT and WHY, never HOW (no component names, no CSS classes, no routes).

**Katagami-specific:** The PRD becomes the **truth anchor** — every design decision must trace back to a PRD section. If a feature isn't in the PRD, it doesn't exist in the design system.

### Phase 2: Visual Research — Find Your Aesthetic

Collect 3–5 references: competitor products, aspirational designs, anything that captures the visual direction you want. For each reference, annotate what to borrow (layout pattern, color approach, spacing) and what to skip. References inform style, not features — never add features to your PRD just because a competitor has them.

### Phase 3: UIDD — UI Design Description

This is the key document that replaces Figma. The UIDD is a **written specification** of your design language: color tokens (exact hex values), typography (font families, size scale, weight rules), spacing system, component inventory with variants and states, screen inventory, and illustration style.

**Why written, not visual?** AI tools read text specifications perfectly but struggle to interpret Figma screenshots consistently. A written UIDD gives AI unambiguous instructions.

**How to create it:** You can write it manually using our [UIDD template](templates/uidd-template.md), or use an AI agent like **Miyabi** — a specialized UX Designer agent that takes your PRD + references as input, generates 3 UI concepts for you to choose from, and produces a complete UIDD with all required sections. The agent approach lowers the barrier significantly: you don't need to know what "design tokens" are to get a professional UIDD.

> See: [templates/uidd-template.md](templates/uidd-template.md) for the fill-in-the-blank template.
> See: [agents/miyabi.md](agents/miyabi.md) for the Miyabi UX agent definition.

### Phase 4: Design Brief — The AI Build Spec

Combine your PRD + UIDD into a single "AI build spec" — a structured document that tells the AI exactly what to build, in what order, with what tokens. This is the ONLY document the AI coding tool needs. If information is missing from the Brief, the AI should ask — not guess.

> See: [templates/design-brief.md](templates/design-brief.md) for the Design Brief template.

### Prerequisites Checklist

Before starting Phase 5 (building), verify:
- [ ] PRD exists with features, roles, acceptance criteria
- [ ] Visual references collected (3-5 products, annotated screenshots)
- [ ] UIDD written with ALL tokens explicit (colors, typography, spacing, components, screens)
- [ ] Design Brief assembled (PRD + UIDD merged into AI-readable build spec)
- [ ] Project initialized (framework + styling + TypeScript)
- [ ] Git branch created for DS work

---

## Which AI Tool for Which Phase

Not all AI tools are equally good at every phase. This was learned the hard way:

| Phase | Best Tool | Why |
|-------|-----------|-----|
| Phase 1 (PRD) | Any chat AI (Claude, ChatGPT) | Text generation, no special requirements |
| Phase 2 (Research) | Browser + human judgment | AI can help analyze, but you need to look at real products |
| Phase 3 (UIDD) | **Claude Projects / Antigravity** | Needs long context to hold PRD + references + 3 concepts simultaneously. Chat-based AI with persistent project context works best here. |
| Phase 3b (Illustrations) | **Antigravity + Recraft V3** | Design concept exploration and illustration generation need visual reasoning and long context. Antigravity holds visual direction across a session better than coding tools. Recraft produces the cleanest vector output. |
| Phase 4 (Design Brief) | Any chat AI | Merging two documents into one structured brief |
| Phase 5 (Build DS) | **Claude Code / Cowork / Cursor** | Needs file system access, terminal, live code editing. This is a coding task — use a coding tool. |
| Phase 6 (Screens) | **Claude Code / Cowork / Cursor** | Same as Phase 5 — composing screens from code components |
| Review/QA | **Claude Code / Cowork** | Needs browser access for screenshots, file access for fixes |

**The key split:** Phases 1-4 (documents + design concept + illustrations) work best in **conversational AI** with long context. Phases 5-6 (building + assembling code) work best in **coding AI** with file system access.

Trying to do design concept work in a coding tool, or coding in a chat tool, produces worse results. Use the right tool for the right job.

---

## Phase 5: Build the Design System

**Input:** Design Brief + AI tool (Claude Code / Cowork / Cursor)
**Output:** Production React components + interactive showcase

**This is where the magic happens.** You feed the Design Brief to an AI coding tool and build components layer by layer following Atomic Design.

### The Momentum Rule (Critical)

> **"While it's generating well — don't stop for small fixes. Push design forward while the AI has momentum. Iterations, polish, and pixel-perfect tweaks come later."**
> — Lesson learned from 100+ build sessions

AI tools lose context quality over long sessions. Every minor correction you make mid-flow "dilutes" the creative focus. The practical strategy:

1. **Build in broad strokes first.** Get 10 screens at 80% quality rather than 2 screens at 100%.
2. **Batch your corrections.** Note issues (wrong padding, color mismatch) but don't interrupt the build flow. Fix them in a dedicated polish session.
3. **Session discipline.** One session = one Block or one batch of screens. Start fresh for the next Block. Don't try to do everything in one mega-session — AI context degrades.
4. **Polish pass is separate.** After all screens exist, run a dedicated review + fix session. This is where you use the Design Reviewer prompt.
5. **Know when to restart.** If the AI starts producing inconsistent output (wrong tokens, ignoring your DS, inventing components) — start a new session with fresh context rather than fighting the current one.

### Build Order

```
Block 1: Tokens & Atoms
  └─ CSS variables (globals.css / Tailwind config)
  └─ Button, Input, Checkbox, Radio, Toggle, Badge, Chip, Tag, Link

Block 2: Core Molecules
  └─ PageHeader, FormField, NavItem, Card variants
  └─ These compose 2-3 atoms into functional units

Block 3: Complex Molecules
  └─ Domain-specific components (StatusBadge, MetricCard, etc.)
  └─ Data visualization components
  └─ Interactive components (Wizard steps, Survey progress)

Block 4: Organisms
  └─ Sidebar, Dashboard panels, Full-page layouts
  └─ Must compose DIFFERENT molecule types + add layout logic or state
  └─ If an organism is just `items.map(molecule)` — it's a thin wrapper, delete it
```

### The Showcase Pattern

Every component gets rendered on an interactive demo page (`/demo/design-system`). This page IS your Storybook, your Figma, and your test suite — all in one.

**Why showcase-driven?**
- Developers see all variants without reading code
- Visual bugs are spotted immediately
- No separate design tool to maintain
- The showcase is always in sync (it IS the code)

### Component Rules

1. **Single source of truth:** The component file IS the spec. No Figma equivalent needed.
2. **Props-driven variants:** All states expressed via TypeScript props, not separate components.
3. **Token-only styling:** Zero hardcoded hex values. Everything references CSS variables.
4. **Barrel exports:** Central `index.ts` for clean imports.
5. **Strict TypeScript:** No `any`. Explicit return types. Enforced at build time.

### Quality Gates

Before any component is "done":
- [ ] `npm run build` passes with zero errors
- [ ] All variants rendered on showcase page
- [ ] Visual verification in browser (screenshot comparison)
- [ ] Colors match UIDD token definitions exactly
- [ ] Typography uses defined classes, not arbitrary sizes
- [ ] Spacing follows grid system
- [ ] Responsive behavior tested (mobile, tablet, desktop)

> See: [docs/phase-5-build.md](docs/phase-5-build.md) for the AI prompt template and component checklist.

---

## Phase 6: Screen Assembly

**Input:** Design System components + PRD screen specs
**Output:** Production pages composed from DS components with real data

**Process:**
1. Take a screen spec from the PRD (e.g., "Dashboard — Manager View")
2. Map required data to existing DS components
3. Compose the page using ONLY DS components — no one-off styling
4. Fill with realistic mock data (not "Lorem ipsum")
5. Verify against PRD acceptance criteria

**Key rule:** If a screen needs a component that doesn't exist in your DS, go back to Phase 5 and build it properly. Never create one-off components inside pages.

### Review Process

For each screen, classify as:
- **`SCREEN EXISTS — needs design polish`**: Built, but doesn't match DS standards
- **`SCREEN MISSING — needs design`**: Specified in PRD/roadmap but not yet implemented

---

## The Zero Hallucination Rule

This is the most important principle in Katagami.

**AI tools will confidently add features, fields, and design patterns that don't exist in your spec.** This is the #1 source of design system bloat and scope creep.

### Rules

1. **Every design element must trace to a source document** (PRD, UIDD, or explicit user decision)
2. **If something "sounds reasonable" but has no doc source — it's a hallucination.** Flag it, don't build it.
3. **Unsourced copy text** must be marked `[DEMO COPY]`
4. **Unsourced design decisions** must be marked `[DESIGN DECISION — not in source docs]`
5. **When in doubt, ask.** Never guess.
6. **Industry-standard patterns** (e.g., close button on modals) are OK. Product-specific features are NOT.

### How to enforce

Include this in every AI prompt:
```
CRITICAL: Do NOT add features, fields, components, or design patterns
that are not specified in the source documents provided. If you think
something is missing, flag it as a GAP and ask — do not fill in the blank.
```

---

## Document Extraction Protocol

When working with specification documents (.docx, .xlsx), AI tools often miss critical data:

### The Problem
`python-docx`'s `doc.paragraphs` **skips all tables**. Derivation rules, option codes, scoring matrices, and privacy thresholds are typically IN tables. Reading only paragraphs = missing 40%+ of spec content.

### The Fix
Always extract BOTH:
```python
import docx
doc = docx.Document(path)

# Paragraphs
for p in doc.paragraphs:
    print(p.text)

# Tables (CRITICAL)
for table in doc.tables:
    for row in table.rows:
        cells = [cell.text.strip() for cell in row.cells]
        print(" | ".join(cells))
```

For .xlsx: read ALL sheets. Lookup values and formulas live in secondary sheets.

---

## Illustration Generation (Optional)

If your product uses custom illustrations, Katagami includes a universal prompt template with 6 style presets (corporate flat, friendly outline, minimal abstract, isometric, organic, bold geometric). Pick a style, plug in your brand colors, generate a consistent batch.

**Three key learnings from 50+ generation iterations:**
1. **Name a specific artist or library** — "in the style of Katerina Limpitsouni" works better than describing the style in words
2. **Hex codes, not color names** — "#1A2B3C" gives you one color. "Navy blue" gives you fifty.
3. **Negative prompts are mandatory** — every image AI defaults toward "friendly/cute" without explicit exclusions

**Recommended tool:** Use Antigravity (Claude Projects) for illustration concept development. It holds visual direction across a session. Use Recraft V3 for final generation — cleanest vector output.

> See: [prompts/illustration-gen.md](prompts/illustration-gen.md) for the full template with all 6 style presets.

---

## Git Workflow for Design System Work

### Branch Strategy
```
main
 └─ dev (working branch)
      └─ concept/design-system (DS changes only)
```

### File Boundary Discipline
Only touch these directories in DS branch:
- `src/components/ds/` — component code
- `src/app/demo/` — showcase pages
- `globals.css` / `tailwind.config` — tokens only

**Why?** Zero merge conflicts guaranteed. Other developers work in `src/app/`, `src/lib/`, `src/api/` — no overlap.

### Commit Convention
```
feat(ds): add date picker molecule — 3 variants
fix(ds): correct status badge colors to match UIDD
refactor(ds): remove thin wrapper organisms
```

---

## Tech Stack (Default, Customizable)

Katagami is stack-agnostic in methodology but ships defaults:

| Layer | Default | Alternatives |
|-------|---------|-------------|
| Framework | Next.js 14+ (App Router) | Remix, Nuxt, SvelteKit |
| Styling | Tailwind CSS v4 | CSS Modules, Styled Components |
| Language | TypeScript (strict) | — |
| Fonts | Local fonts via `next/font/local` | Google Fonts, Fontsource |
| Icons | Lucide React | Heroicons, Phosphor |
| Build | Turbopack | Vite, Webpack |
| Package Manager | pnpm | npm, yarn, bun |

---

## Quick Start

```bash
# 1. Clone this repo
git clone https://github.com/bypshkn/katagami.git

# 2. Read this README (you're doing it now)

# 3. Prepare your prerequisites (PRD, references, UIDD, Design Brief)
#    Use templates/ as starting points

# 4. Pick the right prompt from prompts/ for your current phase
#    Start with ds-architect.md for a new project

# 5. Feed your Design Brief + the prompt to Claude/Cursor/Copilot
#    Build layer by layer: Atoms → Molecules → Organisms → Screens
```

---

## Project Structure

```
katagami/
├── README.md                    ← You are here
├── docs/
│   ├── phase-5-build.md        ← Step-by-step build guide
│   ├── zero-hallucination.md   ← Anti-hallucination rules in detail
│   └── git-workflow.md         ← Branch strategy + commit conventions
├── templates/
│   ├── uidd-template.md        ← Fill-in-the-blank UIDD starter
│   └── design-brief.md         ← Fill-in-the-blank Design Brief
├── prompts/
│   ├── ds-architect.md         ← Master prompt for DS creation
│   ├── component-builder.md    ← Prompt for building individual components
│   ├── screen-assembler.md     ← Prompt for composing screens
│   ├── design-reviewer.md      ← Prompt for QA/review sessions
│   └── illustration-gen.md     ← Prompt template for illustration generation
├── agents/
│   └── miyabi.md               ← Miyabi: AI UX agent for UIDD generation
└── plugin/                     ← Cowork/Claude Code plugin (coming soon)
```

---

## Origin & Transparency

This methodology was not written in theory. It was extracted from **100+ real AI-assisted design sessions** on a production B2B SaaS project — building 40+ components, 20+ screens, and a complete design system from scratch without a designer.

The prompts in `/prompts/` are based on actual working instructions refined through iteration: ~60% extracted from real sessions, ~40% systematized and expanded into reusable templates. None were invented from scratch — but none are raw copy-paste either.

The templates in `/templates/` are formalized versions of documents that worked in production. The UIDD template is based on the output structure of the Miyabi UX agent. The Design Brief template captures the pattern used to brief AI coding sessions.

## Credits

Created by **Anton Pushkin (PSHKN)** at [Brocoders](https://brocoders.com).
Methodology refined with Claude (Anthropic) as the primary AI design engine.

---

## License

MIT — use it, fork it, improve it.
