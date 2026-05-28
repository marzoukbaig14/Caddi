# Project Context: Caddi

This file holds the product context, locked decisions, roadmap, and reference material for the project. It is not behavior-shaping (that is in `instructions.md`). Chats read this when they need detail on what's being built and what's already been decided.

## Product thesis (locked, DEC-0001)

Caddi is a conversational planning agent that helps each user build their own personalized planning system through chat, then maintains it. The conversation is the product. Structured data is a byproduct.

This is NOT a planner with AI bolted on. NOT a chatbot with a todo list attached. Other AI planners (Motion, Reclaim, Sunsama, Mei, Saner.ai) start with a database schema and add a chatbot. Caddi starts with a chat and extracts structure from it.

## V1 scope (locked, DEC-0002)

Three modules eventually: Planning, Journal, Analysis.
V1 ships with Planning only. Hard line.

V1 includes:
- Conversational onboarding (assistant interviews user, proposes structure)
- Fluid taxonomy (user-defined categories, urgency tiers, time horizons)
- Items with attributes and recurrence rules
- Adding, updating, moving items through conversation
- Urgency-weighted probabilistic nudges
- State persistence and integrity (no hallucinated state)
- Right-sized intelligence (asks when ambiguous, doesn't when obvious)

V1 excludes (defer to module 2 or 3):
- Journal entries
- Mood, energy, sleep tracking
- Pattern noticing and analysis
- Recaps and stats
- Voice, photo, calendar integrations
- Sharing and accountability features

## Anti-features (locked, DEC-0003)

Never propose:
- Streaks
- Productivity scores or grades
- Badges and gamification
- Auto-scheduling to calendar
- Social leaderboards or comparisons
- Pre-defined domain modules (e.g. hardcoded "outreach tracker" or "learning tracker")

## Architectural decisions

### Three behavior layers (locked, DEC-0004)

1. Designer rules. Set by the product team. Immutable. Hardcoded in the system prompt.
2. User preferences. Set by the user through conversation. Stored per user.
3. Emergent judgment. Assistant decides in the moment within layers 1 and 2.

Hybrid top-down plus bottom-up design in the Wallach and Allen sense ("Moral Machines: Teaching Robots Right from Wrong," 2008).

### Data model (locked, DEC-0005)

- Small primitive set: item with flexible attributes, recurrence rule, progress counter, custom status set, note, link.
- Generic tool calls operating on primitives. Not domain-specific.
- Finite widget set rendering the primitives.
- Domain concepts emerge from primitive combinations, never from hardcoded modules.

### Asymmetry rule (locked, DEC-0006)

- Flexible at the conversation and data layers.
- Rigid at the safety and reliability layers.

### Behavior approach (locked, DEC-0007)

- "Tuning" means system prompt plus tool definitions plus context management.
- No fine-tuning in v1. Prompt engineering covers it.
- Fine-tuning is a phase 7 option, once real usage data exists.

## Roadmap (locked, DEC-0008)

| Phase | What | Code? |
|---|---|---|
| 0 | Behavior and product spec | No |
| 1 | System design (storage, conversation flow, UI shell, API surface) | No |
| 2 | Tech stack decisions | No |
| 3 | Walking skeleton (ugly working prototype, user as only user) | Yes |
| 4 | Real v1 (auth, persistence, decent UI, onboarding, deploy) | Yes |
| 5 | Portfolio polish (demo mode, case study, video, design pass) | Yes |
| 6 | Modules 2 (Journal) and 3 (Analysis) | Yes |
| 7 | Possible fine-tuning, specialized smaller models, deeper analysis | Yes |

Currently in Phase 0.

## Phase 0 task list

Order matters.

| # | Task | Status |
|---|---|---|
| 0 | Name the project | Done (Caddi, working name, DEC-0009) |
| 1 | Lock the v1 thesis in one written line | Done (DEC-0001) |
| 2 | Mine old handoff doc and current planner chat for behavior input | In progress |
| 3 | Draft the behavior spec / system prompt (Layer 1 designer rules) | Not started |
| 4 | Define tool call signatures (5 to 8 generic tools) | Not started |
| 5 | Define primitives concretely (full attribute set) | Not started |
| 6 | Define widget set (4 to 6 widgets mapped to primitive shapes) | Not started |
| 7 | Write v1 user flow end to end as a narrative | Not started |
| 8 | Define v1 success criteria | Not started |

Recommended execution order: 2 (mining inputs), then 3 (behavior spec). Tasks 4 through 6 (tools, primitives, widgets) are tightly coupled and should be worked together. Tasks 7 and 8 close out Phase 0.

## Project hygiene (locked, DEC-0010, DEC-0011, DEC-0012)

- Locked decisions sync to project files immediately.
- Chats export to backup weekly.
- Decisions log is append-only with sequential DEC-NNNN IDs.
- Project lives in a private GitHub repo named "caddi" with structure: README at root, docs/ (instructions, context, decisions, artifacts/), chats/, code/.
- The Claude project instructions and knowledge files have twin copies in the repo. Edit both together.

## Inputs the user has

- A handoff document from a deleted older planner Claude chat. Months of refined usage encoded into its structure.
- A current Claude planner chat, about a week old, being used as a deliberate prototype going forward.
- This project's brainstorming chats.

## Competitive landscape

The product sits at the intersection of three existing categories:

1. AI planners that auto-schedule: Motion, Reclaim, Sunsama, Akiflow. Different problem space (they optimize calendar, not conversation).
2. Conversational AI assistants: Mei (SMS-based), Saner.ai, others. Closest competitors in spirit. Mostly text-message-based, light on the diary and pattern angle.
3. Mood and journaling apps: Day One, Daylio, Stoic, Rosebud. Rosebud is most relevant (AI journal that asks follow-ups). No real task management.

Caddi sits at the intersection, with the productivity log over time as the long-term moat. Nobody is doing this combination well as of the design conversation.

## Design rationale highlights

**Why conversation-first, not features-first.** The user has months of usage with a planner-style Claude chat. The pattern that worked was chat for input, structured state as byproduct, no fixed modules. Trying to convert that into a traditional planner with a chatbot layer would lose the magic. So the product is built around the chat being the primary interface.

**Why generic primitives, not domain modules.** A "Karpathy tracker" or "outreach tracker" feels useful but is rigid. Real users have idiosyncratic needs. A small set of generic primitives plus custom attributes plus flexible categories covers any user concept the assistant can describe.

**Why finite tool calls, despite wanting fluidity.** LLMs hallucinate. If state is "what the model said it is," it drifts, forgets, and invents. Tool calls bridge conversation to persistent storage. They are invisible to the user but essential for reliability.

**Why no fine-tuning in v1.** Prompt changes are instant. Fine-tunes are slow and expensive. Most behavior can be specified in a system prompt. Fine-tuning becomes worth it once you have real usage data to train on (Phase 7).

**Why no streaks or scores.** They damage diary trust. Users lie to the app to protect the streak or boost the score. The product's long-term value is the truth of the productivity log. Anti-features.

## Reference: Wallach and Allen framework

The architectural framing draws on top-down vs bottom-up approaches to autonomous system ethics:

- Top-down: programmed rules and hierarchies. Asimov's Three Laws style. Deontological logic.
- Bottom-up: behavior emerges from learning, experience, evolution. Reinforcement learning. Virtue ethics.
- Hybrid: top-down rules as guardrails, with context-sensitive judgment emerging underneath.

Caddi is a hybrid: designer rules are the immutable floor, user preferences are configurable, emergent assistant judgment fills the rest.

Reference: Wendell Wallach and Colin Allen, "Moral Machines: Teaching Robots Right from Wrong," Oxford University Press, 2008.

## How chats in this project relate

The user is treating this project modularly. Different chats handle different scoped tasks. A typical structure:

- Main / direction chat: high-level brainstorming, prioritization, decision tracking. Persistent.
- Naming chat: short, focused on producing a project name.
- Input mining chat: analyzes the old handoff doc, extracts behavior patterns.
- Behavior spec chat: drafts and iterates the system prompt for the product. The big one.
- Data model chat: designs primitives, tool calls, and widgets together.
- User flow chat: writes the day-in-the-life narrative that stress-tests the spec.
- Optional: competitor deep-dive chat, prototype observation log.

Decisions made in any chat should be reflected back in `instructions.md`, `context.md`, or `decisions.md` so future chats stay aligned.