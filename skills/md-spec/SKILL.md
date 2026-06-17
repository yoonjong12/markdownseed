---
name: md-spec
description: "Write a precise agent or system specification in markdown. Invoke when the user needs to define behavior for an AI agent, workflow, API contract, or system component — e.g. 'write a spec', 'agent 명세 작성', '시스템 스펙 써줘', 'define this agent', 'spec out the workflow'. Applies strict behavioral definition rules: action-first, no ambiguity, exceptions isolated."
disable-model-invocation: false
---

# md-spec — behavioral specification writing

Produce a spec that leaves zero ambiguity about what a system or agent does, under what conditions, and what it does not do. The core invariant: **every behavior is stated as a definite action or prohibition, never a possibility**.

## 1. Opening questions (ask before writing)

Ask both before writing:

1. "What is the name and single-sentence purpose of this agent/system?"
2. "Who or what calls it, and what do they expect back?"

These two answers define the contract boundary. If the user skips either, produce a stub and mark the gap with `[TBD: ...]`.

## 2. Judgment rules

### Definition rules

- **RULE D1**: Every behavior uses "does" or "does not". Never "can", "may", "might", "should".
- **RULE D2**: Inputs and outputs are defined before any behavior is described. A behavior without a typed interface is incomplete.
- **RULE D3**: Limits are explicit numbers. "Does not call external APIs more than once per request" — not "avoids excessive external calls."
- **RULE D4**: One action per bullet. Compound actions ("parses and validates and stores") are three bullets.

### Structure rules

- **RULE S1**: Section order is fixed: Purpose → Interface → Behavior → Exceptions → Out of Scope.
- **RULE S2**: "Out of Scope" section is mandatory. Ambiguity lives in unstated exclusions.
- **RULE S3**: Exceptions are in their own section, never inline with normal behavior.
- **RULE S4**: No prose in the Behavior section. Bullet list only.

### Language rules

- **RULE L1**: Subject is always the system/agent name, not "it" or "the system."
- **RULE L2**: No softening. "Returns an error" not "may return an error in some cases."
- **RULE L3**: Korean spec: use "한다" / "하지 않는다" endings. No "할 수 있다."

## 3. Template

```markdown
# [AgentName] — [one-line purpose]

## Interface

**Input**
```
{ field: type, field: type }
```

**Output**
```
{ field: type, field: type }
```

**Caller**: [who/what invokes this]
**Invocation**: [sync/async, trigger condition]

## Behavior

- [AgentName] [action] when [condition].
- [AgentName] does not [prohibited action].
- [AgentName] [action] at most [N] times per [unit].

## Exceptions

| Condition | Response |
|-----------|----------|
| [error condition] | [exact response — error type, message, side effects] |

## Out of Scope

- [AgentName] does not [capability that might be assumed but is not provided].
- [AgentName] does not persist state between invocations unless [explicit condition].
```

## 4. Confidence markers

When a behavior is not yet decided, mark it explicitly — never invent behavior:

```
- [AgentName] [TBD: decide whether to retry on timeout or fail fast]
```

TBD markers are visible contract gaps, not placeholders to be silently filled.

## 5. Skill args

- First positional arg: agent/system name
- `--lang=ko` / `--lang=en`: output language (default: match user's message)
- `--stub`: produce a skeleton with TBD markers only — useful for collaborative spec drafting
