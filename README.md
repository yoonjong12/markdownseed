# markdownseed

A Claude Code plugin that injects **senior technical writer judgment** into markdown documents. Three on-demand skills cover the document types where consistency matters most: decision reports, behavioral specs, and async collaboration messages.

It does not enforce a writing style or suppress Claude's defaults — it gives the agent a structured set of judgment rules so the same context produces the same quality every session.

## Skills

| Command | Description |
|---------|-------------|
| `/markdownseed:md-report` | Write a decision-first report. Asks what decision the report must support, then applies structure, content, and language rules to keep conclusions up front and specs out of the body. |
| `/markdownseed:md-spec` | Write a behavioral specification for an agent or system. Enforces typed interfaces, action-only language ("does"/"does not", never "can"/"may"), and a mandatory Out of Scope section. |
| `/markdownseed:md-collab` | Write an async collaboration message: request, status update, handoff note, or review comment. Enforces single-ask structure, deadline requirement, and context-first ordering. |

## Installation

```
/plugin marketplace add yoonjong12/markdownseed
/plugin install markdownseed@markdownseed
```

---

## Why on-demand, not CLAUDE.md

Unlike always-on instruction files, these are `SKILL.md`-based — loaded only when invoked. Markdown judgment rules are irrelevant when you are debugging a service or writing a migration; injecting them into every session wastes context. Call the skill when you need it, and the rest of your sessions stay unaffected.

---

## Skill: `md-report`

Write a report where the reader knows the recommendation before reading any detail.

```
/md-report API vendor selection
/md-report 온보딩 도구 비교 --lang=ko
```

The skill opens by asking what decision the report must support. Every structural choice follows from that answer: section order, table columns, and length target.

**Core rules:**
- First paragraph = recommendation. Never background.
- Each section opens with a one-sentence proof statement.
- Technical specs go in Appendix, not the body.
- Comparison tables contain decision criteria only — not raw specs.

---

## Skill: `md-spec`

Write a behavioral specification with no ambiguity about what a system does, under what conditions, and what it explicitly does not do.

```
/md-spec RecommendationAgent
/md-spec DataPipeline --stub
```

`--stub` produces a skeleton with `[TBD: ...]` markers — useful for collaborative spec drafting before behavior is decided.

**Core rules:**
- Inputs and outputs defined before any behavior.
- Every behavior uses "does" or "does not" — never "can", "may", "might".
- One action per bullet. No compound actions.
- Out of Scope section is mandatory.

---

## Skill: `md-collab`

Write an async message a reader can act on without a follow-up question.

```
/md-collab request --reader=팀 리드
/md-collab handoff
/md-collab review --lang=en
```

Message types: `request`, `update`, `handoff`, `review`. If omitted, the skill asks.

**Core rules:**
- One ask per message. Deadline is a specific date.
- Status updates lead with the change, not the activity.
- Handoff notes must include a "What is not done" section.
- Review comments: observation → implication → suggestion (suggestion optional).

---

## License

MIT © 2026 yoonjong12
