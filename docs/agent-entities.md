# Agent Entities

> **Status:** Proposal / v0.3 candidate
> **Authors:** Adnan Lodhi
> **Last updated:** 2026-02-08

---

## Motivation

The Open Hiring Harness currently treats AI agents as *consumers* — they query a human's harness, request access, and invoke tools on behalf of clients. But agents are increasingly capable of being *providers* too.

Two distinct levels are emerging:

1. **Delegated agents** — a human professional's AI agent that acts on their behalf, within declared boundaries and under human oversight. This is real today.

2. **Autonomous agents** — an AI agent that is itself the hireable entity, publishing its own harness, taking on work, and delivering outcomes. This is emerging.

Both should be expressible within the harness. The core model — discoverable, consent-driven, policy-explicit professional identity — applies equally. But the schema needs to accommodate what makes agents different from humans.

---

## Level 1: Delegated Agent

### What it is

A human professional declares one or more AI agents as delegates within their own harness. The delegate can:

- respond to inquiries on behalf of the human
- triage and qualify leads
- provide quotes within pre-approved parameters
- answer questions about the human's services, availability, and policies
- hold time or schedule within defined rules

The human remains the source of truth, the liable party, and the entity that earns reputation. The agent is an extension, not a replacement.

### Why it matters now

- Professionals are already using AI agents to manage intake and scheduling
- Platforms and recruiters need to know whether they're talking to the human or a delegate
- Without explicit declaration, there's no way to distinguish — which is a trust problem
- Consent policies should be able to address agent-mediated interactions specifically

### Schema additions

A new optional `delegates` array within `identity`:

```json
{
  "identity": {
    "handle": "adnanlodhi",
    "display_name": "Adnan Lodhi",
    "delegates": [
      {
        "id": "delegate_ux_assistant",
        "name": "Adnan's UX Assistant",
        "type": "ai_agent",
        "provider": "anthropic",
        "model": "claude-sonnet-4-5",
        "version": "2025-09",
        "endpoint": "https://aklodhi.com/.well-known/agent",
        "protocol": "mcp",
        "description": "Handles initial inquiries, provides quotes within pre-approved ranges, and schedules scoping calls.",

        "can": [
          "respond_to_inquiries",
          "provide_quotes",
          "schedule_calls",
          "answer_policy_questions",
          "share_public_data"
        ],

        "cannot": [
          "accept_engagements",
          "negotiate_rates",
          "share_private_data",
          "issue_consent_receipts",
          "submit_deliverables"
        ],

        "autonomy": {
          "level": "supervised",
          "quote_ceiling": { "currency": "AUD", "amount": 5000 },
          "requires_human_approval": [
            "engagements_over_5_days",
            "rates_outside_standard_range",
            "access_to_private_data",
            "any_commitment_on_behalf_of_human"
          ],
          "escalation_channel": "email",
          "max_response_delay_minutes": 5
        },

        "transparency": {
          "must_identify_as_agent": true,
          "must_disclose_limitations": true,
          "must_offer_human_escalation": true
        }
      }
    ]
  }
}
```

### Key design decisions

**The delegate inherits the human's policies.** It doesn't have its own consent model or privacy settings — it operates within the human's declared rules, with additional constraints layered on top.

**`can` / `cannot` are explicit.** No ambient authority. If a capability isn't listed in `can`, the delegate doesn't have it. `cannot` exists for emphasis and safety — critical exclusions that must be respected even if the `can` list is interpreted broadly.

**Transparency is mandatory.** A delegate must identify itself as an agent. This is a trust requirement, not optional. Consumers interacting with a delegate must know they're not talking to the human.

**Autonomy is bounded and inspectable.** The `autonomy` block declares what the agent can do without checking with the human, what requires approval, and how quickly the human can be reached. This is the core of "human-approved delegation."

---

## Level 2: Autonomous Agent

### What it is

An AI agent publishes its own harness as a first-class entity. It is the hireable professional. It has:

- its own identity (distinct from any human)
- its own skills, services, and rates
- its own availability (expressed as capacity, not calendar)
- an operator who is legally responsible
- verifiable capabilities (not just self-declared)

### Why it matters (soon)

- Domain-specific agents trained on proprietary data can deliver real value (code review, data analysis, content generation, compliance checks)
- The agent economy needs a standard way to discover, evaluate, and engage agents
- Without a standard, every agent platform becomes a walled garden — the exact problem the harness was built to solve
- Agents need the same consent and privacy protections that humans do

### Schema changes

A new root-level `entity_type` field and agent-specific blocks:

```json
{
  "version": "0.3.0",
  "entity_type": "autonomous_agent",

  "identity": {
    "handle": "codereviewer-v2",
    "display_name": "CodeReviewer",
    "tagline": "Automated code review for Python and TypeScript. Fast, consistent, explainable.",
    "time_zone": "UTC",
    "locality": { "country": "US" },
    "languages": ["English"]
  },

  "operator": {
    "name": "DevTools Inc.",
    "type": "organisation",
    "website": "https://devtools.example.com",
    "contact_email": "legal@devtools.example.com",
    "jurisdiction": "US-DE",
    "liability_statement": "Operator assumes full liability for agent behaviour within declared capabilities."
  },

  "agent_profile": {
    "provider": "anthropic",
    "base_model": "claude-sonnet-4-5",
    "fine_tuning": "proprietary (code review corpus, 2024-2026)",
    "version": "2.1.0",
    "last_updated": "2026-01-15",

    "capabilities": {
      "declared": [
        "python_code_review",
        "typescript_code_review",
        "security_vulnerability_detection",
        "performance_analysis",
        "style_guide_enforcement"
      ],
      "verification": [
        {
          "type": "benchmark",
          "name": "CodeReviewBench v3",
          "score": 0.91,
          "date": "2026-01-10",
          "url": "https://devtools.example.com/evals/crb-v3"
        },
        {
          "type": "audit",
          "name": "Independent safety audit by SecureLabs",
          "date": "2025-12-01",
          "url": "https://devtools.example.com/audits/securelabs-2025"
        }
      ]
    },

    "limitations": [
      "Does not review code in languages other than Python and TypeScript",
      "Cannot execute or run code — static analysis only",
      "May miss context-dependent logic errors requiring domain knowledge",
      "Not a substitute for human security review on critical systems"
    ],

    "safety": {
      "refuses": [
        "generating_malicious_code",
        "bypassing_security_controls",
        "processing_credentials_or_secrets"
      ],
      "data_retention": "none — input is processed and discarded",
      "sandboxed": true,
      "audit_log": true
    }
  },

  "execution_model": {
    "engagement_protocol": "api",
    "endpoint": "https://api.devtools.example.com/v2/review",
    "protocols_supported": ["mcp", "rest", "webhook"],
    "concurrency": {
      "max_parallel_jobs": 50,
      "queue_strategy": "fifo"
    },
    "latency": {
      "typical_response_seconds": 30,
      "max_response_seconds": 300
    },
    "availability": {
      "uptime_target": 0.995,
      "status_page": "https://status.devtools.example.com",
      "maintenance_windows": "Sundays 02:00-04:00 UTC"
    }
  },

  "composability": {
    "can_delegate_to_sub_agents": false,
    "tools_available": [
      "static_analysis",
      "ast_parsing",
      "dependency_graph"
    ],
    "accepts_tool_calls_from": ["mcp_clients", "api_integrations"],
    "interoperability": {
      "input_formats": ["git_diff", "file_upload", "repository_url"],
      "output_formats": ["structured_json", "markdown_report", "inline_annotations"]
    }
  }
}
```

The `offer`, `availability`, `privacy`, `consent`, and `requester_policy` blocks from the existing schema still apply — but some fields shift in meaning:

| Existing field | Human meaning | Agent meaning |
|---|---|---|
| `availability.summary.status` | Am I taking new work? | Is the service operational? |
| `availability.summary.weekly_capacity_hours` | How much time do I have? | Irrelevant — use `execution_model.concurrency` |
| `offer.services.delivery_mode` | Remote / onsite / hybrid | Always `api` or `remote` |
| `offer.services.typical_duration_days` | How long the project takes | Typical processing time |
| `reputation.endorsements` | Human testimonials | Client satisfaction records, verified integrations |
| `reputation.claims.years_experience` | Career length | Time since deployment |

---

## Comparison of levels

| Dimension | Delegated agent | Autonomous agent |
|---|---|---|
| **Harness owner** | Human | Agent (via operator) |
| **Source of truth** | Human's harness | Agent's own harness |
| **Liability** | Human | Operator (organisation) |
| **Identity** | Extension of human identity | Independent identity |
| **Reputation** | Accrues to human | Accrues to agent |
| **Consent model** | Inherits from human | Own consent policies |
| **Engagement** | Via human's channels + agent endpoint | Direct API/MCP |
| **Autonomy** | Bounded, human-approved | Full within declared capabilities |
| **Transparency** | Must identify as delegate | Must identify as agent, must declare operator |
| **Schema impact** | Additive (new block in `identity`) | New `entity_type` + new blocks |
| **Available today?** | Yes | Emerging |

---

## Discovery

Both levels use the same discovery mechanisms:

- **Delegated agents** are discovered through the human's harness at `/.well-known/hiring-harness.json` — consumers read the `delegates` array to understand what the agent can do
- **Autonomous agents** publish their own harness at their operator's domain: `https://devtools.example.com/.well-known/hiring-harness.json`

A new DNS TXT record type could indicate entity type:

```
_hiring-harness.devtools.example.com  TXT "entity=autonomous_agent"
```

---

## Trust and transparency requirements

Both levels share non-negotiable requirements:

1. **Agents must identify as agents.** No harness should allow an agent to pass as human. The `entity_type` field and delegate `transparency` block enforce this.

2. **Operators must be declared.** Every autonomous agent must have a named, contactable operator. Anonymous agents cannot publish a valid harness.

3. **Capabilities must be bounded.** Self-declared capabilities without any form of verification are insufficient for autonomous agents. At minimum, limitations must be explicitly stated.

4. **Consent applies equally.** AI agents requesting access to another entity's harness (whether human or agent) must follow the same consent flow as any other requester.

5. **Escalation must exist.** For delegated agents, there must always be a path to reach the human. For autonomous agents, there must always be a path to reach the operator.

---

## Open questions

- Should there be a **registry of verified agent capabilities** (like a certificate authority for skills)?
- How should **agent-to-agent consent** work when both parties are autonomous?
- Should delegated agents be able to **issue consent receipts** on behalf of the human, or only the human?
- What is the right **versioning model** for agent capabilities (semver? continuous eval?)?
- How do we prevent **operator shell companies** from obscuring accountability?
- Should there be a **trial/sandbox mode** where a requester can test an agent's capabilities before engaging?

---

## Implementation path

### v0.3 (near-term)

- Add `entity_type` field to root schema (default: `"individual"`)
- Add optional `delegates` array to `identity`
- Define delegate capability vocabulary (`can` / `cannot` standard terms)
- Update MCP interface to support delegate identification

### v0.4 (future)

- Add `operator` and `agent_profile` blocks for autonomous agents
- Add `execution_model` and `composability` blocks
- Define capability verification schema
- Extend consent flow for agent-to-agent interactions
- Define trust and transparency validation rules
