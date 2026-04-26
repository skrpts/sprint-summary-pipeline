---
type: skill
id: ticket-fetch
title: Ticket Fetch
description: "Retrieves sprint tickets from Linear via MCP — issues, statuses, assignees, and point values"
tags: [Production, Project Management]
connections:
  - target: linear-mcp
    type: runs_on
  - target: llm-service
    type: runs_on
---

## Capability

Fetches all issues in a sprint cycle (or project) from Linear using the MCP server. Collects issue metadata, status, assignee, priority, labels, and point estimates for downstream analysis.

## When to Use

- As the first step in a sprint summary or reporting pipeline
- When you need a snapshot of sprint progress

## What It Does

1. **Search issues** — calls `linear_search_issues` with the team and cycle/sprint filter to retrieve all issues in the current sprint
2. **Gather metadata** — for each issue: title, description, status (todo, in progress, done, cancelled), assignee, priority (urgent, high, medium, low, none), labels, and point estimate
3. **Include carry-overs** — identifies issues that were in the previous sprint but not completed, now carried into this one

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.team}}` | Yes | Linear team name or ID | `Engineering` |
| `{{input.sprint}}` | No | Sprint/cycle name or number. Default: current active cycle. | `Sprint 24` |

## Outputs

Structured ticket set: list of issues with title, status, assignee, priority, labels, points, and carry-over flag.
