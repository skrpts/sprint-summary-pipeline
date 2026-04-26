---
type: skill
id: status-categorisation
title: Status Categorisation
description: "Groups sprint tickets by status — done, in progress, blocked, cancelled, and carried over"
tags: [Production, Project Management]
connections:
  - target: llm-service
    type: runs_on
context_params:
  voice_profile:
    label: "Voice Profile"
    description: "Your writing style for status summaries"
    required: false
  grouping_mode:
    label: "Grouping Mode"
    description: "How to group tickets — By Status, By Assignee, or By Label"
    default: "By Status"
    required: false
---

## Capability

Takes the raw ticket set and groups issues into status categories. The grouping mode determines the primary axis: by workflow status, by assignee workload, or by label/area.

## When to Use

- As a parallel analysis step after ticket fetching
- When you need a structured breakdown of sprint progress

## What It Does

1. **By Status** (default) — groups tickets as: Done, In Progress, Blocked, Cancelled, Carried Over. Includes count and point totals per group.
2. **By Assignee** — groups tickets under each team member, showing their status breakdown and point load
3. **By Label** — groups tickets by area label (frontend, backend, infrastructure, etc.) with status counts per area

## Outputs

Structured category map: groups with ticket lists, counts, and point totals.
