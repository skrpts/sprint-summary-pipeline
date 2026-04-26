---
type: workflow
id: sprint-summary-pipeline
title: Sprint Summary Pipeline
description: "Fetches sprint tickets from Linear via MCP, analyses status and velocity, and generates a stakeholder-ready report"
tags: [Production, Project Management]
connections:
  - target: ticket-fetch
    type: uses
  - target: status-categorisation
    type: uses
  - target: velocity-analysis
    type: uses
  - target: report-synthesis
    type: uses
  - target: language-polish
    type: uses
  - target: linear-mcp
    type: runs_on
  - target: llm-service
    type: runs_on
metadata:
  estimated_duration: "20-60 seconds"
  avg_tokens: 15000
  trigger: manual
output_step: "language-polish"
composite_steps:
  - "ticket-fetch"
  - "status-categorisation"
  - "velocity-analysis"
  - "report-synthesis"
  - "language-polish"
execution:
  - skill: "ticket-fetch"
    step_type: "generation"
    prompt: "fetch-tickets"
  - parallel:
    - skill: "status-categorisation"
      step_type: "synthesis"
      prompt: "categorise-status"
    - skill: "velocity-analysis"
      step_type: "synthesis"
      prompt: "analyse-velocity"
  - skill: "report-synthesis"
    step_type: "synthesis"
    prompt: "synthesise-report"
  - skill: "language-polish"
    step_type: "content"
    prompt: "polish-report"
---

## Overview

This workflow produces a stakeholder-ready sprint summary from your Linear workspace. It fetches all tickets in a sprint cycle, runs two parallel analysis passes (status categorisation and velocity analysis), synthesises the results into a report, and applies a final language polish.

The report adapts to your audience: choose executive (brief, outcomes-focused), standard (balanced), or detailed (full per-ticket breakdown).

## Pipeline Stages

### Stage 1: Fetch Tickets

**Input:** Team name, sprint/cycle identifier

Using the Linear MCP service, fetch all issues in the specified sprint cycle with their metadata, statuses, assignees, priorities, labels, and point estimates.

**Output:** Structured ticket set.

### Stage 2: Parallel Analysis (Two Agents)

Two analysis agents run concurrently:

#### 2a. Status Categorisation

Groups tickets by status (Done, In Progress, Blocked, Cancelled, Carried Over), by assignee, or by label. Configurable via the `grouping_mode` persona dial.

#### 2b. Velocity Analysis

Computes points completed vs planned, completion rate, carry-over load, and risk flags. If previous sprint data is provided via the `velocity_context` dial, includes trend comparison.

### Stage 3: Report Synthesis

Combines the status breakdown and velocity metrics into a single report. Adapts to the target audience profile and report depth setting (Executive, Standard, Detailed).

### Stage 4: Language Polish

Final cleanup: spelling, grammar, clarity, and Voice Profile alignment. Uses British English throughout.

**Output:** Publication-ready sprint report.

## Error Handling

- If the Linear MCP server is unreachable, abort and report the connection error
- If the team is not found, report available team names
- If no active cycle exists, report this and suggest providing a sprint name
- If the ticket count is very high (100+), the fetch step paginates automatically

## Inputs

| Name | Required | Description | Example |
|------|----------|-------------|---------|
| `{{input.team}}` | Yes | Linear team name or ID | `Engineering` |
| `{{input.sprint}}` | No | Sprint/cycle name or number. Default: current active cycle. | `Sprint 24` |

## Outputs

| Name | Description |
|------|-------------|
| Sprint report | Formatted report in markdown with summary, status breakdown, velocity metrics, highlights, and risks |

## Setup

Before running this workflow:

1. **Linear MCP server** — install and configure the Linear MCP server in your skrptiq settings.
2. **API key** — generate a Linear API key at `linear.app/YOUR-TEAM/settings/api` and set it as `LINEAR_API_KEY`.
3. **Team access** — ensure the API key has access to the team you want to report on.

## Provider Notes

- Status categorisation and velocity analysis are analytical tasks — most models handle them well.
- Report synthesis benefits from a model with strong writing capabilities, especially for the executive summary.
- The pipeline is moderate on token usage — no long-context requirements.

## Example Input

To test this workflow immediately after import:

```
Team: Engineering
Sprint: (leave empty for current cycle)
```
