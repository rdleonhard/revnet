---
title: "How a Solo Dev Raises Compute, Step by Step"
part: "Part V — The Playbook"
status: draft
summary: The whole argument turned into an actionable sequence — define the idea and inference budget, choose the reserve mode, set issuance/split/Diem routing, publish the accountability structure, launch and iterate.
word_count: ~2,500
sources: ["revnet-in-venice.md (PROPOSAL) §10 build path", "$SERF schedule pattern"]
open_questions:
  - "Keep tooling-agnostic to avoid dating the book, or name specific stacks? Currently agnostic."
---

# How a Solo Dev Raises Compute, Step by Step

*Enough theory. If you are the founder from Chapter 1, sitting at the desk from the interlude, what do you actually do on Monday?*

**Raising compute instead of capital is a concrete sequence — define the need, choose how productive the reserve should be, set three parameters, publish how you'll be held to account, and launch — and most of the hard parts are decisions, not code.**

In one breath: this chapter is the book as a checklist. It assumes you've accepted the thesis and want to run it. It stays tooling-agnostic on purpose — specific stacks date fast — and it flags at each step where a decision is genuinely yours versus where the invariants make the choice for you. Nothing here is legal advice; the one step that touches law says so and stops.

## Step 0 — Decide if this is even for you

Before anything, a gate. The productive-reserve revnet fits a specific founder: solo or tiny, open-source (so backers can verify), with a product whose dominant cost is inference, raising a modest amount from a crowd of believers rather than a large amount from institutions. If that's not you — if you need millions, or your work is closed, or your costs are mostly people — a conventional raise may fit better, and the honest move is to use it. The model is a sharp tool for a specific shape, not a universal one. Only proceed if the shape matches.

## Step 1 — Define the idea and the inference budget

Write down two things concretely: *what you're building* (in a form a backer could read your repo and judge) and *what it will cost to build and run in inference.* The second is the number that replaces "how much runway do I need" — estimate your monthly model spend to develop the product and to serve early users. This is your compute budget, and it sizes everything downstream. Be honest and slightly generous; under-budgeting inference is the classic solo-founder mistake.

## Step 2 — Choose the reserve mode

Your first real decision, and the invariants frame it:

- **Inert reserve (USDC/ETH):** stable floor, no yield, operating costs must come from principal or new buyers. Simple, boring, and it carries the operating-cost trap from Chapter 5. Choose it only if you value a rock-stable dollar floor above everything.
- **Productive reserve (staked VVV):** yield funds ops, Diem funds the product, COGS-hedged — at the cost of concentration and counterparty risk (Chapters 14–15). The book's recommendation *for a compute-native founder.*
- **Hybrid:** a capped VVV percentage plus a USDC buffer. Dials the tradeoff — some hedge, some stability. A reasonable default for the risk-averse.

```
   DECISION: reserve mode
   ┌────────────────────────────────────────────────────────────┐
   │ need a stable dollar floor above all?      → INERT (USDC)   │
   │ product cost is inference, want the hedge? → PRODUCTIVE (VVV)│
   │ want the hedge but fear volatility?        → HYBRID          │
   └────────────────────────────────────────────────────────────┘
```

## Step 3 — Set the three parameters

A revnet is mostly three numbers, fixed at launch and immutable forever — so this is where your pre-launch care goes, because there is no patch (Chapter 4).

1. **Issuance decay** — how fast the mint rate worsens for later backers. Steeper rewards early conviction more; gentler is fairer to latecomers. Set it to reflect how much early risk you're asking people to take.
2. **The split** — who gets paid from yield, and how much. Point it at yourself (a stipend), a marketer, a bounty pool — whatever the venture needs. Under the productive model, define it as a *percentage of realized yield* with a coverage ratio ≥ 1 (Invariant 3), never a fixed dollar sum.
3. **Diem routing** — how much of the staked reserve to lock into Diem for the product's inference, versus leave as pure emission-earning stake. This trades emission yield (you keep 80% on the locked part) for standing compute. Size it to your Step 1 inference budget.

## Step 4 — Wire the invariants in

Not optional, and not a matter of taste — these are the rails that keep the design honest, from Chapter 13:

- Redemption denominated in **VVV units**, pro-rata (Invariant 1).
- Ratchet sourced from **VVV-denominated yield**, never USD price (Invariant 2).
- Payouts a **function of realized yield**, capped (Invariant 3).
- Principal governance separated from yield-routing governance; **redemption right immutable** (Invariant 4).
- Venice logic behind a **thin, audited, pausable adapter** (Invariant 5).
- **No Diem stranded** — route or sell surplus (Invariant 6).

If you internalize the one principle underneath them — *keep the reserve asset central, fund ops from yield, keep discretion away from the floor* — you'll get most of these by default. But check each explicitly before launch, because immutability means a missed rail is permanent.

## Step 5 — Publish your accountability structure

This is the $SERF move, and it's what converts "back my idea" into something a stranger can say yes to. Before you take money:

- Write a **sworn schedule** — milestones, order, dates, and *what evidence counts as done* for each. Make it binding and public.
- Decide how you'll be **watched**: what a supervisor (an AI boss, or just a public reporting cadence) will check your progress against, and how holders can lobby that boss without touching the money-rules.
- Set up the **transparent feedback path** — where holder suggestions land and how they're made visible to all holders, not whispered privately (the pager, in the interlude).

You are voluntarily building the thing that will hold you accountable, because visible accountability is the product you're selling to backers.

## Step 6 — Launch, report, iterate

Deploy the immutable contracts. Then the loop that never stops: the reserve stakes and yields, Diem funds the product, the split pays, the boss reports to holders on your progress against the schedule, holders lobby the boss, and the floor ratchets from compounded yield. Your job is to *build in public and let the machine witness it.* Report honestly — a documented pivot beats a hidden slip every time, and the instruments make honesty the only sustainable option anyway.

## The whole playbook on one page

| Step | Decision | The invariant/rule that constrains it |
|---|---|---|
| 0 | Is the model right for you? | Solo, open-source, inference-dominated, crowd-funded |
| 1 | Idea + inference budget | Budget sizes everything downstream |
| 2 | Reserve mode | Inert / productive / hybrid — your risk call |
| 3 | Issuance, split, Diem routing | Split = % of realized yield (Inv. 3) |
| 4 | Wire the invariants | All six; no patch after launch |
| 5 | Accountability structure | Sworn schedule + boss + transparent feedback |
| 6 | Launch and iterate | Build in public; report honestly |

## The one step this book won't take for you

There is a step 3.5 that lives between the parameters and the launch, and it is the one the book has deliberately refused to opine on: **the legal structure.** A token representing a floored, yield-bearing, appreciating claim, sold to a crowd, sits squarely in territory governed by securities law — and that territory is not this book's subject and not this author's to advise on. Before you launch anything real, this is where you stop reading and call a securities attorney in your jurisdiction. The mechanism is the part an engineer can check; the legal wrapper is the part with no on-chain shortcut, and it is genuinely load-bearing. The book gave you the machine. Whether and how you may lawfully turn it on is a question for counsel, and treating this paragraph as permission to skip that call would be the one way to misuse everything that came before it.

*Raising compute isn't a leap of faith; it's a checklist with one lawyer in the middle of it. Define the need, choose the reserve, set three numbers, wire the rails, publish your rope, and build in public. The machinery is ready. The judgment is yours.*
