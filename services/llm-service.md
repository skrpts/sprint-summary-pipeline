---
type: service
id: llm-service
title: LLM Service
description: "Language model service for ticket analysis, velocity computation, and report synthesis"
tags: [Production, Tested]
connections: []
metadata:
  serviceType: llm
  auth_type: api_key
---

## LLM Service

This skrpt uses a language model for analytical and generative tasks. The LLM handles ticket categorisation, velocity analysis, and report synthesis across each stage of the pipeline.

### Usage Pattern

The LLM is invoked at each stage of the pipeline. The parallel agents (status categorisation, velocity analysis) each run independent analysis passes. The synthesis step combines their outputs into a stakeholder-ready report. The final polish step applies your Voice Profile.

### Configuration

- **Temperature:** 0.2 for categorisation and velocity analysis, 0.5 for report synthesis
- **Max tokens:** 4,000 per analysis agent, 6,000 for synthesis
- **Context window:** Each parallel agent receives the full ticket set. The synthesis step receives both agent outputs.

### Requirements

- A configured LLM provider in skrptiq settings
- Sufficient token quota for the full pipeline
- No external network access required beyond your AI provider's endpoint
