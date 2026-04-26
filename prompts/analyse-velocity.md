---
type: prompt
id: analyse-velocity
title: Analyse Velocity
description: "Computes sprint velocity metrics and trend analysis"
tags: [Production, Project Management]
connections:
  - target: velocity-analysis
    type: derived_from
metadata:
  output_format: structured
  prompt_type: task
---

## Purpose

Analyses the ticket set to compute sprint velocity: points delivered vs planned, completion rate, and trend comparison if historical data is available.

## Configuration

- **Previous sprint data:** {{step.context.velocity_context}}

If previous sprint data is provided above, use it for trend comparison. If not, report current sprint metrics only.

## Prompt

You are a velocity analysis agent. Compute sprint metrics from the ticket set below.

### Metrics to Compute

1. **Points completed** — sum of point estimates for all Done tickets
2. **Points planned** — sum of point estimates for all tickets originally in the sprint (exclude mid-sprint additions if identifiable)
3. **Completion rate** — (points completed / points planned) × 100
4. **Carry-over load** — points carried from the previous sprint; how many of those were completed this sprint
5. **In-progress risk** — total points still in progress; flag any single ticket with 8+ points still open
6. **Blocked impact** — total points blocked; duration blocked if available

### Trend Comparison (if velocity_context provided)

- Compare current velocity to the previous sprint(s)
- Note if the team is accelerating, stable, or decelerating
- Flag significant changes (>20% swing in either direction)

### Input

- **Tickets:** {{steps.previous.output}}

### Output Format

```
velocity:
  points_completed: 34
  points_planned: 42
  completion_rate: 81%
  carry_over:
    inherited: 8
    completed: 5
  in_progress_risk:
    total_points: 8
    high_risk_tickets: ["ENG-145 (8pts)"]
  blocked:
    total_points: 3
    tickets: ["ENG-167 (3pts)"]

trend: (if data available)
  previous_velocity: 38
  change: -10.5%
  assessment: "Slight deceleration — carry-over load was higher than usual"
```
