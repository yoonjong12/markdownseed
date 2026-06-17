---
name: md-collab
disable-model-invocation: false
---

# md-collab — async collaboration message writing

Produce a message that a reader can act on without a follow-up question. The core invariant: **every message contains exactly one ask, with enough context to act on it without prior knowledge**.

## 1. Opening questions (ask before writing)

Ask both:

1. "Who is the reader, and what is their relationship to this work?"
2. "What is the one thing you need from them, and by when?"

If the user gives a deadline of "ASAP" or "when possible," push back: ask for a specific date. A message without a deadline is a request the reader can defer indefinitely.

## 2. Message types and their rules

### Type A: Request

Use when asking someone to do something.

Structure: **Context → Current state → Single ask → Deadline**

Rules:
- **RULE R1**: Context is one paragraph max. Reader must understand the situation without reading prior threads.
- **RULE R2**: One ask per message. Multiple asks go in separate messages or a numbered list where each item is independently actionable.
- **RULE R3**: Deadline is a specific date, not relative ("by June 20" not "by end of week").
- **RULE R4**: If the ask requires a decision, include the options explicitly.

### Type B: Status update

Use when informing a stakeholder of progress.

Structure: **What changed → What it means → What comes next**

Rules:
- **RULE U1**: Lead with the change, not the activity. "API integration is complete" not "I spent the week on the API integration."
- **RULE U2**: "What it means" is one sentence about consequence for the reader, not the writer.
- **RULE U3**: "What comes next" has a date or a blocker — not both, not neither.

### Type C: Handoff note

Use when transferring work to another person or agent.

Structure: **State of work → What is done → What is not done → Known risks → Where to find things**

Rules:
- **RULE H1**: "State of work" is one sentence: working / blocked / abandoned.
- **RULE H2**: "What is not done" section is mandatory. Incomplete handoffs cause regression.
- **RULE H3**: File paths, links, and commands are copy-pasteable. No "the file in the design folder."

### Type D: Review comment

Use when giving feedback on a document, code, or spec.

Structure: **Observation → Implication → Suggestion (optional)**

Rules:
- **RULE V1**: One comment per block of text. Do not batch multiple issues into one comment.
- **RULE V2**: Observation is factual, not evaluative. "Section 2 has no success criteria" not "Section 2 is unclear."
- **RULE V3**: Suggestion is optional — a valid comment can be observation + implication only.

## 3. Language rules (all types)

- **RULE L1**: No indirect requests. "Can you review this?" → "Review this by [date]."
- **RULE L2**: No justification padding. State the ask, not why the reader should want to do it.
- **RULE L3**: Greeting and sign-off are optional. Never mandatory.

## 4. Skill args

- First positional arg: message type (`request`, `update`, `handoff`, `review`) — if omitted, ask.
- `--lang=ko` / `--lang=en`: output language (default: match user's message)
- `--reader=`: reader description (e.g. `비개발자 PM`, `에이전트`, `팀 리드`) — changes register and assumption level
