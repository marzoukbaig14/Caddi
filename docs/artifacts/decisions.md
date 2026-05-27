# Caddi Decisions Log

Append-only. Newest at bottom.

## Format

Every entry follows this template:

```
## DEC-NNNN — YYYY-MM-DD — Short title

**Status:** Locked | Open | Revised | Superseded
**Phase:** 0
**Tags:** [tag1, tag2]

**What**
The decision in one or two sentences.

**Why**
The reasoning.

**Open**
Anything related but unresolved. Write "None" if nothing.

**Related:** DEC-XXXX (optional)
**Supersedes:** DEC-XXXX (optional)

---
```

## Rules

- Append only. Never edit past entries.
- If a decision is reversed, write a new entry that supersedes the old one.
- IDs are sequential and never reused, even if a decision is later superseded.
- Date in ISO format (YYYY-MM-DD).
- Tags are lowercase and brief. Suggested vocabulary: foundational, scope, architecture, behavior, data, ops, hygiene, naming, principles, tech, roadmap.

---

## DEC-0001 — 2026-05-26 — Product thesis

**Status:** Locked
**Phase:** 0
**Tags:** [foundational, scope]

**What**
Caddi is a conversational planning agent that helps each user build their own personalized planning system through chat, then maintains it. The conversation is the product. Structured data is a byproduct.

**Why**
Existing AI planners start with a database schema and add a chatbot. Months of personal usage with a planner-style Claude Project proved that chat-first with structure-as-byproduct is the pattern that actually works. The differentiator has to be the inversion, not feature parity.

**Open**
None.

---

## DEC-0002 — 2026-05-26 — V1 scope is Planning only

**Status:** Locked
**Phase:** 0
**Tags:** [scope, foundational]

**What**
The product will eventually have three modules: Planning, Journal, Analysis. V1 ships with Planning only. Hard line.

**Why**
Each module is useful standalone. Planning is the most validated (months of personal usage data). Journal and Analysis can be added once Planning is real and used.

**Open**
Module 2 (Journal) and Module 3 (Analysis) scope to be defined later.

---

## DEC-0003 — 2026-05-26 — Anti-features list

**Status:** Locked
**Phase:** 0
**Tags:** [scope, principles]

**What**
Never propose streaks, productivity scores, badges, gamification, auto-scheduling to calendar, social leaderboards, or pre-defined domain modules.

**Why**
Streaks and scores damage diary trust (users lie to protect the streak). Auto-scheduling is a different product space (Motion's). Pre-defined domain modules contradict the thesis of emergent structure.

**Open**
None.

---

## DEC-0004 — 2026-05-26 — Three-layer behavior architecture

**Status:** Locked
**Phase:** 0
**Tags:** [architecture, behavior, principles]

**What**
The assistant's behavior is structured in three layers. Layer 1: designer rules (set by us, immutable, hardcoded in system prompt). Layer 2: user preferences (set by user through conversation, stored per user). Layer 3: emergent judgment (assistant decides in the moment within layers 1 and 2).

**Why**
Predictable behavior at the safety floor, configurable in the middle, fluid where it matters most. Maps to Wallach and Allen's hybrid top-down plus bottom-up framing ("Moral Machines: Teaching Robots Right from Wrong," 2008).

**Open**
The exact content of Layer 1 (the designer rules themselves) is Task 3 of Phase 0.

---

## DEC-0005 — 2026-05-26 — Data model is primitives plus generic tools plus finite widgets

**Status:** Locked
**Phase:** 0
**Tags:** [architecture, data]

**What**
Small set of primitives: item with flexible attributes, recurrence rule, progress counter, custom status set, note, link. Generic tool calls operating on primitives. Finite widget set rendering primitives. Domain concepts emerge from combinations, never hardcoded.

**Why**
Hardcoded modules are rigid and don't fit real users. Generic primitives let any user concept the assistant can describe be tracked, rendered, and reasoned about.

**Open**
The exact primitive attributes, the exact tool signatures, and the exact widget set are Tasks 4, 5, 6 of Phase 0.

---

## DEC-0006 — 2026-05-26 — Asymmetry rule

**Status:** Locked
**Phase:** 0
**Tags:** [architecture, principles]

**What**
Be flexible at the conversation and data layers (users shape almost anything). Be rigid at the safety and reliability layers (state mutations only via tool calls, designer rules never violated).

**Why**
Without rigidity at the safety layer, the assistant hallucinates state and the product becomes unreliable. Without flexibility at the conversation layer, the product becomes a normal planner and loses its thesis.

**Open**
None.

---

## DEC-0007 — 2026-05-26 — No fine-tuning in v1

**Status:** Locked
**Phase:** 0
**Tags:** [behavior, tech, scope]

**What**
V1 uses prompt engineering plus tool definitions plus context management. No fine-tuning of model weights.

**Why**
Prompt changes are instant. Fine-tunes are slow and expensive. Most behavior can be specified in a system prompt. No usage data exists yet to fine-tune on.

**Open**
Fine-tuning is a Phase 7 option once real usage data exists.

---

## DEC-0008 — 2026-05-26 — Roadmap shape

**Status:** Locked
**Phase:** 0
**Tags:** [roadmap, ops]

**What**
Seven phases. Phase 0 (behavior and product spec, no code), Phase 1 (system design, no code), Phase 2 (tech stack), Phase 3 (walking skeleton), Phase 4 (real v1), Phase 5 (portfolio polish), Phase 6 (modules 2 and 3), Phase 7 (possible fine-tuning and specialized models).

**Why**
Behavior is the product, so it comes first. Code starts at Phase 3 once design is locked. Polish happens late so cycles aren't wasted polishing things that get thrown away.

**Open**
Time-boxes per phase. Suggested Phase 0 = 2 weeks, Phase 3 = 2 weeks. Confirm and lock when ready.

---

## DEC-0009 — 2026-05-26 — Project name is Caddi (working name)

**Status:** Locked
**Phase:** 0
**Tags:** [naming]

**What**
The project is called Caddi. Metaphor is the golf caddy: carries your stuff, knows the course, advises but doesn't take the swing.

**Why**
Strong metaphor for what the product actually is. Short, memorable, fast to type.

**Open**
Domain availability and trademark check needed before production. A dating app already exists with the name in app stores, "Caddy" is a known web server, and a Japanese B2B company called Caddi exists. May need to rename before production. Acceptable as a working name for now.

---

## DEC-0010 — 2026-05-26 — Project operations standing rule

**Status:** Locked
**Phase:** 0
**Tags:** [ops, hygiene]

**What**
Locked decisions sync to project files immediately. Chats export to backup weekly. Decisions log is append-only. This runs in parallel with all phases.

**Why**
The user previously lost months of design data when a Claude chat was deleted. Project hygiene prevents this from happening again and keeps multi-chat workflow aligned.

**Open**
None.

---

## DEC-0011 — 2026-05-26 — Decisions log format

**Status:** Locked
**Phase:** 0
**Tags:** [ops, hygiene]

**What**
Every decision logged uses a structured markdown format with stable ID (DEC-NNNN), date, status, phase, tags, and structured fields (What, Why, Open, Related, Supersedes). Append-only. See template at top of this file.

**Why**
Consistent structure makes the log machine-parseable for future mining or analysis. Stable IDs allow cross-referencing. Tags allow categorical filtering. Append-only with explicit Supersedes preserves the full reasoning history.

**Open**
None.

---

## DEC-0012 — 2026-05-26 — Storage and version control

**Status:** Locked
**Phase:** 0
**Tags:** [ops, hygiene, tech]

**What**
Project lives in a private GitHub repo named "caddi." Folder structure: README at root, docs/ (instructions, context, decisions, artifacts/), chats/ (exported Claude conversations), code/ (Phase 3 onward).

**Why**
Version control on design docs captures the evolution of thinking, not just the current state. GitHub is the same place the eventual code will live, so the project history is unified. Going public in Phase 5 makes the whole design process part of the portfolio.

**Open**
None.

---