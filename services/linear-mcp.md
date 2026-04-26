---
type: service
id: linear-mcp
title: Linear MCP
description: "Linear MCP server for reading sprint cycles, issues, and project data"
tags: [Production, Project Management]
connections: []
metadata:
  provider: linear
  protocol: mcp
  auth_type: api_key
  env_var: LINEAR_API_KEY
  required_scopes: [read]
---

## Service Description

Provides access to Linear issue tracking data via the Model Context Protocol (MCP). This service is used to fetch sprint cycle data, issue statuses, assignee workloads, and project progress for report generation.

## Configuration

### Authentication

Requires a Linear API key set as the `LINEAR_API_KEY` environment variable. Generate one at `linear.app/YOUR-TEAM/settings/api`.

The API key provides read access to all workspaces and teams the key owner belongs to. No additional scopes are required — Linear API keys are all-or-nothing.

### MCP Server Setup

The Linear MCP server must be configured in your MCP settings:

```json
{
  "mcpServers": {
    "linear": {
      "command": "npx",
      "args": ["-y", "linear-mcp-server"],
      "env": {
        "LINEAR_API_KEY": "{LINEAR_API_KEY}"
      }
    }
  }
}
```

## Capabilities Used

### Reading

- `linear_search_issues` — search issues with filters: team, status, assignee, labels, priority, and free-text query. Supports pagination via `limit`.
- `linear_get_user_issues` — retrieve all issues assigned to a specific user, with optional archive inclusion

### Not Used by This Skrpt

- `linear_create_issue` — this is a read-only report; no issues are created
- `linear_update_issue` — not used
- `linear_add_comment` — not used

## Rate Limiting

Linear's API allows 1,500 requests per hour. The pipeline typically consumes 5–15 requests per sprint summary depending on team size. For large teams (50+ members), the fetch step batches requests by assignee.

## Privacy Considerations

Issue titles, descriptions, and assignee names are sent to your configured LLM provider for analysis and report generation. Ensure your organisation's policies permit sending project management data to third-party AI services.
