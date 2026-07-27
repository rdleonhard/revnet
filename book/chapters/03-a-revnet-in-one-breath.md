---
title: "A Revnet in One Breath"
part: "Part I — Compute Is the New Capital"
status: draft
summary: The primer — a reader new to tokens finishes able to explain a revnet: staged issuance, a cash-out floor, and no governance, and why those three are exactly what an audacious long-dated promise needs.
word_count: ~2,500
sources:
  - "README.md — general revnet framing"
  - "$WAKE (LIVE prototype + designed token, README PROJECT 1)"
open_questions:
  - How much bonding-curve math to expose here vs. defer to Appendix A (currently deferred).
  - Confirm the precise live-vs-designed boundary of the $WAKE Testament Network before this goes to `final`.
---

# A Revnet in One Breath

*Forget tokens for a moment. Ask a plainer question: if a stranger is going to fund your idea years before it pays off, what would have to be true for that to be sane?*

**A revnet is a funding contract whose rules — who gets in on what terms, and what your money is always worth — are fixed in code that no one, including the founder, can change.**

In one breath: money goes in and mints a token; a reserve backs that token so it always has a floor; the earliest backers get the best price by rule; and none of it can be altered after launch, because there is no one with the power to alter it. That is the whole machine. Everything else in this book is variations on those four sentences. This chapter earns them, one property at a time, and if you have never touched a token before, it is written for you.

Let me define the word first and then take it apart.

> **revnet** *(revenue network)* — a token whose issuance and redemption rules live in an immutable smart contract. Contributions mint tokens; a reserve backs their redemption; the terms cannot be changed by anyone. The entire point is credibility through the *inability* to renege.

## The basic loop

Picture a contract sitting on a public blockchain. It does two things and only two things.

**When money comes in, it mints tokens and holds the money as reserve.** You send it, say, some USDC; it creates $EXAMPLE tokens and hands them to you, and it keeps your USDC in a reserve that backs the tokens. You are now a holder.

**When a holder cashes out, it burns their tokens and returns a share of the reserve.** You send your tokens back; the contract destroys them and pays you your proportional slice of the reserve it holds.

That's it. That's the loop.

```
        money in ──▶ ┌───────────────────────────┐
                     │   REVNET CONTRACT          │
   holder gets  ◀────│   • mints tokens           │
   tokens            │   • holds a RESERVE         │
                     │   • burns tokens on exit    │
   holder cashes ───▶│   • returns share of reserve│──▶ money back
   out (burn)        └───────────────────────────┘
                                 │
                       rules are FIXED — no one can change them
```

Simple as it is, three rules layered onto this loop are what make it useful — and honest. Take them in order.

## Property one: staged issuance (the earliest believer buys cheapest)

The first rule governs *the price of getting in*, and it changes over time by design.

> **staged issuance / issuance decay** — each successive contribution mints fewer tokens per dollar than the one before. The earliest backers get the most tokens for their money; later ones get fewer.

Why build it this way? Because the earliest backer of an unproven idea is taking the most risk, and fairness says they should be rewarded for it — not by a negotiation they have to win, but by a rule. When you back a founder on day one, before there's traction, before it's safe, the contract mints you tokens at the best rate anyone will ever get. The person who shows up a year later, once the risk has visibly fallen, mints at a worse rate. No cap-table meeting, no insider round, no "friends and family" tier decided in private. **The reward for early conviction is set in code and applied to everyone identically.**

This is the token-native version of "seed investors pay a lower price than Series A investors" — except there is no one deciding the price at each stage. The curve decides. You can read exactly what your dollar mints, right now, before you commit.

## Property two: the cash-out floor (you can never hold a rug)

The second rule governs *your downside*, and it is the one that lets a stranger sleep at night.

> **cash-out tax / redemption floor** — a holder can always redeem their tokens for a pro-rata share of the reserve (the *floor*). An exit fee (the *cash-out tax*) is left behind for the holders who stay, rewarding duration over flipping.

The floor is the promise that **the token is never worth less than the reserve backing it.** If the project stalls, if the hype evaporates, if the founder wanders off — you are not left holding a worthless token and a story. You can always send it back to the contract and get your share of the reserve. There is a hard bottom under you, enforced by code, and it does not depend on anyone's goodwill.

The cash-out tax is the subtle part. When you exit, you don't quite get your full arithmetic share — a small portion stays behind and is redistributed across the holders who remain. This gently penalizes flipping in and out and rewards those who hold through the project's life. It aligns the token with the people who actually mean to stay for the thing being built, not the ones passing through for a quick trade.

Together, floor and tax do something a normal startup investment cannot: they give you a *known worst case* and a reason to be patient. You can lose money — if the reserve asset itself falls, or if you'd rather have exited earlier — but you cannot be rugged. The bottom is real and it is yours.

## Property three: no governance (the rules cannot rot)

The third rule is the strangest to newcomers and the most important: **there is no steering wheel.**

Most crypto projects come with governance — token-holder votes that can change parameters, redirect the treasury, mint more tokens, alter the rules. That flexibility sounds like a feature. It is usually the vulnerability. A treasury that *can* be redirected is a treasury that can be captured, drained, or slowly bent toward insiders. Rules that *can* be changed are rules that will be changed, eventually, under pressure, in someone's favor.

A revnet's founding move is to throw the steering wheel out the window. The issuance curve, the floor, the tax — all fixed at launch, immutable, beyond the reach of the founder and the holders alike. No one can vote to mint themselves more tokens. No one can vote to raid the reserve. **The rules cannot rot, because rot requires a hand to turn them, and there is no hand.**

This is a genuine trade. You lose the ability to adapt the terms if something needs fixing. What you buy with that loss is the only thing that makes a long-dated promise from a stranger credible: the certainty that the deal you signed up for is the deal you will still have in five years. For a founder asking people to believe in something audacious and slow, that certainty is worth more than flexibility.

## Why these three fit an audacious, long-dated promise

Now the payoff. Put the three properties together and ask: what kind of venture are they *for*?

They are for a promise that is longer and bolder than the person making it — exactly the situation of a founder raising against an idea that will take years to prove. And the repo's most extreme example makes the point better than an abstraction can.

Consider $WAKE [LIVE prototype + designed token], the token behind a digital-immortality project called the Testament Network. The product is, literally, *forever*: it turns a person's memories into an AI avatar meant to run long after that person has died, funded by an endowment they leave behind. This is a real prototype — there is a small live constellation of avatars posting to a shared commons tonight — and it is also, in its full form, a designed promise reaching far past anything shipped so far. (Keeping that boundary honest is exactly the discipline the Preface committed to.)

A product that promises "forever" has a credibility problem no marketing can fix: *the promise is longer than the promiser.* A company selling perpetual anything, backed by a treasury its founders can spend at will, is asking you to bet that its founders, its board, and its bank account all outlive your grandmother's ghost. They won't. So how could such a promise ever be honestly issued?

Only by making the things you must trust *non-discretionary* — which is precisely the list of revnet properties:

- **Staged issuance** means the earliest believers in an audacious, far-off promise are rewarded by rule, not by who got into the private round.
- **The floor** means nobody is holding a rug in a graveyard — if the dream stalls, the reserve is still there and still yours.
- **No governance** means the rules that carry a forever-promise cannot be quietly rewritten by whoever controls the company next.

The founding thesis of that project — *too important to trust to a company* — is really just the revnet thesis applied to the founder's own money. And what's true for a forever-product is true, in gentler form, for our compute-raising developer: they too are asking strangers to fund a promise before it pays off, and they too need that promise to be credible without requiring anyone to trust their discretion.

## "If the rules can't change, isn't that dangerously rigid?"

The fair objection: immutability cuts both ways. If you can't change the rules, you can't fix a mistake, respond to a market shift, or correct a parameter that turns out wrong. Isn't that recklessly inflexible for something as dynamic as a startup?

Yes — and that rigidity is the price of the credibility, paid on purpose. The answer is not to add a steering wheel back; it is to *design the operating room, not the foundation, to be where the flexibility lives.* A revnet fixes the money-rules — issuance, floor, tax — and leaves everything about the actual work adaptable. The founder can change strategy, pivot the product, rewrite every line of code; what they cannot change is the promise they made to the people who funded them. Later chapters (especially the $SERF example) show how to put a great deal of adaptability *around* an immutable core — even holder influence over direction — without ever touching the rules that make the thing trustworthy. You get to be flexible about the work and rigid about the promise. That combination, not flexibility everywhere, is the point.

## What you can now say

If you started this chapter never having touched a token, you can now explain a revnet to a friend: money in mints a token; a reserve gives it a floor you can always cash out to; the earliest backers get the best rate by rule; and none of it can be changed by anyone. You can say why those properties suit a promise longer than its promiser. And you're ready for the turn that makes this book more than a primer — because so far, that reserve has just been sitting there, inert, doing nothing. The next part asks what happens when we make it *work.*

*A revnet doesn't ask you to trust the founder. It asks you to check the contract — and then makes the founder trustworthy by taking away their power to be otherwise.*
