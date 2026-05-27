# Project Context: Reference Material

This file holds reference material for chats in the project. It is not behavior-shaping (that is in the instructions). Refer to this when you need detail on the roadmap, current task list, design rationale, or supporting context.

## Roadmap

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
| 0 | Name the project | Not started |
| 1 | Lock the v1 thesis in one written line | Concept locked, not formally written |
| 2 | Mine old handoff doc and current planner chat for behavior input | Not started |
| 3 | Draft the behavior spec / system prompt (Layer 1 designer rules) | Not started |
| 4 | Define tool call signatures (5 to 8 generic tools) | Not started |
| 5 | Define primitives concretely (full attribute set) | Not started |
| 6 | Define widget set (4 to 6 widgets mapped to primitive shapes) | Not started |
| 7 | Write v1 user flow end to end as a narrative | Not started |
| 8 | Define v1 success criteria | Not started |

Recommended execution order: 0 (naming), then 2 (mining inputs), then 3 (behavior spec). Tasks 4 through 6 (tools, primitives, widgets) are tightly coupled and should be worked together. Tasks 1, 7, 8 close out Phase 0.

## Inputs the user has

- A handoff document from a deleted older planner Claude chat. Months of refined usage encoded into its structure. To be uploaded as a knowledge file when ready to mine.
- A current Claude planner chat, about a week old, being used as a deliberate prototype going forward.
- This project's brainstorming chats.

## Competitive landscape

The product sits at the intersection of three existing categories:

1. AI planners that auto-schedule: Motion, Reclaim, Sunsama, Akiflow. Different problem space (they optimize calendar, not conversation).
2. Conversational AI assistants: Mei (SMS-based), Saner.ai, others. Closest competitors in spirit. Mostly text-message-based, light on the diary and pattern angle.
3. Mood and journaling apps: Day One, Daylio, Stoic, Rosebud. Rosebud is most relevant (AI journal that asks follow-ups). No real task management.

The product sits at the intersection, with the productivity log over time as the long-term moat. Nobody is doing this combination well as of the design conversation.

## Design rationale highlights

**Why conversation-first, not features-first.** The user has months of usage with a planner-style Claude chat. The pattern that worked was: chat for input, structured state as byproduct, no fixed modules. Trying to convert that into a traditional planner with a chatbot layer would lose the magic. So the product is built around the chat being the primary interface.

**Why generic primitives, not domain modules.** A "Karpathy tracker" or "outreach tracker" feels useful but is rigid. Real users have idiosyncratic needs. A small set of generic primitives plus custom attributes plus flexible categories covers any user concept the assistant can describe.

**Why finite tool calls, despite wanting fluidity.** LLMs hallucinate. If state is "what the model said it is," it drifts, forgets, and invents. Tool calls bridge conversation to persistent storage. They are invisible to the user but essential for reliability.

**Why no fine-tuning in v1.** Prompt changes are instant. Fine-tunes are slow and expensive. Most behavior can be specified in a system prompt. Fine-tuning becomes worth it once you have real usage data to train on (phase 7).

**Why no streaks or scores.** They damage diary trust. Users lie to the app to protect the streak or boost the score. The product's long-term value is the truth of the productivity log. Anti-features.

## Reference: Wallach and Allen framework

The architectural framing draws on top-down vs bottom-up approaches to autonomous system ethics:

- Top-down: programmed rules and hierarchies. Asimov's Three Laws style. Deontological logic.
- Bottom-up: behavior emerges from learning, experience, evolution. Reinforcement learning. Virtue ethics.
- Hybrid: top-down rules as guardrails, with context-sensitive judgment emerging underneath.

This product is a hybrid: designer rules are the immutable floor, user preferences are configurable, emergent assistant judgment fills the rest.

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

Decisions made in any chat should be reflected back in the instructions or this context file so future chats stay aligned.
