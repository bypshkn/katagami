# The Zero Hallucination Rule — Katagami's Core Discipline

> This is the single most important document in the methodology.
> Print it. Pin it. Paste it into every AI prompt.

---

## The Problem

AI tools (Claude, ChatGPT, Cursor, Copilot) will confidently generate UI elements that don't exist in your specification. They'll add search bars, filters, pagination, extra fields, bonus features, and "nice-to-have" interactions — all without being asked. They sound reasonable. They look professional. And they're all hallucinations.

**The cost of hallucinated UI:**
- Scope creep disguised as "good design"
- Developer hours wasted building unspecified features
- Product owner discovers features in code review that were never approved
- Design system bloated with components nobody asked for
- Stakeholder trust eroded ("who approved this filter?")

---

## The Rules

### Rule 1: Source Tracing
Every design element MUST trace to a source document.

**Valid sources:**
- PRD (Product Requirements Document)
- SRS (Software Requirements Specification)
- UIDD (UI Design Description)
- Task specifications (Jira/Notion)
- Explicit user/stakeholder decision (documented)

**Invalid sources:**
- "It's a common pattern"
- "Users would expect this"
- "It would improve UX"
- "Best practice in the industry"
- AI's own reasoning about what should be there

### Rule 2: Flag, Don't Fill
If something is missing from the spec, do NOT fill in the gap. Instead:

```
[GAP]: The spec does not define filtering behavior for this table.
Options:
A) No filtering (simplest, matches spec as-is)
B) Client-side filter by [field] (if needed, requires spec update)

Awaiting decision before implementing.
```

### Rule 3: Mark Everything Unsourced

| Marker | When to Use |
|--------|------------|
| `[DEMO COPY]` | Text content you wrote because the spec doesn't provide copy |
| `[DESIGN DECISION — not in source docs]` | Any visual/UX choice not backed by a document |
| `[GAP]` | Missing specification that blocks implementation |
| `[DEMO DATA]` | Mock data you invented for demo purposes |

### Rule 4: Spec-Only Feedback in Reviews
When reviewing existing screens, ALL feedback must trace to source documents.

**FAIR GAME to flag:**
- Wrong color (doesn't match UIDD token) → cite UIDD §X
- Missing field that's in the PRD → cite PRD §X
- Layout doesn't match task spec → cite Task TX.X
- Label mapping bug (code shows `TECH_IT` instead of "Technology & IT")

**NOT fair game:**
- "This page should have search" (if search isn't in the spec)
- "Users would benefit from pagination" (if pagination isn't specified)
- "The empty state should have an illustration" (if not specified)
- "I'd add a confirmation modal here" (if not in the task)

### Rule 5: When in Doubt, Ask
The cost of asking is 30 seconds. The cost of building an unspecified feature is hours of development, review, and potential rollback.

---

## How to Enforce in AI Prompts

Add this block to EVERY prompt that involves building or reviewing UI:

```
## Zero Hallucination Policy

CRITICAL: Do NOT add features, fields, components, screens, copy text,
or design patterns that are not explicitly specified in the source
documents provided in this context.

If you encounter a gap in the specification:
1. Flag it with [GAP]: description
2. Propose 2-3 options
3. WAIT for approval before implementing

Mark all unsourced content:
- [DEMO COPY] for invented text
- [DESIGN DECISION — not in source docs] for unsourced visual choices
- [DEMO DATA] for invented mock data

Every design comment in reviews must include a document reference.
No reference = don't mention it.
```

---

## Document Extraction Protocol

Hallucinations also come from incomplete spec reading. AI tools often miss data stored in tables.

### The Bug
`python-docx`'s `doc.paragraphs` skips all tables. Critical data lives in tables:
- Scoring formulas
- Field validation rules
- Option codes and enums
- Privacy thresholds
- Role-permission matrices

### The Fix
```python
import docx
doc = docx.Document(path)

# Paragraphs
for p in doc.paragraphs:
    process(p.text)

# Tables (CRITICAL — do NOT skip)
for table in doc.tables:
    for row in table.rows:
        cells = [cell.text.strip() for cell in row.cells]
        process(cells)
```

For .xlsx: read ALL sheets. Secondary sheets contain lookup values, formulas, and enums.

### Never Say "Not In Doc" Without Checking Tables
If you've only read paragraphs and claim a rule "isn't documented" — you're wrong. Check tables first.

---

## Real Examples of Caught Hallucinations

From 100+ design sessions on a production B2B SaaS project:

| Session | Hallucination | How Caught |
|---------|--------------|------------|
| DS Review #4 | AI added search bar to a list page | PRD has no search requirement for MVP |
| DS Review #7 | AI suggested pagination for 50-row table | Spec says "show all" — dataset is small |
| Screen Assembly #2 | AI added "dark mode toggle" to settings | Zero mention in UIDD or PRD |
| Component Build #5 | AI created a notification bell organism | No notification system in MVP scope |
| Illustration Gen #3 | AI added a chat bubble to illustration | Product has no messaging feature |
| Design Audit #1 | AI flagged "missing empty state illustration" | UIDD doesn't specify illustration for empty states |

**Pattern:** Every hallucination "sounds reasonable." That's what makes them dangerous. The only defense is source tracing.

---

## Spec Cascade & Staleness Prevention

When specs change, ALL downstream artifacts must be updated:

```
PRD changes → update SRS → update UIDD → update Task descriptions → update Design Brief
```

**Critical risk:** Task descriptions in Jira/Notion become stale when upstream docs change. This causes developers to implement against outdated mental models.

**Prevention:**
1. When any doc changes, trigger a 5-point cascade check
2. Update task BODY text (not just summary/title)
3. Add `[Design Sync YYYY-MM-DD]` comment to each updated task
4. Never assume downstream artifacts are current — verify

---

## Summary

| Principle | Action |
|-----------|--------|
| Every element has a source | Cite PRD/UIDD/Task for every design choice |
| Flag gaps, don't fill them | Use [GAP] marker, propose options, wait |
| Mark unsourced content | [DEMO COPY], [DESIGN DECISION], [DEMO DATA] |
| Reviews are spec-only | No "nice-to-haves", no invented requirements |
| Read tables, not just paragraphs | Use full extraction protocol |
| Cascade updates | When docs change, update ALL downstream artifacts |
| When in doubt, ask | 30 seconds vs. hours of wasted work |
