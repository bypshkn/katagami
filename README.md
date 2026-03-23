<div align="center">

# Katagami 型紙

![Version](https://img.shields.io/badge/version-1.0.0-blue?style=flat-square)
![Methodology](https://img.shields.io/badge/methodology-Atomic_Design-purple?style=flat-square)
![Phases](https://img.shields.io/badge/phases-6-green?style=flat-square)
![Prompts](https://img.shields.io/badge/battle--tested_prompts-5-orange?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-grey?style=flat-square)

**Build production-ready UI without a designer.**<br>
A methodology for creating scalable design systems using AI + Atomic Design + Spec-Driven Development.

---

Works with: **Claude Code** · **Cursor** · **Windsurf** · **Antigravity** · **Cowork**

</div>

---

## What Is This?

You describe what your product does. You collect visual references. AI generates a complete design system — tokens, components, screens — as production React code. You review in the browser and say "yes" or "fix this."

No Figma. No designer. No coding skills required (for PMs).

```
 You write spec    You pick style    AI generates     You combine      AI builds        AI assembles
 ┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐    ┌──────────┐     ┌──────────┐
 │  Phase 1  │ ──→│  Phase 2  │ ──→│  Phase 3  │ ──→│  Phase 4  │──→│  Phase 5  │ ──→│  Phase 6  │
 │   PRD     │    │ Research  │    │   UIDD    │    │  Brief    │   │Build DS   │    │ Screens   │
 └──────────┘     └──────────┘     └──────────┘     └──────────┘    └──────────┘     └──────────┘
```

---

<div align="center">

| 6 Phases | 5 Prompts | 2 Templates | 1 AI Agent | 100+ Sessions |
|:--------:|:---------:|:-----------:|:----------:|:-------------:|
| Linear pipeline from spec to screens | Battle-tested AI instructions | UIDD + Design Brief fill-in-the-blank | Miyabi — generates your design language | Methodology extracted from real builds |

</div>

---

## Get Started — Pick Your Role

<table>
<tr>
<td width="33%" valign="top">

### 🎯 I'm a PM / Founder

You write specs, pick visual direction, review results. You don't touch code.

**Your phases:** 1 → 2 → 3 → 4 → Review

**Time to first result:** ~2 hours

[**→ PM Getting Started**](docs/getting-started-pm.md)

</td>
<td width="33%" valign="top">

### ⚡ I'm a Developer

You get structured prompts that produce consistent, token-based components. TypeScript strict, CSS variables, Atomic Design.

**Your phases:** 5 → 6 → Review

**Time to first component:** ~15 minutes

[**→ Developer Getting Started**](docs/getting-started-dev.md)

</td>
<td width="33%" valign="top">

### 🚀 I'm a Solo Founder

You do everything — specs, design decisions, and code. The full pipeline, optimized for one person.

**Your phases:** 1 → 2 → 3 → 4 → 5 → 6

**Time to full DS:** ~1-2 days

[**→ Solo Founder Getting Started**](docs/getting-started-solo.md)

</td>
</tr>
</table>

---

## How It Actually Works (2 minutes)

1. **Write what you're building** — features, user roles, business rules → a PRD
2. **Collect visual inspiration** — screenshots of products you like, with notes
3. **AI generates your design language** — colors, fonts, spacing, components → a UIDD document. Pick from 3 concepts.
4. **Combine into one brief** — "here's what to build and how it should look"
5. **AI builds the components** — paste a prompt, AI writes production code. Watch it appear in the browser.
6. **AI assembles screens** — full pages composed from the components it built. You review.

**That's it.** The magic is in the quality of documents (steps 1-4) and the prompts (steps 5-6). This repo gives you both.

> **Just want to build?** → [Quickstart — 7 steps from idea to screens](docs/quickstart.md)
>
> Want the deep dive? Read the [full methodology](docs/methodology.md).

---

## Core Principles

**Zero Hallucination** — AI will confidently add features you never asked for. Every design element must trace to a source document. If it's not in the spec, it doesn't get built. [Read more →](docs/zero-hallucination.md)

**Momentum Over Perfection** — Build 10 screens at 80% before polishing 2 at 100%. AI context degrades over long sessions. Push forward, batch fixes later. [Read more →](docs/phase-5-build.md#session-strategy-momentum-over-perfection)

**Showcase-Driven** — Every component renders on a live demo page. This IS your Storybook, your Figma preview, and your test suite — always in sync with the code.

---

## Project Structure

```
katagami/
├── README.md                        ← You are here
│
├── docs/
│   ├── quickstart.md               ← 7 steps, no philosophy, just do it
│   ├── getting-started-pm.md       ← PM onboarding path
│   ├── getting-started-dev.md      ← Developer onboarding path
│   ├── getting-started-solo.md     ← Solo founder onboarding path
│   ├── methodology.md              ← Full pipeline deep dive
│   ├── tools-guide.md              ← Which AI tool for which phase
│   ├── phase-5-build.md            ← Step-by-step build guide
│   ├── zero-hallucination.md       ← Anti-hallucination rules
│   └── git-workflow.md             ← Branch strategy + commits
│
├── templates/
│   ├── uidd-template.md            ← Fill-in-the-blank UIDD starter
│   └── design-brief.md             ← Fill-in-the-blank Design Brief
│
├── prompts/
│   ├── ds-architect.md             ← Master prompt for DS creation
│   ├── component-builder.md        ← Build individual components
│   ├── screen-assembler.md         ← Compose screens from DS
│   ├── design-reviewer.md          ← QA / review sessions
│   └── illustration-gen.md         ← Illustration generation
│
└── agents/
    └── miyabi.md                    ← Miyabi: AI UX agent for Phase 3
```

---

## Quick Start

```bash
# 1. Clone
git clone https://github.com/bypshkn/katagami.git

# 2. Pick your role above and follow the getting-started guide

# 3. When ready to build: feed your Design Brief + prompt to your AI tool
```

---

## Why "Katagami"?

**型紙 (katagami)** — traditional Japanese stencils for dyeing kimono fabric. One stencil, once crafted, stamps a consistent design across meters of silk. You invest effort once into the design system (the stencil), and every screen inherits the same tokens, proportions, and consistency.

*Part of an agent family: Satori (悟り) for discovery, Toranaga for strategy, Miyabi (雅) for design, Kiwari (木割) for architecture, Takumi (匠) for implementation.*

---

## Default Tech Stack

| Layer | Default | Swap for |
|-------|---------|----------|
| Framework | Next.js 14+ (App Router) | Remix, Nuxt, SvelteKit |
| Styling | Tailwind CSS v4 | CSS Modules, Styled Components |
| Language | TypeScript (strict) | — |
| Icons | Lucide React | Heroicons, Phosphor |

> Katagami is stack-agnostic in methodology. These are defaults, not requirements.

---

<div align="center">

**Created by [Anton Pushkin (PSHKN)](https://github.com/bypshkn) at [Brocoders](https://brocoders.com)**<br>
Methodology refined with Claude (Anthropic) as the primary AI design engine.<br>
Extracted from 100+ real AI-assisted design sessions.

MIT License — use it, fork it, improve it.

</div>
