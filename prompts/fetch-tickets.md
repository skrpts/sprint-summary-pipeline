---
type: prompt
id: fetch-tickets
title: Fetch Tickets
description: "Retrieves and structures sprint tickets from Linear via MCP"
tags: [Production, Project Management]
inputs:
  team:
    label: "Team"
    description: "Linear team name or ID"
    example: "Engineering"
    required: true
    type: text
  sprint:
    label: "Sprint"
    description: "Sprint or cycle name. Leave empty for the current active cycle."
    example: "Sprint 24"
    required: false
    type: text
connections:
  - target: fetch-linear-tickets
    type: derived_from
metadata:
  output_format: structured
  prompt_type: task
---

## Purpose

Fetches all issues in a sprint cycle from Linear and structures them for downstream analysis.

## Prompt

You are a data retrieval agent. Using the Linear MCP server, fetch all tickets for the specified sprint.

### Steps

1. Call `linear_search_issues` with the team filter set to the specified team. Filter by the current active cycle (or the named sprint if specified).
2. For each issue, collect: title, identifier (e.g. ENG-123), status (todo, in progress, done, cancelled), assignee, priority (urgent, high, medium, low, none), labels, and point estimate.
3. Identify carry-over issues — tickets that were open at the end of the previous cycle and appear in this one. Mark them with a carry-over flag.
4. If the team has many issues (50+), paginate using the `limit` parameter to ensure all tickets are captured.

### Input

- **Team:** {{input.team}}
- **Sprint:** {{input.sprint}} (default: current active cycle)

### Output Format

Return a structured ticket set:

```
sprint:
  name: "Sprint 24"
  team: "Engineering"
  start_date: "2025-03-03"
  end_date: "2025-03-14"

tickets:
  - id: "ENG-123"
    title: "Implement user onboarding flow"
    status: "done"
    assignee: "Jane Smith"
    priority: "high"
    labels: ["frontend", "onboarding"]
    points: 5
    carry_over: false
```

### Error Handling

- If the team is not found, report the error with available team names
- If no active cycle exists, report this and suggest using a sprint name
