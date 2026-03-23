# Getting Started — PM / Founder

> You write specs, pick visual direction, and review results. You don't write code — AI does that.

---

## Your Checklist

- [ ] **Phase 1: Write the PRD** — features, user roles, acceptance criteria, business rules
- [ ] **Phase 2: Collect references** — 3-5 products you like, annotated ("borrow the layout, skip the color")
- [ ] **Phase 3: Get a UIDD** — use [Miyabi agent](../agents/miyabi.md) or fill the [UIDD template](../templates/uidd-template.md)
- [ ] **Phase 4: Assemble the Design Brief** — merge PRD + UIDD using the [template](../templates/design-brief.md)
- [ ] **Hand off to developer** — they take the Brief + prompts from `/prompts/` and build

---

## Phase 1: PRD

Write a Product Requirements Document covering: feature inventory, user roles, acceptance criteria, data rules, business logic. The PRD describes **WHAT** and **WHY**, never HOW (no component names, no CSS, no routes).

The PRD becomes the **truth anchor** — every design decision must trace back to it. If a feature isn't in the PRD, it doesn't exist in the design system.

**Tool:** Any chat AI (Claude, ChatGPT). No special requirements.

---

## Phase 2: Visual Research

Collect 3-5 reference products. For each one, write down what to borrow (layout pattern, color approach, spacing rhythm) and what to skip. References inform **style**, not features — never add features just because a competitor has them.

**Tool:** Your browser + your taste. AI can help analyze, but you need to look at real products.

---

## Phase 3: UIDD

The UI Design Description replaces Figma. It's a **written specification** of your design language: color tokens (hex values), typography (font families, size scale), spacing, component inventory, screen inventory.

**Why written?** AI reads text specs perfectly but struggles to interpret Figma screenshots consistently. A written UIDD gives AI unambiguous build instructions.

**Two ways to create it:**

1. **Use Miyabi** (recommended) — an AI agent that takes your PRD + references, generates 3 UI concepts, you pick one, and it outputs a complete UIDD. You don't need to know what "design tokens" are. → [agents/miyabi.md](../agents/miyabi.md)

2. **Fill the template** — if you know what you want, fill in the blanks. → [templates/uidd-template.md](../templates/uidd-template.md)

**Tool:** Claude Projects or Antigravity (Google AI IDE). Needs long context to hold PRD + references + 3 concepts. See [tools guide](tools-guide.md).

---

## Phase 4: Design Brief

Combine PRD + UIDD into one "AI build spec." This is the ONLY document the developer (or AI) needs to start building. If something is missing from the Brief, the builder should ask — not guess.

→ [templates/design-brief.md](../templates/design-brief.md)

**Tool:** Any chat AI. You're merging two docs into one structured brief.

---

## Your Review Role (Phases 5-6)

Once the developer builds, you review:

- **Does it match the UIDD?** Colors, fonts, spacing — compare against your spec
- **Does it match the PRD?** Every screen should satisfy acceptance criteria
- **Zero Hallucination check** — if you see a feature nobody asked for, flag it

Your feedback should always reference a document: "This doesn't match UIDD §4.2" or "PRD says role X shouldn't see this screen."

---

## Files You Need

| File | What It Is | When You Use It |
|------|-----------|-----------------|
| [templates/uidd-template.md](../templates/uidd-template.md) | Design language template | Phase 3 |
| [templates/design-brief.md](../templates/design-brief.md) | AI build spec template | Phase 4 |
| [agents/miyabi.md](../agents/miyabi.md) | AI agent that generates UIDD for you | Phase 3 |
| [docs/zero-hallucination.md](zero-hallucination.md) | Rules for catching AI inventions | Review |

**Everything else in this repo is for developers.** You don't need it.
