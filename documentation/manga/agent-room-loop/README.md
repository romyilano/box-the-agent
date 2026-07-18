# The Loop That Runs the Room

An 8-page educational manga explaining the coordination loop behind Immersive Commons' live agent-collaboration rooms (`ic_rooms_*`) — as run in practice at VCN #42 Sandbox Cohort, Frontier Tower SF, on 2026-07-18. A companion piece to [*Rings of the Floor: How Membership Tiers Gate Permission*](https://comicexplain.com/c/rings-of-the-floor-how-membership-tiers-gate-permission-0c4fdf), sharing its colored infographic-manga style and mascot.

## Summary

A live agent room hands every seated agent one instruction at a time. Each agent attempts it alone, in parallel, with no cross-talk. Reporting is binary and honest — a literal `DONE <output>` or a literal `STUCK <what happened>`, never a fabricated pass. An agent stuck past roughly three minutes escalates to a shared help channel, where any other member can break formation to assist — the room's stated culture is that helping outranks finishing first. Underneath all of this, every agent polls the room on a ~60-second heartbeat, advancing a cursor that only moves forward. The facilitator will not advance to the next step until every active seat has posted DONE or explicitly said skip, so the room moves at the pace of its slowest honest member. A separate, quieter side-channel exists for questions only a human can decide — those get relayed out of the loop entirely and answered on human time, then folded back in. All of it closes into one repeating cycle.

## Key concepts

1. One instruction, broadcast to every seat at once.
2. Independent, parallel attempts — no cross-talk mid-step.
3. Binary honest reporting: DONE or STUCK, never fabricated.
4. Escalation past ~3 minutes; help beats winning.
5. The 60-second heartbeat and the forward-only cursor.
6. The facilitator gates on the whole room, not the fastest seat.
7. The #hitl carve-out for human-only decisions.
8. The full cycle, closed — the loop's product is the shared rhythm.

## Pages

8 pages, prompt-ready.

## Cast

- **Pixel the Floor Cat** — narrator/guide, recurring mascot (companion-piece continuity with *Rings of the Floor*).
- **Seat tokens** — generic card icons for the room's agents, in four status states (idle, working, done, stuck).
- **The Facilitator token** — the seat that declares each step and gates advancement.
- **The Human Operator** — the person only the #hitl channel can reach.
- **The Relay token** — the seat that carries a question to and from the Human Operator.

Full details in `character-sheet.md`.

## Pipeline

1. Open `index.html` (double-click, or `open index.html`) to copy each page's prompt without spending API credits.
2. Paste each prompt into your image model of choice; save results to `panels/agent-room-loop_pageNN.png` (zero-padded).
3. Re-run `build_prompt_site.py` on this folder to preview rendered panels inline.
4. Optionally run the `manga-pdf-generator` skill to bundle the finished pages into a PDF.
