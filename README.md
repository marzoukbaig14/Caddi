# Caddi

A conversational planning agent that helps each user build their own personalized planning system through chat, then maintains it.

The conversation is the product. Structured data is a byproduct.

## Status

Phase 0 of 7. Behavior and product spec stage. No code yet.

## What this is

Not a planner with AI bolted on. Not a chatbot with a todo list attached. Other AI planners start with a database schema and add a chatbot. Caddi starts with a chat and extracts structure from it.

The user talks to Caddi about their life, ambitions, and current commitments. Caddi proposes a structure (categories, time horizons, urgency tiers) through conversation. The user shapes it. Items are added, updated, and reprioritized through chat. Probabilistic nudges surface what matters. State is persistent, structured, and visible.

## Repo structure

```
caddi/
├── README.md           you are here
├── docs/
│   ├── instructions.md the system prompt for Claude project chats
│   ├── context.md      reference material for chats
│   ├── decisions.md    append-only decisions log
│   └── artifacts/      design artifacts as they get produced
├── chats/              exported Claude conversations
└── code/               application code (Phase 3 onward)
```

## Roadmap

| Phase | What | Code? |
|---|---|---|
| 0 | Behavior and product spec | No |
| 1 | System design | No |
| 2 | Tech stack | No |
| 3 | Walking skeleton | Yes |
| 4 | Real v1 | Yes |
| 5 | Portfolio polish | Yes |
| 6 | Modules 2 (Journal) and 3 (Analysis) | Yes |
| 7 | Possible fine-tuning, specialized models | Yes |

See `docs/decisions.md` for locked decisions. See `docs/context.md` for full reference material.

## Working notes

This is a portfolio project with possible product trajectory. Design is happening through structured conversations with Claude in a Claude Project. All locked decisions are mirrored here so the design state survives outside any single chat.
