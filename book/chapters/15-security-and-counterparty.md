---
title: "The Security and Counterparty Surface"
part: "Part IV — Risks, Honestly"
status: draft
summary: The web/smart-contract and dependency risks a builder actually faces — integration attack surface, oracle manipulation, MEV on the ratchet, and the one irreducible risk: Venice itself.
word_count: ~2,400
sources: ["revnet-in-venice.md (PROPOSAL) §7 security + dependency"]
open_questions:
  - "Consider adding a short 'questions to ask before you deploy' checklist as an appendix."
---

# The Security and Counterparty Surface

*Economics can fail from bad assumptions. Software fails from someone finding the one input you didn't consider. This chapter is about that someone.*

**Making the reserve productive means wiring it into another protocol and pricing an external asset — two new attack surfaces — and it means betting the whole thesis on one company's continued good behavior, which is the risk no amount of clever code removes.**

In one breath: an inert USDC reserve was, for all its dullness, *small* attack surface — money in a box. A productive reserve talks to Venice's staking contracts, may reference VVV's price, and settles into a bonding curve that searchers watch. Each is a way in. And beneath all of it sits a dependency you cannot engineer away: Venice. This chapter treats the security risks (which are containable) and the counterparty risk (which is not, only sizable) with equal honesty.

## Risk 1 — The integration attack surface

The moment the revnet stakes VVV, claims emissions, and mints Diem, it is calling into someone else's contracts. Every external call is surface: a bug in the staking adapter, the reward-claim logic, or the Diem accounting could misallocate or drain funds. The inert reserve never had this exposure because it never called anyone.

**Mitigation — Invariant 5, in full.** Isolate *all* Venice-specific logic in a **thin, separately-audited adapter module**, and keep the revnet's core accounting ignorant of Venice's internals. The core knows "the adapter holds N VVV of reserve"; it does not know how staking works. Put a **circuit breaker / pause** on the adapter so a discovered bug can be frozen without touching the core. And enforce, as a verified invariant, that **reserve-per-token can only rise from yield and fall only from honored redemptions** — never silently decrease. That last property is worth formal verification: it's the mathematical statement of "the floor is safe," and if it holds, an enormous class of integration bugs becomes non-catastrophic.

The principle: contain the blast radius. The founder is integrating a counterparty's code; she treats it as untrusted, wraps it thinly, and makes sure a failure in it can be paused rather than propagated.

## Risk 2 — Oracle manipulation

Anywhere the system prices VVV in dollars — for analytics, for a hybrid-reserve rebalance, for any "current valuation" display — it needs a price feed. And price feeds on a thinly-traded token are manipulable: a searcher can use a flash loan to spike VVV's price on a shallow pool for a single block, mint cheap or redeem rich against the distorted number, and unwind. Oracle manipulation is one of the most-exploited patterns in all of DeFi, and a naive productive-reserve build invites it.

**Mitigation — remove the oracle from the critical path entirely.** This is the security dividend of **Invariant 1** (denominate redemption in VVV units): the core mint-and-redeem path never asks "what is VVV worth in dollars?", so there is no price to manipulate on the path that moves the most value. A holder redeems for a *fraction of the VVV pile*, computed with no external price at all. Where a price genuinely is needed (peripheral analytics, hybrid rebalancing), use a **time-weighted average across multiple sources**, never a spot price, so a single-block spike can't move it. And value Diem **conservatively or at zero** in core accounting, so it can't be gamed either.

Notice the pattern: the same choice that contained the *economic* reflexivity risk (Chapter 14) also removes the *security* oracle risk here. Denominating in the reserve asset is doing an enormous amount of load-bearing work across both chapters — which is exactly why it's Invariant 1.

## Risk 3 — MEV on the ratchet

When reserve-per-token rises in a discrete jump — say, right when a batch of emissions is claimed and compounded — a searcher can sandwich it: buy $BUILD just before the jump posts, redeem or sell just after, extracting the yield increment that belonged to the standing holders. The ratchet, if it moves in visible steps, is a thing to front-run.

**Mitigation.** **Accrue yield continuously**, per-block, rather than in discrete claimable jumps, so there's no single moment to front-run — the floor drifts up smoothly and there's no edge in timing an entry to it. Lean on the existing **cash-out tax** (Chapter 4), which already penalizes fast in-and-out and blunts the profitability of a sandwich. For unusually large redemptions, a commit-reveal scheme can hide the intent until it's executed. None of this is exotic; it's standard MEV-hardening, and the point is simply to *do* it rather than leave the ratchet as a step function a bot can straddle.

## Risk 4 — Griefing the claim path

A smaller, real one: if the reward-claim function is permissionless, an attacker can spam it — wasting gas or manipulating the timing of when rewards post relative to the ratchet.

**Mitigation.** Access-control or economically bound the claim; **batch claims** on a schedule rather than allowing arbitrary triggering; make claim cadence policy-driven, not attacker-triggerable. Cheap to do, annoying to have skipped.

## Risk 5 — The irreducible one: Venice

Now the risk that no invariant removes, only sizes. The entire thesis — productive reserve, COGS hedge, Diem-funded product — rests on Venice continuing to honor Diem, maintain the network, and keep emissions flowing on terms that make the model work. If Venice changes staking terms, cuts emissions, deprecates Diem, gets acquired and pivots, or simply fails, the reserve thesis breaks. Every specific number in Chapter 6 and Chapter 13 is a parameter of *someone else's protocol*, set by a company, revisable by that company. This is a centralization dependency at the root of a design whose whole aesthetic is trustlessness, and pretending otherwise would be the book's biggest possible lie.

**Mitigation — and be clear that this is *management*, not *elimination*.** Treat Venice as an explicit **counterparty-risk line item**, sized deliberately: don't bet protocol survival on one provider's roadmap; make the exposure a decision, not an accident. Maintain an **exit path** — the ability to convert VVV → ETH/USDC and fall back to an inert reserve — if Venice's terms deteriorate past a threshold. Monitor Venice's governance and announcements as an operational duty, not an afterthought. And design the adapter (Invariant 5) so a **future multi-provider inference reserve** is possible: Venice is v1, the first productive-reserve asset that happens to yield compute, not a permanent hard-wire. If other inference networks develop stakeable, yield-bearing tokens, the same architecture holds with the counterparty risk diversified across several rather than concentrated in one.

But the honest bottom line, stated plainly: **you can contain the security risks and only *reduce* the counterparty risk.** A builder who deploys this is making a real bet on Venice. That bet might be a good one — Venice's usage-driven buyback and real product give the token genuine underpinning — but it is a bet, it is concentrated, and it should be entered as such.

## "So the trustless treasury actually trusts a company"

The objection writes itself, and it's correct: for all the immutable-contract, no-oracle, denominate-in-the-asset discipline, the productive reserve's value ultimately depends on trusting Venice. Isn't the trustlessness a bit of a costume?

The honest answer is to be precise about *what* is trustless and *what* isn't — the same move as the $CITE chapter. The revnet's **rules** are trustless: issuance, floor, redemption, the fact that no one can dilute you or seize the reserve — all immutable, all real, all independent of Venice. What is *not* trustless is the **value of the reserve asset**, which depends on Venice the way any asset's value depends on its issuer. But notice: this is not a new or special weakness. A USDC reserve trusts Circle to honor the peg. An ETH reserve trusts Ethereum's validators and roadmap. *Every* reserve asset carries issuer risk; there is no such thing as a reserve that trusts no one. The productive-reserve model doesn't uniquely introduce counterparty trust — it *concentrates* it in one younger, more volatile issuer in exchange for yield and a COGS hedge. That concentration is the honest cost, and the mitigations above are about sizing and diversifying it, not pretending it's absent. The trustlessness isn't a costume; it's real and it's *scoped* — to the rules, not to the asset's issuer, and the book has never claimed otherwise.

*You can engineer the security risks down to manageable. You cannot engineer Venice out of the design — you can only size the bet, keep the exit open, and never, ever pretend the bet isn't there.*
