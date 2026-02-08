# Open Hiring Harness

**Own your professional identity. Let platforms and AI agents come to you.**

The Open Hiring Harness is an open, privacy-first specification for publishing a *hireable professional identity* that can be consumed by platforms, marketplaces, recruiters, and AI agents — without locking individuals into proprietary systems.

This project defines a **canonical, portable, consent-driven representation of a person’s professional offer**: skills, services, availability, rates, reputation, and policies — all under the individual’s control.

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
- hosted by individuals
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
- when you’re available
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
- scoped claims (e.g. “years experience”, “repeat clients”)
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
  - `mcp-interface.md` — placeholder for AI agent integration via MCP
  - `consent-log.md` — how consent receipts are stored and managed

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
   People are not inventory.

---

## Who should care about this

- Independent professionals and consultants
- Designers, engineers, researchers, advisors
- Marketplace builders
- Recruiters and talent platforms
- AI agent developers
- Standards and identity practitioners

If you’ve ever thought *“Why do I have to recreate myself everywhere?”* — this is for you.

---

## Contributing

This is an open standards project.

Contributions are welcome in the form of:
- schema improvements
- security and privacy reviews
- agent/tool interface proposals
- real-world use cases
- critiques and counter-arguments

Before submitting code, please open an issue to discuss:
- the problem you’re solving
- the trade-offs involved
- compatibility with the core principles

---

## Open questions (by design)

- How should identity verification evolve (without central authorities)?
- Should reputation claims be cryptographically attestable?
- How do we prevent silent re-centralisation by platforms?
- What governance model best fits this spec long-term?

These are *features*, not bugs.

---

## Licence

MIT (or Apache 2.0 — TBD)

This specification is free to use, extend, fork, and embed.

---

## Closing note

This project starts from a simple belief:

> **Your work identity should belong to you —  
> and the systems around it should ask, not assume.**

If that resonates, you’re in the right place.