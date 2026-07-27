---
title: "Revnet in Venice — The Keystone, Worked End to End"
part: "Part III — Case Studies"
status: draft
summary: The spine chapter — a solo developer raises compute through a productive-reserve revnet, walked start to finish with numbers, held together by the six invariants.
word_count: ~3,100
sources:
  - "revnet-in-venice.md (PROPOSAL) — full"
  - "Venice VVV/Diem live docs (2026) — as in Ch 6"
open_questions:
  - "All VVV/Diem figures are illustrative and depend on Venice's live parameters (emission rate, Mint Rate, cooldown). Re-verify before `final`; the walk-through's shape, not its decimals, is the point."
---

# Revnet in Venice — The Keystone, Worked End to End

*Every chapter until now has been a piece. This is where the pieces become a machine you could actually build — one founder, one treasury, one lifecycle, with the numbers in.*

**Put it all together and you get a solo developer who raises compute, runs their product on the reserve's own output, pays their people from its yield, floors their backers in the reserve asset, and lets the floor rise on its own — every step guarded by an invariant that keeps it honest.**

In one breath: this is the book's thesis reduced to a single worked example. A developer deploys a productive-reserve revnet whose treasury is staked VVV; the reserve's two yields (emissions and Diem) fund the split and the product; holders hold a VVV-denominated floor that ratchets upward; and six invariants keep the whole thing from tipping into the failure modes the skeptics rightly fear. Every number here is illustrative and rests on Venice's 2026 parameters, which Venice controls and can change — the *shape* is the lesson, not the decimals.

## Meet the founder, one more time

She's the developer from Chapter 1: solo, open-source, an idea that would once have needed a team, and a cost structure dominated by inference. She's going to raise not money but compute, and she's going to do it through the machine Part II built. Call her token $BUILD. Here's her whole life cycle, then we walk it step by step.

```
   ┌─ 1. RAISE ───────────────────────────────────────────────────────┐
   │  backers contribute → mint $BUILD → reserve = 50,000 VVV          │
   └───────────────────────────────┬──────────────────────────────────┘
                                    ▼
   ┌─ 2. STAKE ───────────────────────────────────────────────────────┐
   │  stake all 50,000 VVV → ~14%/yr emissions + inference entitlement │
   │  lock part of sVVV → mint Diem (keep 80% of yield on locked part) │
   └───────────────────────────────┬──────────────────────────────────┘
              ┌─────────────────────┼─────────────────────┐
              ▼                     ▼                     ▼
   ┌─ 3a. DIEM ────────┐ ┌─ 3b. EMISSIONS ─────┐ ┌─ 3c. PRINCIPAL ─────┐
   │ ~$12k/yr inference│ │ ~7,000 VVV/yr:      │ │ 50,000 VVV stays    │
   │ → runs the product│ │ split + compound    │ │ as holders' floor   │
   └───────────────────┘ └──────────┬──────────┘ └──────────┬──────────┘
                                     ▼                        ▼
                          ┌─ 4. RATCHET ────────┐  ┌─ 5. REDEEM ─────────┐
                          │ VVV-per-token rises │  │ pro-rata VVV back,  │
                          │ (compounded yield)  │  │ 7-day cooldown      │
                          └─────────────────────┘  └─────────────────────┘
```

## Step 1 — The raise

Backers contribute, and the revnet mints $BUILD on the staged-issuance curve: the earliest backers get the best rate, by rule, exactly as Chapter 4 described. When the raise settles, the reserve holds — to pick a clean number — **50,000 VVV**, and there are **50,000 $BUILD** outstanding. So each $BUILD is backed by 1 VVV. (VVV's dollar price will wander; we deliberately track the reserve in *VVV units*, and in a moment you'll see that's not a stylistic choice but a safety rail.)

> **Invariant 1 — redemption is denominated in VVV units, pro-rata.** A $BUILD holder's claim is "1/50,000 of the reserve's VVV," not "some number of dollars." This keeps the core exit path from ever touching a price oracle, which — as Chapter 14 will show — removes the single richest target for manipulation. The floor is a fraction of a pile of VVV, full stop.

## Step 2 — Staking the treasury

The reserve doesn't sit. All 50,000 VVV gets staked, which does the two things from Chapter 6: it earns emissions (~14%/yr as of 2026, so roughly **7,000 VVV in the first year**) and it entitles the treasury to inference capacity. Part of the staked position is then locked to mint **Diem** — the perpetual $1/day-per-unit compute asset — and, crucially, the locked portion still earns 80% of its staking yield. The treasury is now a three-stream engine: principal, emissions, Diem.

> **Invariant 5 — Venice logic lives behind a thin, audited, pausable adapter.** All of this — staking, claiming emissions, minting Diem — happens through an isolated module, not tangled into the revnet's core accounting. If Venice changes an interface, or a bug appears, the blast radius is one auditable, pausable component. The founder is integrating a counterparty, and she treats it like one.

## Step 3 — Three streams, three jobs

Now the treasury pays for the whole venture without spending its principal.

**3a — Diem runs the product.** Say the founder's product needs about **$12,000/year** of inference to serve its users. She locks enough sVVV to mint ~33 Diem ($33/day ≈ $12k/yr) and points that inference at the live app. The product runs on the reserve's own output, in kind. No dollars raised, converted, and spent at retail — the reserve *is* the fuel. This is the COGS hedge from Chapter 2 made literal: if inference gets scarcer and pricier, the Diem she holds is worth more in the same motion.

**3b — Emissions fund the split, or compound.** The ~7,000 VVV/year of emissions is money that arrived with no new buyer. She splits it: a slice pays a marketer (the split from Chapter 7) — a real stipend, funded entirely by yield — and the rest compounds back into the reserve.

> **Invariant 3 — committed payouts are a function of realized yield, capped by a coverage ratio ≥ 1.** The marketer's split is defined as *a percentage of emissions actually received*, never a fixed dollar sum. If emissions fall (Venice tapers them, or network stake dilutes her share), the split throttles down automatically, and it can never reach past yield into principal. The floor is structurally unspendable for operations. This is the anti-ponzi rail from Chapter 5, enforced arithmetically.

**3c — Principal is the floor, untouched.** The 50,000 VVV stays whole. Every operating cost above was paid from yield. The holders' redemption claim is exactly as strong at the end of the year as at the start — stronger, actually, because of the next step.

> **Invariant 4 — principal governance ≠ yield-routing governance.** Holders can vote on *where the yield goes* — more to the split, more to compounding, tuning the marketer's cut — but they can *never* vote to touch the principal or rewrite the redemption right. That right is immutable. Governance steers the yield; it cannot reach the floor. (This is the same architecture as $SERF's boss: holders shape the soft layer, never the hard core.)

> **Invariant 6 — no day's Diem is stranded.** Diem is a daily flow; unused inference evaporates. If the product under-uses its Diem on a quiet day, the surplus is routed — sold, or handed to holders as a perk — never left to expire. Use it or route it, never lose it.

## Step 4 — The ratchet

Here's the part that looks like magic and isn't. The emissions she compounded (3b) added VVV to the reserve while the $BUILD supply stayed at 50,000. So after year one, the reserve might hold — say she compounded 4,000 of the 7,000 VVV — **54,000 VVV backing the same 50,000 $BUILD.** Backing per token rose from 1.00 to 1.08 VVV. The redemption floor went up 8%, and the price a new buyer pays rose with it. Later backers enter at a higher valuation than the earliest ones — mechanically, from realized yield, not from hype.

> **Invariant 2 — the ratchet is sourced from VVV-denominated yield, never VVV's USD price.** The floor rose because *more VVV backs each token* (1.00 → 1.08 VVV), and for no other reason. We never say "the floor rose because VVV got more expensive in dollars" — that would be the reflexive bubble Chapter 6 warned about. Measured in VVV units, the 8% is real and durable. Measured in dollars, it would be a mirage. Same number, and only one framing is safe. This is the single most important line in the whole design.

## Step 5 — Redemption

A holder wants out. They send their $BUILD back; after the 7-day unstaking cooldown, they receive their pro-rata share of the reserve — now 1.08 VVV per token instead of the 1.00 they might have entered at. They bear exactly one risk, named honestly since Chapter 6: **VVV's dollar price.** If VVV fell over the year, their 1.08 VVV is worth fewer dollars; if it rose, more. The floor guaranteed their *share of the VVV*, which grew; it never guaranteed a dollar price, which the market sets. That is the "take the loss and take back your VVV" shape — a visible, chosen exposure, not a hidden one.

The 7-day cooldown is why a real deployment holds a liquid VVV buffer and runs redemptions through a queue — you can't unstake instantly, so you don't promise instant exit. (Chapter 13 sizes that buffer against a bank-run.)

## The year on one page

| | At launch | After year 1 |
|---|---|---|
| Reserve (VVV) | 50,000 | ~54,000 (compounded emissions) |
| $BUILD supply | 50,000 | 50,000 |
| Backing per token | 1.00 VVV | ~1.08 VVV |
| Product's inference | funded by ~33 Diem | funded by ~33 Diem |
| Marketer's split | % of emissions | % of emissions (throttles with yield) |
| Principal spent on ops | 0 | 0 |
| Holder's risk | VVV price | VVV price |

Read that table and the thesis is just… sitting there, true. A solo developer raised compute, ran her product on the reserve's output, paid a marketer from yield, spent none of the principal, and handed her backers a floor that rose 8% in VVV terms — all on rules no one can change, with the founder's discretion removed from every place it could do harm.

## Where the other case studies plug in

This keystone isn't separate from the earlier examples; it's their common engine.

- Bolt on **$SERF's** boss and sworn schedule, and the founder's self-directed split becomes *accountable* — the AI manager reports her progress to the $BUILD holders, who lobby the boss without touching the money-rules. The Diem-native version of $SERF *is* this chapter with an overseer added.
- The anti-ponzi proof that **$HARD** made literal (redemption from external cashflow, never from new buyers) holds here too, in a different form: ops come from emissions, not deposits. Different source, same clean shape.
- And the whole thing is issued with the honesty **$WAKE** and **$CITE** insisted on — immutable terms, a real floor, precommitment over discretion — just applied to a compute-native founder instead of a forever-product or a centralized firm.

## "Six invariants is a lot of ways to get it wrong"

The honest objection to end on: if the model only works when all six invariants hold, that's six single points of failure. Isn't a design that fragile just... fragile?

Two answers. First, **the invariants aren't six independent bets — they're one idea, restated.** Denominate in the reserve asset (1), grow the floor from that asset's yield (2), pay ops only from that yield (3), never let governance reach the principal (4), isolate the counterparty (5), waste nothing (6). Underneath, they're all the same discipline: *keep the reserve asset central, keep operations funded by yield, and keep discretion away from the floor.* A builder who internalizes that one principle gets most of the six for free. Second, **naming them is what makes the design safe, not fragile.** Every one of these invariants marks a place where a careless build *would* fail — and the failure mode is real whether or not you wrote the invariant down. Unwritten, they're six landmines. Written, they're six checks. A model that names its own failure conditions precisely is more robust than one that waves at "trust me," not less. The fragility was always there in the problem; the invariants are how you engineer around it in the open.

*This is the whole book on one desk: raise in compute, reserve in compute, run on compute, floor your backers in the asset itself, and let the yield lift the floor — six rails keeping every step honest. The founder changed. Now the funding has caught up.*
