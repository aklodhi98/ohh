# Consent Log

> **Status:** Draft / Placeholder

This document describes how consent receipts are stored and managed separately from the main harness file.

---

## Rationale

The harness file (`hiring-harness.json`) represents your professional identity — relatively static data about who you are, what you offer, and your policies.

Consent receipts are transactional — they accumulate over time as you grant access to platforms, agents, and individuals. Mixing these concerns in a single file creates problems:

- The file grows unboundedly
- Static identity data and dynamic access logs have different update frequencies
- Privacy expectations differ (you may want your harness public but your consent log private)

---

## Proposed structure

Consent receipts are stored in a separate file:

```
/.well-known/hiring-harness.json         # Your identity and policies
/.well-known/hiring-consent-log.json     # Granted receipts (private by default)
```

The harness may reference the consent log location:

```json
{
  "consent": {
    "log_location": "/.well-known/hiring-consent-log.json",
    ...
  }
}
```

---

## Consent log schema

> TODO: Define formal schema

```json
{
  "version": "0.2.0",
  "receipts": [
    {
      "receipt_id": "cr_8f4c2b19",
      "granted_to": { ... },
      "purpose": "...",
      "scopes": ["read:rates"],
      "issued_at": "2026-01-29T10:05:00Z",
      "expires_at": "2026-01-30T10:05:00Z",
      "revoked": false
    }
  ]
}
```

---

## Open questions

- Should the consent log be cryptographically signed?
- How are revocations recorded and propagated?
- Should there be a maximum retention period for expired receipts?
