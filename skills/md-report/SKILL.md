---
name: md-report
disable-model-invocation: false
---

# md-report — decision-first report writing

Produce a markdown report that a busy reader can scan in 30 seconds and still make the right decision. The core invariant: **the reader should know the recommendation before reading any detail**.

## 1. Opening question (always ask first)

Before writing, ask one question:

> "What decision does this report need to support?"

The answer anchors every structural choice. If the user cannot answer, help them narrow it down — a report without a decision is a data dump.

## 2. Judgment rules

Apply all rules. There are no exceptions within a report.

### Structure rules

- **RULE S1**: First paragraph = recommendation or conclusion. Never background. Never scope.
- **RULE S2**: Each top-level section (`##`) opens with a one-sentence summary of what that section proves.
- **RULE S3**: Sections are limited to: Recommendation, Basis, Comparison, Risk, Appendix. No "Overview", "Introduction", or "Summary" sections — the first paragraph is already the summary.
- **RULE S4**: If there are more than 3 options to compare, use a table. Table columns = decision criteria only (not raw specs).

### Content rules

- **RULE C1**: Every claim has one of: a number, a name, or a direct consequence. Vague claims ("it is better") are forbidden.
- **RULE C2**: Technical specs belong in Appendix, not in the body. The body contains only decision-relevant facts.
- **RULE C3**: If a section has more than 5 bullet points, convert to prose or a table. Long bullet lists are a sign of uncommitted structure.

### Language rules

- **RULE L1**: Active voice. "We recommend X" not "X is recommended."
- **RULE L2**: One idea per sentence. Split sentences with more than two clauses.
- **RULE L3**: No hedge stacking ("it might potentially be somewhat better"). Pick one hedge or remove all.

## 3. Template

```markdown
**Recommendation: [one-line decision]**

[2–3 sentences: the key reason this is the right call, with one concrete number or fact.]

## Basis

[Section summary sentence.]

[Supporting points — 3 to 5 max. Each backed by a number, name, or outcome.]

## Comparison

[Table if ≥3 options. Columns = decision criteria only.]

| Criterion | Option A | Option B (recommended) | Option C |
|-----------|----------|------------------------|----------|
| ...       | ...      | ...                    | ...      |

## Risk

[What could make this recommendation wrong. One paragraph.]

## Appendix (optional)

[Raw specs, full data, methodology — only if the user needs it on record.]
```

## 4. Length guidance

- Short report (single decision, 1–2 options): 200–400 words
- Standard report (3+ options, multi-criteria): 400–800 words
- Long report (strategic, multi-stakeholder): 800–1500 words

Never exceed the length the decision requires. If you find yourself writing past the guidance, audit for rule C2 violations (specs in the body).

## 5. Argument args

- First positional arg: the topic/domain (e.g., `API vendor selection`, `팀 온보딩 도구`)
- `--lang=ko` / `--lang=en`: output language (default: match the user's message language)

If no topic is given, ask before writing.
