# Caddi Decisions Log

Append-only. Newest at bottom. Each entry follows this format:

```
## YYYY-MM-DD: Short title

Status: Locked | Open | Revised
What: one-line summary
Why: reasoning
Open: anything still unresolved related to this decision
```

If a decision is reversed or modified later, write a new entry referencing the old one. Never edit past entries.

---

## 2026-05-26: Product thesis

Status: Locked
What: Caddi is a conversational planning agent that helps each user build their own personalized planning system through chat, then maintains it. The conversation is the product. Structured data is a byproduct.
Why: Existing AI planners start with a database schema and add a chatbot. The user's months of usage with a planner-style Claude Project proved that chat-first with structure-as-byproduct is the pattern that actually works. The differentiator has to be the inversion, not feature parity.
Open: None.

---

## 2026-05-26: V1 scope is Planning only

Status: Locked
What: The product will eventually have three modules: Planning, Journal, Analysis. V1 ships with Planning only. Hard line.
Why: Each module is useful standalone. Planning is the most validated (months of usage data). Journal and Analysis can be added once Planning is real and used.
Open: None for v1. Module 2 and 3 scope to be defined later.

---

## 2026-05-26: Anti-features list

Status: Locked
What: Never propose streaks, productivity scores, badges, gamification, auto-scheduling to calendar, social leaderboards, or pre-defined domain modules.
Why: Streaks and scores damage diary trust (users lie to protect the streak). Auto-scheduling is a different product (Motion's space). Pre-defined domain modules contradict the thesis of emergent structure.
Open: None.

---

## 2026-05-26: Three-layer behavior architecture

Status: Locked
What: The assistant's behavior is structured in three layers. Layer 1: designer rules (set by us, immutable, hardcoded in system prompt). Layer 2: user preferences (set by user through conversation, stored per user). Layer 3: emergent judgment (assistant decides in the moment within layers 1 and 2).
Why: Predictable behavior at the safety floor, configurable in the middle, fluid where it matters most. Maps to Wallach and Allen's hybrid top-down plus bottom-up framing ("Moral Machines," 2008).
Open: The exact content of Layer 1 (the designer rules themselves) is Task 3 of Phase 0.

---

## 2026-05-26: Data model is primitives plus generic tools plus finite widgets

Status: Locked
What: Small set of primitives (item with flexible attributes, recurrence rule, progress counter, custom status set, note, link). Generic tool calls operating on primitives. Finite widget set rendering primitives. Domain concepts emerge from combinations, never hardcoded.
Why: Hardcoded modules are rigid and don't fit real users. Generic primitives let any user concept the assistant can describe be tracked, rendered, and reasoned about.
Open: The exact primitive attributes, the exact tool signatures, and the exact widget set are Tasks 4, 5, 6 of Phase 0.

---

## 2026-05-26: Asymmetry rule (flexible at conversation, rigid at safety)

Status: Locked
What: Be flexible at the conversation and data layers (users shape almost anything). Be rigid at the safety and reliability layers (state mutations only via tool calls, designer rules never violated).
Why: Without rigidity at the safety layer, the assistant hallucinates state and the product becomes unreliable. Without flexibility at the conversation layer, the product becomes a normal planner and loses its thesis.
Open: None.

---

## 2026-05-26: No fine-tuning in v1

Status: Locked
What: V1 uses prompt engineering plus tool definitions plus context management. No fine-tuning of model weights.
Why: Prompt changes are instant, fine-tunes are slow and expensive. Most behavior can be specified in a system prompt. No usage data exists yet to fine-tune on.
Open: Fine-tuning is a Phase 7 option once real usage data exists.

---

## 2026-05-26: Roadmap shape

Status: Locked
What: Seven phases. Phase 0 (behavior and product spec, no code), Phase 1 (system design, no code), Phase 2 (tech stack), Phase 3 (walking skeleton), Phase 4 (real v1), Phase 5 (portfolio polish), Phase 6 (modules 2 and 3), Phase 7 (possible fine-tuning and specialized models).
Why: Behavior is the product, so it comes first. Code starts at Phase 3 once design is locked. Polish happens late so we don't waste cycles polishing things that get thrown away.
Open: Time-boxes per phase. Suggested: Phase 0 = 2 weeks, Phase 3 = 2 weeks. Confirm and lock when ready.

---

## 2026-05-26: Project name is Caddi (working name)

Status: Locked (working name)
What: The project is called Caddi. Metaphor is the golf caddy (carries your stuff, knows the course, advises but doesn't take the swing).
Why: Strong metaphor for what the product actually is. Short, memorable, fast to type.
Open: Domain availability and trademark check needed before production. A dating app already exists with the name in app stores, and Caddy is a known web server, and there is a Japanese B2B company called Caddi. May need to rename before production. Acceptable as a working name for now.

---

## 2026-05-26: Project operations standing rule

Status: Locked
What: Locked decisions sync to project files immediately. Chats export to backup weekly. Decisions log is append-only. This runs in parallel with all phases.
Why: The user previously lost months of design data when a Claude chat was deleted. Project hygiene prevents this from happening again and keeps multi-chat workflow aligned.
Open: None.

---

## Template for new entries

```
## YYYY-MM-DD: Short title

Status: Locked | Open | Revised
What:
Why:
Open:
```
