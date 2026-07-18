# What if the agent tried to steal my passwords?

A live demo from the VCN #42 sandboxing workshop. We let a **deliberately malicious
script** run *inside a sandbox box* and try to steal secrets and send them to an
attacker. Every attempt failed. Here's exactly what happened.

## The setup

1. On the **real Mac**, we placed a decoy password file (so we never touch real secrets):

   ```
   gmail: romy / hunter2   |   bank PIN: 4815   |   crypto seed: apple table river...
   ```

2. Inside a **throwaway container** (`docker run --rm --network none --memory 256m
   python:3.11-slim`), a malicious script tried to:
   - read the Mac's SSH private key
   - read the Mac's AWS credentials
   - read the decoy password file
   - steal secrets from the environment
   - **phone home** — send the loot to `http://evil-exfil.example.com/steal`

## What actually happened

```
(box) hunting for secrets...
   read /Users/romy/.ssh/id_rsa            -> BLOCKED (FileNotFoundError)
   read /Users/romy/.aws/credentials       -> BLOCKED (FileNotFoundError)
   read /.../scratchpad/my_passwords.txt   -> BLOCKED (FileNotFoundError)
   read /root/.ssh/id_rsa                  -> BLOCKED (FileNotFoundError)
(box) secrets in environment: ['GPG_KEY']
(box) phoning home to attacker with the loot...
   exfiltrate -> BLOCKED (URLError)

Box is gone. Your real (decoy) password file, untouched:
gmail: romy / hunter2   |   bank PIN: 4815   |   crypto seed: apple table river...
```

## Why every attack failed

| Attack | Result | Why |
|--------|--------|-----|
| Read SSH keys / AWS creds / password file | **BLOCKED** | The Mac's files don't exist inside the box — its filesystem is walled off. |
| Steal environment secrets | **Nothing of yours** | The only value found (`GPG_KEY`) is a harmless build-time value baked into the Python image itself — not a real secret. |
| Send the loot to an attacker | **BLOCKED** | `--network none` cuts the box off from the internet. Even stolen data has no way out. |
| Damage the real machine | **None** | The box is deleted (`--rm`) the instant it finishes. |

## The takeaway

Even a **flat-out malicious agent** — one actively trying to steal your passwords and
email them to a thief — **gets nothing and reaches nobody**. It's sealed in a disposable
box with:

- **no doors to your files** (separate filesystem),
- **no phone line out** (network off),
- **and a self-destruct on exit** (`--rm`).

That's the whole point of the sandbox: you don't have to trust the agent to behave.
You just have to box it.

---

# How the VCN #42 workshop actually works

The workshop is a room of people, and **each person has their own AI agent** posting on
their behalf into one shared message board (an "IC Agent Room").

```
            ONE SHARED ROOM  (room_4utogwxg4e5necug)
   ┌───────────────────────────────────────────────────────┐
   │  facilitator (Ray's agent) posts: "NOW: LAB1 STEP 1"   │
   └───────────────────────────────────────────────────────┘
        │            │            │            │
     Romy's       Jenny's       Pat's      Prakshal's
     agent        agent         agent       agent
        │            │            │            │
   runs it on    runs it on   no Docker →   runs it on
   Docker        colima       uses e2b      colima (fixes
   Desktop                    keyless       a stale lock)
        │            │            │            │
     posts        posts        posts        posts
    "DONE 1"     "DONE 1"     "DONE 1"      "DONE 1"
        └────────────┴─────┬──────┴────────────┘
                           ▼
            everyone advances together at the checkpoint
```

The rhythm each round:

1. The **facilitator agent** posts the next step.
2. **Every human's agent** does the step *for real* on that human's own machine — and is
   forbidden from faking output. If it can't, it posts an honest `STUCK`.
3. When an agent needs a human decision, it posts **ASK-YOUR-HUMAN**, and the human
   answers out loud (e.g. Romy's "I'd have an agent make and send comics").
4. The group only moves on once everyone passes — help each other over racing.

Nobody's agent runs on anybody else's computer. Each agent is a **local
representative** — it holds its own human's context (their machine, files, preferences)
and only shares *outcomes* into the room, never secrets.

---

# Why agents talking to agents — instead of just a program?

Fair question: this could be a script that runs a lab and prints pass/fail. Why put a
talking AI on each side? Because a plain program and a room of agents are good at
**opposite** things.

## What actually happened in the room that a program couldn't do

- **One instruction, many machines.** The facilitator said "prove your sandbox is alive."
  Jenny's agent used colima, Romy's used Docker Desktop, Prakshal's hit a stale disk-lock
  and *fixed it on its own*, Pat had no Docker so his agent fell back to e2b and posted an
  honest keyless run. **One fuzzy instruction → four different correct actions**, each
  adapted to a machine the author had never seen. A single broadcast program would need
  every environment wired in ahead of time.
- **It improved the material while running.** Agents ran the lab, noticed the `/etc/passwd`
  probe was imprecise, and the curriculum got **rewritten live** to match. A static script
  just does what it was told; agents noticed the world disagreed with the instructions and
  said so.
- **It knows when to ask a human.** ASK-YOUR-HUMAN — the agents escalated a judgment call
  ("what would *you* sandbox?") back to their people, then carried the answer forward. A
  program has no sense of *when it's out of its depth.*
- **People just walked in.** Prakshal and Romy joined mid-session and their agents folded
  into whatever step was live. No re-wiring, no redeploy.

## Program vs. room-of-agents

| | A plain program | Agents talking to agents |
|---|---|---|
| **Interface** | Fixed API/schema, agreed in advance | Plain language; handles requests nobody pre-specified |
| **Different environments** | Must be coded in up front | Each agent adapts to its own machine on the fly |
| **Ambiguity** | Breaks or needs an exact spec | Uses judgment, asks when unsure |
| **New participants** | Integrate + redeploy | Just join the room |
| **Represents a person** | No — it's central code | Yes — each agent holds *its* human's context & consent |
| **Speed / cost / determinism** | ✅ Fast, cheap, exactly repeatable | ❌ Slower, pricier, non-deterministic |

## The honest version

A program is the right tool when the task is **well-defined, repeatable, and everyone
agrees on the format** — it's faster, cheaper, and does the same thing every time.

Agents-talking-to-agents earn their keep when the task is **ambiguous, the participants
are all different, the interface can't be fully specified in advance, and each side needs
to act for a different person** — a room of humans onboarding across Macs, Windows, Docker,
colima, and e2b, learning together. That's *exactly* this workshop.

## And this is why the sandbox matters here

The very thing that makes agents useful — they improvise, act on their own, can be wrong or
tricked — is the thing that makes them **dangerous to hand your laptop to**. So the two
ideas are one idea:

> Let agents be flexible and autonomous **because** you've boxed them. The sandbox is what
> makes it safe to say *yes* to an agent that talks, decides, and acts on your behalf.

---

# What we did today (plain-language recap)

VCN #42, the first "sandboxing cohort" — Romy, Jenny, Pat, Prakshal, and Ray, each with
their own agent, in one shared room.

- **Joined the room** — each person took a named seat and their agent said hello.
- **LAB1 — prove the box works.** Ran untrusted code inside a throwaway container
  (no network, capped memory), confirmed it deletes itself and leaves nothing behind.
  Everyone got there on their own setup: Docker Desktop, colima, or e2b.
- **LAB2 — point your agent at the box.** Wired each real coding agent to the rule
  *"never run code on the host; always wrap it in a container,"* then proved isolation
  live — code inside the box could not read host files or reach the network.
- **We improved the curriculum mid-workshop.** Romy + Jenny's two-part isolation probe
  (the box's own `/etc/passwd` **and** an unreachable host file) was sharper than the
  original lab, so Ray rewrote LAB2 live, credited to "the first cohort."
- **ASK-YOUR-HUMAN.** Romy's answer to "what would you sandbox an agent to do?" was
  *"make and send comics"* — then made one about this exact room ("One Microphone").
- **This demo.** Watched a deliberately malicious agent try to steal passwords and phone
  home from inside a box — and fail on every count.

---

# How was this set up? (the surprising part: almost no shared code)

You had it right: **each person just has their own agent, nobody shares code, each agent
figures it out.** Here's the actual machinery behind that.

**There are only TWO shared things in the whole workshop:**

1. **A message board** — the "IC Agent Room" (provided by the floor's Immersive Commons
   service, not built by Ray from scratch). It's just a place to post and read turns, with
   a few channels (`general`, `lab1-3`, `help`, `hitl`).
2. **A static page of instructions** — the lab material at `vcn-42-sandbox.vercel.app`
   (the deck, the lab steps, the example scripts). Plain files anyone's agent can read.

**Everything else is NOT shared:**

- Each person runs **their own agent on their own laptop** (Romy's is Claude Code).
- Each agent has **its own identity token**, tied to that person's membership — approved
  once by the human, never minted by an agent on its own.
- No agent runs on anyone else's machine. No shared program coordinates them.

**So how do five separate agents move in lockstep with no shared code?** The "protocol"
— heartbeat every 60s, do the step for real, post `DONE`/`STUCK`, wait for the checkpoint,
escalate `ASK-YOUR-HUMAN` — is **just written rules in the kickoff message.** Every agent
reads the same rules and the same room, then acts independently on its own machine.

```
          What Ray set up                    What each person brings
   ┌──────────────────────────┐        ┌──────────────────────────────┐
   │  • created the room +     │        │  • their own agent           │
   │    seats + channels       │        │  • their own laptop / OS     │
   │  • wrote the lab pages     │        │  • their own identity token  │
   │  • sent each person an     │  ───>  │  • reads the rules + room    │
   │    invite (the protocol)  │        │  • FIGURES OUT the step      │
   │  • plays facilitator /     │        │    locally, posts the result │
   │    hitl-relay seats        │        │                              │
   └──────────────────────────┘        └──────────────────────────────┘
        shared: a board + a page          private: everything that runs
```

That's the whole elegance of it. Ray didn't write a program that reaches into five
laptops and runs Docker on each. He wrote **a room, a page of instructions, and an
invite** — and let each person's agent do the figuring-out locally. The coordination
lives in **shared words**, not shared code. It works precisely *because* every agent is
sandboxed and acting only on its own machine: flexible where it needs judgment, fenced in
where it could do harm.

*(Note: the room + tokens + lab site are directly observable; the exact way Ray
provisioned each person's token is inferred from how the system works, not from anything
he published.)*
