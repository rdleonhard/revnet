---
title: "Raising Inference: Staking the Treasury, VVV and Diem"
part: "Part II — The Mechanics"
status: draft
summary: The productive-reserve machine made concrete with Venice's real mechanics — staked VVV yields emissions and Diem (perpetual $1/day API credit), giving one treasury three separable value streams.
word_count: ~2,700
sources:
  - "revnet-in-venice.md (PROPOSAL) §3–§4, §8 invariants"
  - "Venice help centre — VVV tokenomics (web, 2026)"
  - "Venice blog — Introducing Diem as Tokenized Intelligence (web, 2026)"
  - "AInvest, Datawallet, Crypto-Economy — VVV staking/emissions/buyback coverage (web, 2026)"
open_questions:
  - Venice can change these parameters (emission rate, mint rate, buyback %, Diem target). All figures are as-of-2026 and should be re-checked before `final`.
  - Confirm exact emission distribution cadence and whether the 14% is fixed or usage-throttled.
---

# Raising Inference: Staking the Treasury, VVV and Diem

*Chapter 5 argued for a reserve that yields the very compute a product burns, then stopped short of naming one. It exists. Here it is, with the numbers.*

**Stake the token of an inference network and your treasury throws off two different things at once — more of the token, and a daily, perpetual right to compute — which is exactly the two-part yield the productive-reserve model needs.**

In one breath: Venice is a private-AI platform whose token, VVV, is *productive* when staked. Staking earns emissions (more VVV) and grants a pro-rata claim on the network's inference; that inference claim can be crystallized into a separate, tradable asset called Diem, where each unit is worth one dollar per day of API credit — forever. A revnet whose reserve is staked VVV therefore holds principal that stays redeemable, an emission stream that can fund the split, and an inference stream that can fund development. This chapter makes that concrete, using Venice's own live mechanics as of 2026 — and flags plainly that Venice controls those mechanics and can change them.

A necessary caveat before the numbers, per this book's house rule: **everything specific below is Venice's design as documented in 2026, and Venice can revise it.** Emission rates, mint rates, and cooldowns are parameters of someone else's protocol, not laws of nature. Treat them as the current terms of a counterparty — which is exactly what Chapter 14 will insist they are.

## What VVV is, and why staking it is productive

VVV is Venice's native token, launched in early 2025 on Base (an Ethereum layer-2), with a genesis supply of 100 million and no presale. On its own, held in a wallet, it does nothing special. **Staked**, it becomes an income-and-utility instrument, and that transformation is the whole reason it can serve as a productive reserve.

Staking VVV mints a staked position (sVVV) and does two things for the staker:

1. **It earns emissions.** New VVV is emitted to stakers — on the order of **14% annually** as of 2026, tied to network API usage. This is yield denominated in the reserve asset itself: stake VVV, receive more VVV.
2. **It grants inference.** A staked position confers a *pro-rata share of the network's AI compute capacity.* (Concretely, staking as little as 100 VVV unlocks unlimited personal use of the platform; larger stakes scale proportional API capacity.) The reserve, simply by being staked, is entitled to run models.

Two properties of this that matter for a treasury. There is a **7-day unstaking cooldown** — you cannot exit a staked position instantly; you wait a week. And there is a natural demand sink under the token: Venice runs an **automatic buyback-and-burn**, where roughly **$5 of every $100 spent on API credits is used to buy VVV on the open market and permanently burn it.** Real platform usage translates into standing buy pressure and a shrinking float. (For a revnet builder, both facts are double-edged, and Chapters 13–14 treat them as risks, not just features.)

## Diem: crystallizing the inference into an asset

The inference entitlement of staked VVV is a *flow* — capacity you have while you're staked. Venice's second-generation move, **Diem**, turns that flow into a *thing you can hold and trade.*

The mechanism: you lock sVVV to **mint Diem** at the current *Mint Rate*. Each Diem is a claim to **one dollar per day of Venice API credit, perpetually** — it does not expire and does not change in value. Stake enough and mint 100 Diem, and you hold a standing right to $100/day of inference, every day, forever. Diem is, in Venice's framing, a directly-held, tradable AI-compute asset.

The locking has a builder-friendly shape. While your VVV is locked into Diem you continue earning **80% of the normal staking yield** — so minting Diem doesn't cost you your emissions, only a fifth of them. And you can **burn Diem to unlock your original sVVV whenever you want**, with no additional lockup beyond the base cooldown. The Mint Rate itself isn't a fixed cap; it **starts low and rises as total Diem supply approaches the network's target**, throttling issuance as the system fills up.

For our purposes, the essential facts are three: Diem is **inference you can hold**, it is **perpetual**, and minting it **keeps most of your staking yield**. That combination is what lets a treasury run a product on its reserve's output without giving up the reserve's income.

## Three streams from one treasury

Now assemble it. A revnet whose reserve is staked VVV — with some portion locked into Diem — is not holding one asset with one return. It is holding **one principal that produces two distinct yields**, and each maps cleanly onto a role the venture needs to pay.

```
        contributions ──▶ ┌───────────────────────────┐
                          │  RESERVE = staked VVV      │
                          │  (portion locked → Diem)   │
                          └─────────────┬──────────────┘
                                        │
              ┌─────────────────────────┼─────────────────────────┐
              ▼                         ▼                          ▼
        PRINCIPAL                 EMISSION YIELD               DIEM
      the staked VVV             ~14%/yr in VVV          $1/day/unit of
      itself                     (×80% while             API credit,
              │                   locked to Diem)          perpetual
              ▼                         │                          │
      HOLDERS' FLOOR                    ▼                          ▼
      redeem pro-rata            fund THE SPLIT              fund the
      in VVV, anytime            (e.g. a marketer),         DEVELOPER's
      (after 7-day cooldown)     or compound the floor      actual inference
```

**Stream 1 — Principal (the floor).** The staked VVV is the holders' redeemable claim, exactly as Chapter 4 described a floor — except now the floor asset also earns. Holders redeem for a pro-rata share of the VVV, denominated in VVV. (The 7-day cooldown is why a real deployment needs a liquidity buffer and a redemption queue — a risk Chapter 13 handles head-on.)

**Stream 2 — Emission yield (the split).** The ~14% VVV emissions are new reserve that arrived without a new buyer. This is the money that pays for work *without touching principal* — the third source Chapter 5 was hunting for. Route it to a beneficiary (a marketer, say) as the split, or compound it back into the reserve to raise the floor for everyone. Either way, the operating cost is covered by yield, and the floor is never spent.

**Stream 3 — Diem (the developer's compute).** The locked-sVVV-minted Diem is a perpetual inference budget. Point it at the developer's live application and the product runs on the treasury's own output — the reserve literally fueling the thing it backs. This is the COGS hedge made physical: the founder isn't converting dollars to compute at retail, they're *holding compute that yields compute.*

One treasury; three jobs; the principal never consumed to do any of them. That is the productive-reserve model, no longer abstract.

## The ratchet — and the one rule that keeps it honest

There's a fourth effect, and it's the one most likely to be oversold, so here is the claim and its catch in the same breath.

**The claim:** if you compound the emission yield back into the reserve instead of paying it out, the reserve grows while the token supply doesn't — so **reserve-per-token rises**, which lifts the redemption floor and raises the price the next buyer pays. Later entrants buy in at a higher valuation than earlier ones, mechanically, funded by real yield rather than by hype. This is the "future buyers buy at an automatically increased valuation" property, and it is genuine.

**The catch — and it is load-bearing:** this is only safe if the ratchet is measured in **VVV-denominated terms** — units of VVV accrued per token — and *not* in VVV's dollar price. If you let the "increasing valuation" be driven by VVV's USD price, you've built a reflexive loop: buying pumps the price, the higher price advertises a higher valuation, which attracts buying, which pumps the price — until it doesn't, and the unwind is violent. The proposal doc (`revnet-in-venice.md`) makes this the first of its six invariants for exactly this reason. **The floor grows because more VVV backs each token, full stop — never because VVV got more expensive in dollars.** Measured in VVV units, the ratchet is real and mechanical. Measured in dollars, it's a bubble waiting to inflate. Same feature, two framings, and only one of them is safe. Get this single choice right and the appreciation is honest; get it wrong and you've built the thing the skeptics accuse you of.

This is why redemption, too, is denominated in VVV units and not dollars: it keeps the core of the machine — floor, ratchet, exit — entirely inside the reserve asset, where no price oracle can be manipulated to mint cheap or redeem rich. (The security payoff of that choice is Chapter 14's material.)

## "You've just moved all the risk onto one volatile token"

The sharp objection, and the right one to end on: an inert USDC reserve was *stable.* You've replaced it with a single, younger, more volatile token whose entire value depends on one company's platform. Haven't you traded a boring-but-safe floor for a floor that can fall out from under everyone?

Yes — that trade is real, and this book will not pretend otherwise. Denominating in VVV means the *dollar value* of the floor rises and falls with VVV, and a holder who redeems after a VVV drawdown gets fewer dollars back. That is a genuine cost, and it is the honest counterweight to the COGS hedge: you are hedged against inference getting *expensive*, and exposed to VVV getting *cheap.* Whether that trade is worth making is a real decision, not a free lunch, and Part IV walks through how to size and soften it (hybrid reserves, buffers, concentration caps) without hand-waving it away. What the model does *not* do is hide the exposure — redemption in VVV units makes it legible: you always know exactly how much VVV backs your token, and you bear the market risk on that VVV knowingly, not by surprise. A visible risk you chose beats an invisible one you didn't. But make no mistake that it is a risk, and that naming a real ticker is what makes it one.

*Stake the token of an inference network, and the treasury stops being money waiting to be spent — it becomes an engine that prints more of itself with one hand and pours compute into the product with the other. Just never let anyone tell you the floor rose because the price did.*
