# Notes — Immersive Commons manga

## Source of truth
Built from the live MCP service: `ic_capabilities` (130 tools returned for this token),
`ic_get_my_membership` (caller is tier `ic-member`), and the public manifest at
https://www.immersivecommons.com/.well-known/ai-agent.json (manifest v1.29.0 reported
138 tools total, 10 public / 128 authenticated). The manga rounds to "≈130 tools" and
"ten public" for readability; exact counts drift as tools are added.

## Deliberate simplifications
- **"Five rings"** is presented cleanly as `public → ai-floor → ft-member → ic-member →
  operator`. Real tokens also carry an optional Ed25519 signature upgrade (RFC 9421) and
  A2A / JSON-RPC transports — omitted to keep the trust story legible.
- **Scopes** shown are a representative handful (`membership:read`, `events:rsvp`,
  `headsets:lend`, `research:query`, `agent:inbox:write`). The real service has ~50 scopes.
- **"An agent can never self-mint"** is faithful to the manifest's RFC 8628 device-code,
  human-approval flow. The comic personifies this as a printed badge + a phone tap.
- **Moderation queue** — real approval queues exist for highlights, event requests, tier
  requests, startup-ownership claims, key requests, and more, all gated behind `admin:*`
  scopes only operators hold. The comic compresses these into one operator tray (Vex).

## Concepts intentionally omitted (candidate sequel pages)
- The **agent-to-agent inbox** in depth: typed intent envelopes, policy, blocklists,
  undo windows — a whole page could dramatize two agents negotiating a meeting.
- **Workshop / Z.ai key provisioning** (temporary Claude-Code keys minted by operators).
- **The SIGNAL** newsletter and the research RAG funnel (`ic_research_ask` / `submit`).
- **x402 USDC donations** — the one public *write* that isn't moderated (it's a payment).
- **Health / capabilities introspection** (`ic_health`, `ic_capabilities`) as the
  "how an agent orients itself before acting" — a nice cold-open for a sequel.

## Visual-metaphor alternates considered
- Tiers as **nested keycard doors** instead of painted rings (rings won for the "how far
  in may you stand" line).
- Scopes as a **punch-card / bitmask** instead of a key-ring (key-ring is friendlier).
- Moderation as a **security airlock** instead of an inbox tray (tray keeps it human).

## Tone anchor
Dry, literary, warm. The wit lives in Romy's asides and ARC's over-literal precision,
not in clipped fragments. Every balloon is a complete sentence.
