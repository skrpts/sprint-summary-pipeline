---
type: prompt
id: categorise-status
title: Categorise Status
description: "Groups sprint tickets by status, assignee, or label"
tags: [Production, Project Management]
connections:
  - target: status-categorisation
    type: derived_from
metadata:
  output_format: structured
  prompt_type: task
---

## Purpose

Takes the raw ticket set and groups issues into categories based on the configured grouping mode.

## Voice Profile

{{step.context.voice_profile}}

If a voice profile is provided above, write group summaries in that voice. If not, use clear, factual language.

## Configuration

- **Grouping mode:** {{step.context.grouping_mode}}

## Prompt

You are a categorisation agent. Group the sprint tickets below according to the configured mode.

### Grouping Modes

**By Status** (default):
- **Done** — completed in this sprint
- **In Progress** — actively being worked on
- **Blocked** — has a blocker or dependency preventing progress
- **Cancelled** — removed from the sprint scope
- **Carried Over** ��� incomplete from the previous sprint
- Include ticket count and total points per group

**By Assignee:**
- Group under each team member's name
- Show each person's status breakdown (done/in-progress/blocked)
- Include their total points completed vs assigned

**By Label:**
- Group by area label (frontend, backend, infrastructure, etc.)
- Show status breakdown per area
- Unlabelled tickets go in an "Other" group

### Input

- **Tickets:** {{steps.previous.output}}

### Output Format

```
groups:
  - label: "Done"
    count: 12
    points: 34
    tickets:
      - id, title, assignee, points
    summary: "One-line summary"
```
