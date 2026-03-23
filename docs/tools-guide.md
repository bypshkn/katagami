# Which AI Tool for Which Phase

> Not all AI tools are equally good at every phase. This was learned the hard way across 100+ sessions.

---

## The Key Split

**Phases 1-4** (documents, design concepts, illustrations) → **Conversational AI** with long context.

**Phases 5-6** (building code, assembling screens) → **Coding AI** with file system access.

Using a coding tool for Phase 3 (UIDD generation) will give you worse results. Using a chat tool for Phase 5 (code generation) will lose your files. Match the tool to the phase.

---

## Phase-by-Phase Recommendations

| Phase | Best Tool | Why | Alternatives |
|-------|-----------|-----|-------------|
| **Phase 1** — PRD | Any chat AI | Text generation, no special requirements | Claude, ChatGPT, Gemini |
| **Phase 2** — Research | Browser + human judgment | You need to look at real products | AI can help analyze screenshots |
| **Phase 3** — UIDD | **Claude Projects / Antigravity** | Needs long context to hold PRD + references + 3 concepts simultaneously | Any chat AI with large context window |
| **Phase 3** — Illustrations | **Antigravity + Recraft V3** | Antigravity holds visual direction across a session; Recraft produces cleanest vector output | Midjourney (needs post-processing) |
| **Phase 4** — Design Brief | Any chat AI | Merging two documents into one structured brief | Simple enough for any tool |
| **Phase 5** — Build DS | **Claude Code / Cowork / Cursor** | Needs file system access, terminal, live code editing | Any AI coding tool with terminal |
| **Phase 6** — Screens | **Claude Code / Cowork / Cursor** | Same as Phase 5 — composing screens from code components | Same as Phase 5 |
| **Review/QA** | **Claude Code / Cowork** | Needs browser access for screenshots, file access for fixes | Cursor with browser preview |

---

## Why Antigravity for Phase 3?

Google's Antigravity (AI IDE) handles the UIDD generation phase well because it maintains visual reasoning context across a long session. When you're iterating on 3 design concepts with color palettes, typography scales, and component inventories, you need the AI to "remember" the creative direction without drifting.

Claude Projects works similarly well — the persistent project context keeps your PRD and references available across the full conversation.

Regular chat (without project context) tends to lose track of earlier design decisions by the time you're refining the third concept.

---

## Why Not Cursor/Claude Code for Documents?

Coding tools are optimized for file editing, not long-form document generation with iterative refinement. When you're in Phase 3, you want a conversational back-and-forth: "Make concept 2 more corporate." "Darken the background." "What if we used Inter instead of DM Sans?"

Coding tools will try to write files immediately. Chat tools let you explore before committing.

---

## Session Length Guidance

| Tool | Optimal Session | When to Restart |
|------|----------------|-----------------|
| Claude Projects | 30-50 messages | When concepts start mixing or context feels "stale" |
| Antigravity | 20-40 exchanges | When visual direction becomes inconsistent |
| Claude Code | 1 Block per session | When AI ignores tokens or invents components |
| Cursor | 1 Block per session | When autocomplete starts suggesting wrong patterns |
| Cowork | 1 Block per session | Same as Claude Code |

The universal rule: when AI output quality drops, don't fight it. Start a new session with fresh context and only the relevant inputs.
