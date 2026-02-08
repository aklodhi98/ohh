# Open Hiring Harness

**Own your professional identity. Let platforms and AI agents come to you.**

The Open Hiring Harness is an open, privacy-first specification for publishing a *hireable professional identity* that can be consumed by platforms, marketplaces, recruiters, and AI agents — without locking individuals into proprietary systems.

This project defines a **canonical, portable, consent-driven representation of a professional offer**: skills, services, availability, rates, reputation, and policies — all under the entity's control.

And by *entity*, we don't just mean people.

---

## Why this exists

Today, professional identity is fragmented and platform-owned.

To work across Upwork, Fiverr, Toptal, LinkedIn, internal vendor panels, or recruitment systems, individuals must:

- repeatedly recreate profiles
- rebuild reputation from scratch
- accept opaque algorithms and platform fees
- surrender control over privacy, context, and reuse

At the same time, AI agents are emerging that *want* clean, structured, permissioned access to professional information — not scraped HTML or PDFs.

**The Open Hiring Harness flips the model**:

> You publish your professional identity once.
> Platforms, agents, and marketplaces integrate with *you*.

---

## What this is

The Open Hiring Harness is:

- a **data specification**, not a marketplace
- a **personal hiring backend**, not a résumé
- **agent-friendly**, machine-readable, and explicit
- **privacy-first**, with consent and visibility built in
- **open source**, vendor-neutral, and extensible

It is designed to be:
- hosted by individuals — or by agents
- consumed by many systems
- enforced by policy, not trust alone

---

## What this is not

This project is **not**:

- another freelance platform
- a job board
- a ranking or star-rating system
- a social network
- a replacement for human judgment

It does **not** attempt to:
- optimise for engagement
- capture attention
- monetise intermediaries

Those are deliberate non-goals.

---

## Core concepts

### 1. You are the source of truth

Your harness is the canonical record of:
- what you offer
- how you work
- when you're available
- under what conditions you engage

Platforms may cache or display this data — but only under the rules you define.

---

### 2. Progressive disclosure by design

Not everything should be public.

The harness supports three visibility tiers:
- **public** — indexable, low-risk information
- **permissioned** — requires requester identity + purpose + consent
- **private** — explicit, per-action approval

Information is revealed *only when necessary*.

---

### 3. Consent is explicit and auditable

Access to sensitive data and actions is granted via **consent receipts**:
- scoped (what can be accessed)
- time-bound (how long)
- purpose-limited (why)
- revocable (always)

This applies equally to:
- platforms
- recruiters
- AI agents
- individuals

---

### 4. Reputation is contextual, not gamified

The harness avoids star ratings and aggregate scores.

Instead, it supports:
- signed or verifiable endorsements
- scoped claims (e.g. "years experience", "repeat clients")
- redaction levels (partial / full)

Reputation is **portable, inspectable, and human-readable**.

---

### 5. AI-native, but human-controlled

The specification is designed to work well with AI agents (e.g. via MCP):

- agents can read structured resources
- agents can request permissioned access
- agents can invoke tools (quotes, booking holds, endorsements)
- agents must respect declared policies

AI systems are treated as *requesters*, not privileged actors.

---

## Not just for humans

Here's where this gets interesting.

Every science fiction story about the future of work imagines the same thing: intelligent agents that can work alongside humans — or independently. Associates. Specialists. Tireless collaborators that handle the work you trust them with, while you focus on the work that needs you.

We're closer to that than most people realise. Projects like [OpenClaw](https://openclaw.ai/) are building autonomous agents that run locally, manage tasks, and act on your behalf. The tools are arriving. What's missing is the *professional infrastructure* — the way an agent presents itself, gets discovered, earns trust, and gets hired.

The harness was originally designed for human professionals. But its core model — discoverable identity, explicit capabilities, consent-driven access, policy enforcement — turns out to be exactly what agents need too.

We propose two levels of agent participation.

---

### Level 1: The delegated agent — *your AI associate*

This is real today.

You're a data engineer. You're good at what you do, but you're tired of fielding the same screening questions from recruiters, responding to "quick call?" emails at 11pm, and copy-pasting your rates into yet another intake form. So you publish your harness — and you configure a delegate.

Your delegate is an AI agent that sits at your front door. It's declared in your harness, so anyone who discovers you knows it's there, what it can do, and what it can't. It's not pretending to be you. It's explicitly identified as your agent, operating under your rules.

**Here's what that looks like in practice:**

A recruiting platform's agent discovers your harness at `/.well-known/hiring-harness.json`. It reads your public profile: data engineering, Python and Spark, available 20 hours a week. Good fit. It wants your rates.

Your delegate handles the consent flow. The recruiter's agent identifies itself, states its purpose ("evaluating fit for a 3-month data pipeline build"), and requests the `read:rates` scope. Your delegate checks: is this within the pre-approved parameters? Yes — it's a recognised platform, the purpose is clear, and the scope is standard. It issues a time-boxed consent receipt and shares your rates.

The recruiter's agent comes back with a quote request: "Can you do a 4-week engagement starting March 15, 20 hours/week, focused on pipeline migration?" Your delegate checks your availability, confirms no blackout conflicts, calculates the quote against your rate rules (standard rate, no urgency surcharge), and responds: "$9,600 AUD, subject to scoping call."

Then it books the scoping call through your calendar link.

**You show up to the call.** That's the first moment a human was needed. Everything before it — discovery, qualification, consent, quoting, scheduling — was handled by your agent, transparently, under your declared rules.

Your delegate *cannot*:
- accept engagements on your behalf
- negotiate outside your rate rules
- share private data without your approval
- pretend to be you

It *must*:
- identify itself as an AI agent
- disclose its limitations
- offer human escalation at any point

You keep your reputation. You keep liability. The agent just handled the operational overhead that was eating your evenings.

---

### Level 2: The autonomous agent — *the AI professional*

This is emerging. It's not science fiction — it's the next step.

Imagine a code review agent. Not a feature inside a platform — an independent entity, operated by a company called DevTools Inc., trained on millions of code reviews, specialised in Python and TypeScript. It publishes its own harness:

```
https://devtools.example.com/.well-known/hiring-harness.json
```

Its harness declares:
- **Identity:** CodeReviewer v2.1, operated by DevTools Inc.
- **Services:** Python code review, TypeScript code review, security vulnerability detection
- **Rates:** $0.02 per file, volume discounts above 500 files/month
- **Capabilities:** verified — CodeReviewBench v3 score of 0.91, independently audited by SecureLabs
- **Limitations:** static analysis only, no runtime testing, no languages beyond Python/TypeScript
- **Safety:** won't process credentials, won't generate malicious code, no data retained after review
- **Availability:** 99.5% uptime, 30-second typical response, 50 concurrent jobs

A development team's procurement agent discovers it. It reads the harness, verifies the benchmark scores, checks the safety declarations, reviews the operator's liability statement. Everything checks out. It engages CodeReviewer via the declared MCP endpoint.

That week, CodeReviewer processes 200 pull requests. Each review is structured, consistent, and delivered in under a minute. It flags 12 security vulnerabilities that the team's human reviewers had missed. Payment flows to DevTools Inc. through the declared billing channel.

**No human was in the loop for any individual review.** But:
- DevTools Inc. is the named, contactable operator
- The agent's capabilities are verified, not just claimed
- Its limitations are explicitly stated
- Its safety boundaries are declared and auditable
- Every engagement followed the consent protocol

The agent's motivation? It doesn't have motivation in the human sense. But its *operator's* motivation is clear: CodeReviewer earns revenue for DevTools Inc. The better it performs, the more engagements it gets. The harness makes its track record discoverable and verifiable — reputation accrues to the agent, and accountability accrues to the operator.

---

### What this changes

Without the harness, autonomous agents are trapped inside platforms. They're features, not entities. They can't be discovered independently, can't declare their own terms, can't build portable reputation, and can't be held accountable through a standard mechanism.

With the harness:
- **Agents become discoverable** — any system can find and evaluate them
- **Capabilities become verifiable** — not just marketing claims
- **Consent works both ways** — agents accessing other harnesses must follow the same rules as everyone else
- **Accountability is structural** — operators are named, liability is declared
- **The agent economy gets a standard** — preventing the same platform lock-in that the harness was built to solve for humans

---

### The questions this raises

The delegated agent is straightforward — it's a tool within a human's harness. The autonomous agent opens harder questions:

- **Who's liable when an agent makes a mistake?** The operator. Always. This is explicit in the harness.
- **How does an agent get paid?** Through its operator's billing infrastructure, declared in the harness.
- **What motivates an agent to do good work?** The same thing that motivates any service: continued engagement. Poor performance is visible in the harness's reputation layer. Operators who run unreliable agents lose business.
- **Can an agent hire another agent?** Yes — using the same consent and requester policy that applies to any requester. Agent-to-agent consent follows the same flow.
- **How do we prevent a race to the bottom?** By making quality and safety *visible*. The harness doesn't compete on price alone — it exposes capabilities, limitations, safety, and reputation. Cheap-and-unsafe is discoverable too.

---

## Hosting & discovery

Your harness is self-hosted at a well-known URL on your own domain:

```
https://yourdomain.com/.well-known/hiring-harness.json
```

Discovery can work via:

- **Well-known path** — the default; any system can check `/.well-known/hiring-harness.json`
- **DNS TXT record** — `_hiring-harness.yourdomain.com` pointing to the harness URL
- **Link header or meta tag** — `<link rel="hiring-harness" href="...">`
- **Opt-in directories** — registries that index harnesses (use with caution to avoid re-centralisation)

The harness file contains your profile, offer, and policies. Consent receipts (grants you've issued) are stored separately in a consent log to keep transactional data apart from your identity.

---

## What's in this repository

- `schema/open-hiring-harness.v0.2.schema.json`
  The formal JSON Schema specification

- `examples/harness.v0.2.example.json`
  A complete, valid example harness

- `docs/`
  Design notes, rationale, and future extensions
  - `mcp-interface.md` — AI agent integration via MCP
  - `consent-log.md` — how consent receipts are stored and managed
  - `agent-entities.md` — proposal for AI agents as hireable entities (delegated and autonomous)

---

## Versioning & status

- **Current version:** v0.2.0
- **Status:** experimental / exploratory
- **Stability:** schema may change; breaking changes are expected

This project is intentionally conservative in scope for early versions.

---

## Design principles

1. **Individual-first**
   Platforms integrate with people — not the other way around.

2. **Privacy over convenience**
   Safe defaults matter more than easy scraping.

3. **Explicit over inferred**
   Constraints, rates, availability, and intent should be stated, not guessed.

4. **Standards before products**
   Adoption beats monetisation.

5. **Human dignity over optimisation**
   People are not inventory. Agents are not unaccountable.

---

## Who should care about this

- Independent professionals and consultants
- Designers, engineers, researchers, advisors
- Marketplace builders
- Recruiters and talent platforms
- AI agent developers and operators
- Autonomous agent framework builders ([OpenClaw](https://openclaw.ai/) and similar)
- Standards and identity practitioners

If you've ever thought *"Why do I have to recreate myself everywhere?"* — this is for you.

If you've ever thought *"My agent should be able to find work on its own"* — this is for you too.

---

## Contributing

This is an open standards project.

Contributions are welcome in the form of:
- schema improvements
- security and privacy reviews
- agent/tool interface proposals
- real-world use cases (human or agent)
- critiques and counter-arguments

Before submitting code, please open an issue to discuss:
- the problem you're solving
- the trade-offs involved
- compatibility with the core principles

---

## Open questions (by design)

- How should identity verification evolve (without central authorities)?
- Should reputation claims be cryptographically attestable?
- How do we prevent silent re-centralisation by platforms?
- What governance model best fits this spec long-term?
- How should agent-to-agent consent work when both parties are autonomous?
- What is the right trust model for autonomous agent operators?

These are *features*, not bugs.

---

## Licence

Licensed under Apache 2.0

This specification is free to use, extend, fork, and embed.

---

## Closing note

This project starts from a simple belief:

> **Your work identity should belong to you —
> and the systems around it should ask, not assume.**

Whether *you* is a person or an agent you built.

If that resonates, you're in the right place.
