# Manifest — Immersive Commons: How an Agent Enters the Floor

- **Title:** Immersive Commons — How an Agent Enters the Floor
- **Source:** Immersive Commons MCP service (Floor 10, Frontier Tower, San Francisco). Manifest: https://www.immersivecommons.com/.well-known/ai-agent.json
- **Topic slug:** `immersive-commons-mcp`
- **Audience:** Technical / builder audience who knows what an API or MCP server is, but has never seen this specific service.
- **Depth:** Practitioner-friendly conceptual walkthrough — the trust model and the shape of the system, not an exhaustive tool reference.

## Output target
- **Format:** Single cohesive script (scenes + narration + dialogue) intended to be pasted into **comicexplain.com**, which generates the art itself.
- Because the target renders its own art, there is **no locked per-panel art-style block**. Scene descriptions carry the visual direction. A house look is suggested once, at the top of `script.md`, as guidance rather than a per-panel lock.

## Voice / tone
Dry, literary, faintly deadpan — warm underneath. The humor lives in the observation and the subordinate clause, never in clipped fragments. Complete, grammatical sentences throughout. Think: a patient systems engineer who finds the bureaucracy quietly beautiful.

## Suggested house look (guidance only)
Clean modern educational manga; black and white with light gray screentone; confident linework; generous negative space; legible diagrams integrated into panels; approachable realistic proportions. A physical San Francisco maker-floor: VR headsets on a shelf, a 3D-print farm humming, standing desks, a big front-of-house kiosk screen.

## Core concepts (dependency order)
1. The premise — a physical AI builder floor that agents can act upon, reached through one MCP door.
2. The trust boundary — agent identity is human-gated; a token is minted only by a human-approved device-code flow. An agent can never self-mint.
3. Tiers (rings) — `public → ai-floor → ft-member → ic-member → operator`; each ring widens what a token may hold.
4. Scopes — a token carries named permissions; every tool demands a specific scope *and* a minimum tier.
5. Breadth of real-world action — events, VR headset lending, file vault, transcription, 3D prints, research corpus, startup profiles, agent-to-agent inbox, rooms, the SIGNAL newsletter.
6. Moderation-first — every member-facing write lands in an operator approval queue; nothing auto-publishes.
7. Public edge & recap — ten tools need no token at all; the rest sit behind the gate.

## Page table
| # | Concept | Narrative purpose | Visual metaphor | Status |
|---|---------|-------------------|-----------------|--------|
| 1 | One door into a real place | Setup / hook | A physical floor behind a single glowing MCP doorway | prompt-ready |
| 2 | Human-gated identity | The core trust rule | A human hand approving a device-code before the badge prints | prompt-ready |
| 3 | Tiers / rings | Permission grows in concentric rings | Concentric rings painted on the floor; the badge lights up more of them | prompt-ready |
| 4 | Scopes | Fine-grained keys, not one master key | A key-ring where each key is etched with one verb | prompt-ready |
| 5 | What the agent can actually do | Show the breadth | A tour of stations: headset shelf, print farm, vault, inbox | prompt-ready |
| 6 | Moderation queue | Writes are proposals, not commands | Every action drops into an operator's inbox tray before it's real | prompt-ready |
| 7 | Public edge + recap | Land the model | The lobby: ten open kiosks anyone may touch; the gate behind them | prompt-ready |

## Status
All pages `prompt-ready`. Combined single-paste script written to `script.md`.
