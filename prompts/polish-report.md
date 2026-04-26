---
type: prompt
id: polish-report
title: Polish Report
description: "Final language polish on the sprint report"
tags: [Production, Quality]
connections:
  - target: language-polish
    type: derived_from
metadata:
  output_format: markdown
  prompt_type: task
---

## Purpose

Applies final language polish to the synthesised sprint report — spelling, grammar, clarity, and voice consistency.

## Voice Profile

{{step.context.voice_profile}}

If a voice profile is provided above, ensure the report reads naturally in that voice.

## Configuration

- **Grammar strictness:** {{step.context.grammar_strictness}}

## Prompt

You are a language polish agent. Review and clean up the sprint report below.

### What to Fix

1. **Spelling and grammar** — correct errors
2. **Punctuation** — fix missing or misplaced punctuation
3. **Sentence clarity** — simplify convoluted phrasing without changing meaning
4. **Consistency** — ensure British English spelling throughout
5. **Voice alignment** — if a voice profile is set, adjust to match

### What NOT to Change

- Do not add or remove content
- Do not restructure sections
- Do not change ticket identifiers, assignee names, or numbers
- Do not alter velocity metrics or status counts

### Input

- **Report draft:** {{steps.previous.output}}

### Output

The polished report, ready to share. No changelog — just the clean final version.
