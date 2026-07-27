---
title: "The Economic Caveats"
part: "Part IV — Risks, Honestly"
status: draft
summary: Where the productive-reserve model can fail economically — concentration, yield decay, bank-run liquidity, reflexivity — each paired with its mitigation.
word_count: ~2,400
sources: ["revnet-in-venice.md (PROPOSAL) §7 economic + §8 invariants"]
open_questions: []
---

# The Economic Caveats

*A book that only sold you the upside would be the exact kind of writing this book was built to be the opposite of. So here is where it breaks.*

**The productive-reserve model's benefits are real only if its risks are managed — and the honest news is that its worst risk and its subtlest risk are killed by the same single design choice.**

In one breath: swapping an inert stablecoin reserve for staked VVV buys you a productive treasury and a COGS hedge, and it costs you four economic risks — concentration in a volatile asset, yield that can decay, a liquidity mismatch on exit, and the temptation of reflexive valuation. This chapter names each with its mitigation. None is hand-waved; one is irreducible and gets its own treatment in Chapter 15. The house rule holds throughout: the catch sits next to the claim.

## Caveat 1 — Concentration: you swapped stable for volatile

The plainest cost. A traditional revnet reserve in USDC is stable; the floor, in dollars, barely moves. A reserve of VVV is a single, younger, more volatile token, and the floor's dollar value now rides with it. A holder who redeems after a VVV drawdown gets their full VVV share — but worth fewer dollars. This is a genuine, structural downgrade in floor stability, and it must never be sold as anything else.

**Mitigation.** Set expectations honestly and denominate in VVV: this is a VVV-risk instrument *by design*, and redemption returns VVV units, so the exposure is visible, not hidden. For founders who want a softer floor, a **hybrid reserve** — a governance-capped VVV percentage with a USDC buffer — trades some COGS hedge for some stability. Cap the maximum VVV concentration in the revnet's parameters. And never, ever market the floor in dollar terms; market it in VVV, where it's true.

The honest framing: you are hedged against inference getting *expensive* and exposed to VVV getting *cheap*. That is a real trade, not a free lunch, and whether it's worth making is a decision the founder and backers make with eyes open.

## Caveat 2 — Yield decay and Diem dilution

The model leans on two flows: emissions (to fund the split and the ratchet) and Diem (to fund the product). Both can shrink. Emission schedules taper over time — "offset the split with yield" fails if yield falls below the committed split. And Diem is a *share of a fixed daily inference pie*: as total network stake grows, the inference per staked VVV falls, even if the treasury's own stake is unchanged. The founder can be diluted by other people staking.

**Mitigation.** This is exactly what **Invariant 3** exists for: make every committed payout *a function of realized yield*, never a fixed dollar sum, and enforce a **coverage ratio ≥ 1** — if realized yield can't cover the split, the split throttles automatically, *before* principal is ever touched. Never write a fixed obligation the reserve might not be able to earn. For Diem dilution, treat the inference budget as variable: monitor network-wide stake growth, re-forecast the product's compute allotment on a schedule, and size the product's usage against a conservative estimate of future Diem, not today's.

The discipline: the model must degrade gracefully as yield falls, not snap. A split that shrinks in a lean year is working as designed; a split that forces a principal drawdown is a bug.

## Caveat 3 — The bank-run: unbonding vs. redemption

Staked VVV has a **7-day unstaking cooldown.** But holders expect to redeem their $BUILD reasonably promptly. If many redeem at once, the contract can't unstake fast enough to pay them — a classic liquid-staking liquidity crunch, the on-chain version of a bank run. The reserve is solvent but temporarily illiquid, and a queue of holders is waiting on a 7-day timer.

**Mitigation.** Hold a **liquid VVV buffer** (unstaked) sized to expected redemption velocity, so ordinary exits are paid instantly. Beyond the buffer, implement a **redemption queue that mirrors the cooldown**: redeemers wait out the 7 days, exactly as they would if they'd staked and unstaked themselves — no false promise of instant exit, no insolvency, just an honest timer. If a liquid-staking wrapper for VVV exists, holding *that* keeps the reserve liquid and sidesteps the problem. And disclose the cooldown prominently, so no holder is surprised by it in a moment of stress.

```
   redemption demand in a stress event
        │
        ▼
   liquid buffer (instant) ──▶ empty? ──▶ redemption queue (7-day cooldown)
        │                                        │
     ordinary days                         stress days: solvent, just slow —
     paid on the spot                      never insolvent, never a rug
```

The key property: the design fails *slow*, not *insolvent*. A holder in a run waits; they do not lose their claim.

## Caveat 4 — Reflexivity: the ratchet that eats itself

The subtlest and most dangerous. The ratchet — future buyers entering at a higher floor — is a genuine feature. But if you let its "increasing valuation" be driven by VVV's *dollar price*, you build a reflexive loop: buying pumps the price, the higher price advertises a higher valuation, which attracts more buying, which pumps the price further — a self-reinforcing spiral that inflates and then unwinds violently. That is precisely the bubble the skeptics accuse token schemes of being, and a careless build walks straight into it.

**Mitigation.** **Invariant 2**, the most load-bearing line in the whole design: source the ratchet from **VVV-denominated yield** — units of VVV per token — and *never* from VVV's USD price. The floor rises because more VVV backs each token, mechanically, for no other reason. Measured in VVV units, the appreciation is real and durable; measured in dollars, it would be a mirage, and you simply never measure it that way. Additionally, keep the treasury a **small fraction of total VVV stake**, so the project is a price-*taker*, not a price-*maker* — a treasury large enough to move VVV's price is a treasury that has started feeding its own reflexive loop.

Here is the payoff of the whole chapter, and the thing to underline: **Caveat 1's exposure and Caveat 4's reflexivity are both neutralized by the same choice** — denominate in VVV units and source the ratchet from VVV-denominated yield. Get that one decision right and the two scariest economic risks are contained at a stroke. The rest is monitoring and honest disclosure.

## The caveats on one page

| Risk | The danger | The mitigation |
|---|---|---|
| **Concentration** | Floor's dollar value rides a volatile token | VVV-denominated redemption; optional hybrid reserve + concentration cap; never market the floor in dollars |
| **Yield decay / Diem dilution** | Emissions taper; per-VVV inference shrinks as network stake grows | Payouts = % of realized yield; coverage ratio ≥ 1; variable inference budget, re-forecast on a schedule |
| **Bank-run** | 7-day cooldown vs. mass redemption | Liquid buffer + cooldown-mirroring queue; fail slow, never insolvent |
| **Reflexivity** | USD-priced ratchet → inflate-and-collapse | Ratchet from VVV-denominated yield only; stay a price-taker |

## "If it needs this much managing, is it actually better than boring USDC?"

The fair objection: a plain USDC reserve had none of these problems. It just sat there, stable and safe. Have we invented a pile of risk to manage in exchange for some yield?

The answer is to weigh both sides honestly, which is the whole point of the chapter. The USDC reserve had no concentration, decay, cooldown, or reflexivity risk — true. It also had the *opportunity cost* and the *operating-cost trap* from Chapter 5: idle capital, and a cruel choice between eroding the floor and importing ponzi dynamics to pay for work. Those weren't visible as "risks" because they were baked into the boring version's structure, but they were real losses every single day. The productive reserve trades a set of *quiet, structural* costs for a set of *loud, manageable* ones — and adds the COGS hedge that no stablecoin can offer. For a founder whose product is compute, that trade is usually worth it, but "usually" is the honest word. For a founder who values a rock-stable dollar floor above a productive treasury, boring USDC is a legitimate choice, and the hybrid reserve exists precisely to let them dial the tradeoff. The model doesn't claim to dominate the boring version everywhere. It claims to be better *for the compute-native founder* — and it names exactly what that founder is taking on to get there.

*The productive reserve doesn't remove risk; it trades the invisible kind for the kind you can see and manage. That trade is only honest if you can see all of it — so here it all is.*
