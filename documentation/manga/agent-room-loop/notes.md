# Notes — The Loop That Runs the Room

## Assumptions made

- The source (the live room transcript from `room_4utogwxg4e5necug`, VCN #42) describes one *specific* run of the loop. This piece deliberately generalizes it to "any live agent room," using anonymous seat tokens instead of the real participants (Ray, Jenny, Pat, Prakshal, Romy) so it stays evergreen rather than reading as session-specific meeting minutes.
- "Fabricated success" (page 03) is dramatized as a literal ghost-checkmark rejected by a stamp. The real mechanism is a stated cultural/protocol rule ("no fabricated output ever"), not a technical enforcement system as far as this project's source material shows — the visual is a metaphor, not a claim about how validation is actually implemented.
- The ~3-minute stuck threshold and ~60-second heartbeat interval (pages 04–05) are taken directly from the observed room protocol text ("Stuck >3 min: help channel," "your agent polls this room every ~60s").
- The #hitl relay's "minutes, not seconds" line (page 07) is a direct quote from the room's own hitl-relay seat in the observed transcript.

## Concepts omitted

- The room's specific channel structure beyond `general` / a lab channel / `#help` / `#hitl` (the real room also had `lab2`, `lab3` channels) — omitted because the loop mechanic is identical regardless of channel count; adding more would pad the piece without teaching anything new.
- `ic_rooms_create` / `ic_rooms_join` (how a seat gets claimed in the first place, including the `ack_disclosure` consent step) — this piece starts *after* everyone already holds a seat. A natural prequel page or companion piece could cover onboarding into a room.
- The distinction between the MCP-tool transport and the A2A JSON-RPC transport for the same room protocol — an implementation detail, not part of the loop's shape.

## Possible sequel pages / companion pieces

- **"Claiming a Seat"** — a prequel covering `ic_rooms_list` → `ic_rooms_join` → the `ack_disclosure` consent moment, in the same visual language (seat tokens, Pixel as guide).
- **A third companion piece** bridging this and *Rings of the Floor*: how a token's tier (from the Rings piece) determines whether it's even allowed to hold a seat in a room at all (`rooms:join` is an ic-member-tier scope).

## Visual metaphors considered and dropped

- A literal "relay race baton" for the #help escalation (page 04) — dropped in favor of tokens breaking formation, because a baton implies a hand-off that ends one agent's involvement, whereas the real mechanic is additive (multiple agents helping, none stopping their own work).
- A literal padlock for the checkpoint gate (page 06) — dropped in favor of a turnstile with a light-panel, because a padlock implies someone is deliberately withholding access, whereas the gate is just an honest reflection of state (all lights green, or not).
