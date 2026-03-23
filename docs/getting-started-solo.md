# Getting Started — Solo Founder

> You're PM, designer, and developer in one person. Here's the fastest path through all 6 phases.

---

## The Full Pipeline (1-2 days)

### Day 1: Documents (Phases 1-4)

| Step | Time | Action | Tool |
|------|------|--------|------|
| **Phase 1** | 1-2h | Write PRD: features, roles, acceptance criteria | Any chat AI |
| **Phase 2** | 30m | Collect 3-5 visual references with annotations | Browser |
| **Phase 3** | 1-2h | Generate UIDD via [Miyabi](../agents/miyabi.md): feed PRD + references → pick from 3 concepts | Claude Projects / Antigravity |
| **Phase 4** | 30m | Merge PRD + UIDD into [Design Brief](../templates/design-brief.md) | Any chat AI |

### Day 2: Build (Phases 5-6)

| Step | Time | Action | Tool |
|------|------|--------|------|
| **Block 1** | 30m | Initialize tokens: CSS variables + Tailwind config | Claude Code / Cursor |
| **Block 2** | 1-2h | Build Atoms with [ds-architect prompt](../prompts/ds-architect.md) | Claude Code / Cursor |
| **Block 3** | 1-2h | Build Molecules with [component-builder prompt](../prompts/component-builder.md) | Claude Code / Cursor |
| **Block 4** | 1h | Build Organisms | Claude Code / Cursor |
| **Phase 6** | 2-4h | Assemble screens with [screen-assembler prompt](../prompts/screen-assembler.md) | Claude Code / Cursor |
| **Polish** | 1-2h | Review with [design-reviewer prompt](../prompts/design-reviewer.md) | Claude Code / Cursor |

---

## Speed Tips

**Don't iterate early.** Get all screens to 80% before polishing any to 100%. AI context degrades over long sessions — use the momentum while it lasts.

**One session = one block.** Don't try to build the entire DS in one mega-session. Start fresh for each block. Copy only the relevant tokens and task into the new session.

**Batch corrections.** Note issues during build (wrong padding, color mismatch) but don't interrupt the flow. Fix everything in a dedicated polish session at the end.

**Use the checklist.** Before declaring anything done: `npm run build` = zero errors, all variants on showcase page, colors match UIDD.

---

## Key Documents

| Phase | You Need | Get It From |
|-------|----------|-------------|
| Phase 3 | UIDD | [Miyabi agent](../agents/miyabi.md) or [UIDD template](../templates/uidd-template.md) |
| Phase 4 | Design Brief | [Design Brief template](../templates/design-brief.md) |
| Phase 5 | Build prompts | [prompts/ds-architect.md](../prompts/ds-architect.md), [prompts/component-builder.md](../prompts/component-builder.md) |
| Phase 6 | Assembly prompt | [prompts/screen-assembler.md](../prompts/screen-assembler.md) |
| Review | QA prompt | [prompts/design-reviewer.md](../prompts/design-reviewer.md) |

---

## Which AI Tool When?

Phases 1-4 (documents) → **Conversational AI** with long context: Claude Projects, Antigravity

Phases 5-6 (code) → **Coding AI** with file system access: Claude Code, Cowork, Cursor

> Detailed comparison: [tools-guide.md](tools-guide.md)

---

## Critical Rules

1. **Zero Hallucination** — if AI adds something not in your spec, delete it. [Read the rules →](zero-hallucination.md)
2. **Tokens only** — no hardcoded hex, no arbitrary font sizes. Everything through CSS variables → Tailwind.
3. **Source tracing** — every design element traces to PRD or UIDD. No "it seemed like a good idea."
