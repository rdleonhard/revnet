---
title: "Why Money Was the Bottleneck, and Inference Is the New One"
part: "Part I — Compute Is the New Capital"
status: draft
summary: Money was scarce because it bought scarce labor; AI collapses the labor cost, and the residual scarcity migrates to compute — the true variable cost of an AI-native product.
word_count: ~2,300
sources: ["revnet-in-venice.md (PROPOSAL) — COGS-hedge thesis T2"]
open_questions:
  - Replace the illustrative inference-COGS percentages with a sourced figure before this chapter goes to `final`.
  - Confirm the Jevons framing lands for a non-economics reader or needs a plainer analogy.
---

# Why Money Was the Bottleneck, and Inference Is the New One

*Money was never the point. It was a solvent — the thing you poured on a harder problem to dissolve it. The question worth asking is what the hard problem actually was.*

**Capital was scarce because the thing it bought — skilled human hours — was scarce; collapse the cost of those hours and the scarcity doesn't vanish, it relocates.**

In one breath: for the entire history of software startups, the binding constraint was people. A good idea was cheap and a working implementation was expensive, and the gap between them was measured in engineer-years. Money mattered because it was the only way to buy engineer-years you didn't have. Everything else in the funding apparatus — the dilution, the boards, the eighteen-month runways — was scaffolding around that one fact.

This chapter is about what happens to the scaffolding when the fact changes.

## Scarcity is conserved; it just moves

Think of a startup's cost structure as a landscape, and cost as water. It pools at the lowest, scarcest point — whatever input is hardest to get. For decades that point was labor. A seed round was a bucket of water poured onto the labor problem: hire the engineers, and the idea gets built.

AI did not drain the landscape. It *raised the labor floor* — it made the once-scarce input, skilled implementation hours, dramatically cheaper and more abundant. One developer with frontier models can now do what took several. When you do that, the water doesn't disappear. It runs downhill to the next-lowest point. And for an AI-native product, the next-lowest point — the new scarcest, most expensive input — is **inference:** the compute burned every time a model runs.

This is not a metaphor for a small effect. It is the whole shape of the new business.

```
   WHERE THE COST POOLS

   Old software startup                 AI-native product
   ┌───────────────────────┐            ┌───────────────────────┐
   │ labor      ██████████  │  scarce    │ labor      ██          │  cheap now
   │ compute    ██          │  cheap     │ compute    ██████████  │  scarce now
   │ idea       █           │            │ idea       █           │
   └───────────────────────┘            └───────────────────────┘
       money bought labor                    money must buy compute
```

The founder from Chapter 1 feels this directly. Their build cost is model calls. Their *running* cost is model calls. The scarcest input they face is not a person they can't afford to hire — it is inference they can't yet afford to run.

## The tell: cost of goods

There is a precise, unromantic way to see how deep this goes, and it is the concept of **cost of goods sold** — COGS, the direct variable cost of delivering one more unit of your product.

For a classic SaaS business, COGS was gloriously small. Once the software was written, serving one more customer cost a sliver of server time — pennies. That is why SaaS gross margins famously ran 80–90%: the marginal cost of the product rounded to zero, and almost every dollar of revenue was gross profit. The expensive part was the one-time build (labor), not the serving.

An AI-native product breaks this. Every time a user makes a request, the product runs a model, and running a model costs real, metered compute *every single time.* The cost doesn't amortize away after the build; it recurs on every call. Depending on the product, inference can eat a large share of each dollar of revenue — a structural inversion of the SaaS margin story. [The exact share is product-specific and moves with model prices; I'm flagging the specific percentage as a to-verify item rather than asserting a number I can't source.]

Sit with what that means. For this founder, **the biggest cost of building the product and the biggest cost of running the product are the same thing** — inference — and that thing is a metered commodity with a price you can look up. Their capital need and their cost of goods have collapsed into a single substance.

That collapse is the hinge of this entire book. Because once your dominant cost is a specific, purchasable commodity, a strange and powerful option opens up: instead of raising dollars and converting them to that commodity at retail, over and over, forever — you could **raise, hold, and repay in the commodity itself.** You could denominate the whole venture in compute.

## Why "denominate in compute" is more than a slogan

Hold a treasury in dollars and you are exposed to a quiet mismatch: your reserve is money, but your costs are compute, and the price of compute relative to money can move against you. If inference gets more expensive, your dollar reserve buys less of the thing you actually need, exactly when you need it most.

Now flip it. Suppose your reserve *were* compute — or a productive asset that yields compute. Then when inference gets scarcer and pricier, your reserve becomes *more* valuable in the same motion, because it is denominated in the scarce thing rather than the abundant one. Your treasury and your cost of goods rise and fall together. You are hedged, structurally, against the one price that can hurt you most — not by cleverness, but by holding the right substance.

This is the economic seed of the book's keystone proposal (the [PROPOSAL] doc, `revnet-in-venice.md`), and it has a name there: the reserve as a natural COGS hedge. For an AI-native project, a treasury that yields inference is collateralized in the exact currency it spends. Few businesses in history have been able to say that. This one can — and later chapters show the mechanism that makes it real.

We are not there yet. Chapter 3 has to build the funding instrument from zero first. But the reason we bother is right here: *if the scarce input, the cost of goods, and the natural reserve are all the same substance — compute — then the honest thing is to build the whole financial structure out of that substance.*

## "But inference keeps getting cheaper — won't this whole premise evaporate?"

This is the strongest objection to the chapter, and you should press it hard: model prices have fallen relentlessly. Cost per token drops; open models get better; yesterday's frontier capability is next year's commodity. If inference is racing toward free, why build a thesis on its scarcity?

Two reasons, and together they are decisive.

First, **falling unit prices don't shrink budgets — they raise ambition.** This is an old pattern; economists call it the Jevons paradox. When a resource gets cheaper to use, we don't spend less on it; we find so many more uses that total consumption *rises.* Cheaper compute per call means agents that make hundreds of calls where one used to do, models run over entire codebases instead of snippets, products that were absurd at last year's prices becoming merely expensive at this year's. The founder doesn't pocket the savings — they spend them on a bigger idea. The inference bill stays large because the ambition expands to fill it.

Second, **the frontier stays expensive by definition.** "Inference got cheap" is always a statement about *last year's* capability. The models that let one developer replace a team are the newest, largest, most costly ones — and those are the ones this founder needs to attempt something worth funding. Commodity inference is real and useful, but the projects that warrant outside backing are precisely the ones reaching for capability that is not yet cheap. As long as there is a frontier, running at it costs money.

So the premise holds — not despite falling prices, but partly because of them. The unit cost drops; the total spend, and the strategic importance of securing it, does not.

## What we've established

The founder changed (Chapter 1). Now we can say why that change reorganizes everything downstream: the scarcity that money used to clear has moved from labor to compute; the dominant build cost and the dominant cost of goods have merged into a single metered commodity; and that merger makes it not just possible but *natural* to run the whole venture — the raise, the reserve, the repayment — in compute rather than cash.

What's missing is the instrument. We have a founder who should raise compute and a good reason to reserve in it, but no honest machine for doing so — nothing that lets a crowd of verifying believers put resources in on fixed terms, get a floor under their downside, and let the earliest backers of an audacious idea be rewarded by rule rather than by who negotiated hardest.

That machine is the revnet. The next chapter builds it in one breath.

*Money was the old solvent for the old scarcity. The scarcity moved. It's time the solvent did too.*
