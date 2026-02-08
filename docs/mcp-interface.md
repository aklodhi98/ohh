# MCP Interface

> **Status:** Draft / Placeholder

This document describes how AI agents can interact with a hiring harness via the [Model Context Protocol (MCP)](https://modelcontextprotocol.io).

---

## Overview

The Open Hiring Harness is designed to be AI-native. Agents should be able to:

1. **Read** structured resources (profile, availability, services)
2. **Request** permissioned access (rates, detailed availability, reputation)
3. **Invoke** actions (request a quote, hold time, submit an endorsement)

All interactions respect the policies declared in the harness.

---

## Resources (read-only)

Agents can read public data as MCP resources:

| Resource URI | Description |
|--------------|-------------|
| `harness://identity` | Public identity (handle, display name, tagline, links) |
| `harness://offer/roles` | Roles and specialties |
| `harness://offer/services` | Service catalogue |
| `harness://availability/summary` | Availability status (open/limited/closed) |
| `harness://proof` | Case studies and credentials |

---

## Tools (actions)

Agents can invoke tools to perform actions:

| Tool | Description | Requires consent |
|------|-------------|------------------|
| `request_access` | Request permissioned data (rates, detailed availability) | — |
| `request_quote` | Request a quote for a specific service | Yes |
| `hold_time` | Request a tentative booking hold | Yes |
| `submit_endorsement` | Submit an endorsement for review | Yes |

---

## Consent flow

When an agent requests permissioned data or invokes a protected tool:

1. Agent calls `request_access` with identity, purpose, and requested scopes
2. Harness owner receives the request (via configured notification channel)
3. Owner grants or denies; if granted, a consent receipt is issued
4. Agent can now access the scoped data until the receipt expires or is revoked

---

## Example: Agent requesting rates

```
Agent: request_access({
  identity: { id: "agent_xyz", name: "TalentBot", type: "agent" },
  purpose: "Evaluate fit for a UX audit project for ClientCo",
  scopes: ["read:rates", "read:availability_detail"]
})

→ Pending approval from harness owner

Owner: Grants access (timeboxed, 24 hours)

→ Consent receipt issued: cr_abc123

Agent: read("harness://offer/rates", { receipt: "cr_abc123" })

→ { currency: "AUD", units: [...], rate_rules: [...] }
```

---

## Open questions

- How does the agent authenticate the consent receipt?
- Should there be a capability URL pattern instead of explicit receipts?
- How do we handle agent-to-agent delegation?
