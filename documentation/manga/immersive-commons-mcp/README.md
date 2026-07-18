# Immersive Commons — How an Agent Enters the Floor

An educational manga that explains the **Immersive Commons** MCP service (Floor 10,
Frontier Tower, San Francisco) to a technical / builder audience.

**Source:** Immersive Commons agent manifest — https://www.immersivecommons.com/.well-known/ai-agent.json

## What it teaches
How an AI agent (like Claude) plugs into a *physical* members-run AI builder space
through a single MCP door — and why that door is deliberately hard to walk through.
The through-line is the trust model:

- **One MCP door, ~130 tools** behind it onto a real floor.
- **Human-gated identity** — an agent can never self-mint a token; a human approves a
  device-code flow and hands over an `agt_…` badge.
- **Five tiers (rings):** `public → ai-floor → ft-member → ic-member → operator`.
- **Scopes** — single-verb permissions (`events:rsvp`, `headsets:lend`, …); every tool
  needs a specific scope *and* a minimum tier. Scopes never graft onto an old token.
- **Breadth of action** — events, VR headset lending, file vault, transcription, 3D
  prints, research corpus, startup pages, agent-to-agent inbox, shared rooms, THE SIGNAL.
- **Moderation-first** — every member write becomes a proposal in an operator's queue;
  nothing auto-publishes.
- **Public edge** — ten tools need no token at all.

## Cast
- **Romy** — human member, our point-of-view; taps to approve.
- **ARC** — Romy's AI agent; reach is wide but fenced by its scopes.
- **Vex** — a floor operator; the approval queue with a face.

## Pages
7 pages. See `manifest.md` for the concept-per-page table.

## How to use
This project is built for **comicexplain.com**, which generates the art from a script:
1. Open **`script.md`** and paste the whole thing into comicexplain.com. That is the
   primary deliverable — one continuous 7-page script.
2. Prefer to work page-by-page (or use another image tool)? Each `page-01.md … page-07.md`
   is a self-contained scene, and `index.html` gives one-click copy buttons for all of them.
3. Save any rendered images to `panels/immersive-commons-mcp_pageNN.png`, re-run the site
   generator to preview them, then optionally run `manga-pdf-generator` to bundle a PDF.
