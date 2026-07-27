---
title: "The Cast: Dev, Marketer, Holders, Future Buyers, and the AI Boss"
part: "Part II — The Mechanics"
status: draft
summary: One productive treasury serves several roles at once, each drawing from a different layer — and the AI boss ($SERF) is a genuinely new role: accountability without a human manager.
word_count: ~2,200
sources:
  - "revnet-in-venice.md (PROPOSAL) §6"
  - "$SERF (HYPOTHETICAL, README PROJECT 3) — the boss/agent role"
open_questions: []
---

# The Cast: Dev, Marketer, Holders, Future Buyers, and the AI Boss

*A treasury with three streams is a stage with three spotlights. The question is who stands in each — and whether anyone gets shortchanged so someone else can be paid.*

**Because principal, emission yield, and Diem are separate layers, several roles can be paid from the same treasury at once without cannibalizing each other — and one of those roles has no human in it.**

In one breath: the developer lives on Diem, the marketer lives on the split, the holders keep the principal, the future buyer inherits a ratcheted floor, and — the genuinely new character — an AI agent stands in as the boss who keeps everyone honest. The mechanism from Chapter 6 was plumbing. This chapter is the people the plumbing serves. The reason they don't fight over the pot is that, structurally, **each draws from a different layer**, so paying one doesn't drain another.

## Why the roles don't collide

Start with the thing that makes the cast possible at all. In an inert-reserve revnet there is one pot, so every role is rivalrous: money paid to a marketer is money not backing the floor, is money not funding the dev. Everyone is fighting over a single pile, and the founder is forever robbing Peter to pay Paul.

The productive reserve breaks the rivalry by having *different money for different jobs.* Principal is one substance (the staked VVV floor), emission yield is a second (the ~14% VVV stream), Diem is a third (the perpetual inference). Because they are genuinely distinct outputs of one asset, you can hand each to a different person and none of them is reaching into anyone else's share.

| Role | Draws from | What they get | What they bear |
|---|---|---|---|
| **The developer** | Diem (inference stream) | Perpetual compute to build and run the product | Delivery risk — must actually ship |
| **The marketer** | Emission yield (the split) | A VVV income stream for growth work | Paid from yield, so paid only while yield flows |
| **The holders** | Principal (the floor) | A redeemable pro-rata VVV claim | VVV market risk — the floor is VVV-denominated |
| **The future buyer** | The ratchet | Entry against a floor grown by compounded yield | Buys higher than early backers did (by rule) |
| **The AI boss** | A metered sliver of yield | Compute to run its own oversight | Nothing — it's an agent, not a claimant |

Read down the "draws from" column: five roles, and no two of them pulling from the same layer for their primary claim. That non-overlap is the whole trick. It's what lets one founder credibly promise a developer their compute, a marketer their salary, and holders their floor, all in the same breath, without any of those promises being secretly funded by breaking another.

## The developer lives on Diem

The founder-developer's need, established all the way back in Chapter 1, is inference — to build the product and to run it. The treasury's Diem stream is exactly that: a perpetual $1/day-per-unit inference budget, pointed at the developer's live application. They don't receive dollars and go shopping for compute; they receive compute. Their product's cost of goods is served in kind by the reserve that backs the token.

This is the cleanest expression of "raise compute, not money." The developer is paid in the substance they consume, from a reserve denominated in that substance, and the payment never touches the floor. If they need more, the lever is to lock more of the reserve's sVVV into Diem — trading a slice of emission yield (they keep 80% of it, remember) for more standing inference. The developer's compensation and the product's fuel are the same pipe.

## The marketer lives on the split

A product still has to be found. Someone does growth, distribution, the unglamorous work of getting the thing in front of people. That's the marketer, and they're paid from the **emission yield** — the split.

The important property is what funds them: not principal, not new-buyer money, but the reserve's own ~14% VVV emissions. The marketer's salary is covered by money the treasury *earned*, so paying it lowers no one's floor and imports no ponzi shape. And because the split is drawn from yield, it is naturally self-limiting — if emissions fall, the split has to throttle before it can ever reach into principal. (Making that throttle a hard rule, a coverage ratio that keeps committed payouts below realized yield, is one of Chapter 13's mitigations.) The marketer is a real beneficiary with a real income, structurally prevented from being paid out of the holders' safety.

## The holders keep the principal — and can always leave

The backers who funded the raise hold the token, and their claim is the **principal**: a pro-rata, redeemable share of the staked VVV, denominated in VVV, exitable at any time (after the 7-day cooldown). Their upside is the ratchet — if yield compounds into the reserve, their floor rises. Their downside is honest and singular: **VVV market risk.** The floor guarantees their *share of the VVV*, not a dollar price, so if VVV falls they can redeem for fewer dollars than they put in.

That is the "take the loss and take back your VVV" shape the proposal names. It is not a bug hidden in the model; it is the model's honesty. Holders are never rugged and never diluted, but they are exposed to the reserve asset, knowingly, in a form they can read at any moment. The floor protects them from the founder; it does not protect them from the market, and it doesn't pretend to.

## The future buyer inherits a ratcheted floor

The person who buys in a year from now is a holder-to-be, and they enter on the same immutable terms as everyone — except the floor they buy against has grown. If the project compounded its emission yield, reserve-per-token is higher, so the future buyer pays more per token than the early backer did. This is staged issuance's fairness, extended by the productive reserve: **early conviction is rewarded not only by a better mint rate but by a floor that rose while they held.** The future buyer isn't cheated by paying more; they're buying a token with more VVV behind it, into a project that has proven a year of yield. They take less risk and pay a fairer, higher price — by rule, the same rule, applied to them as to everyone.

## The new character: an AI as the boss

Here is the role with no precedent, and it's why the repo's [HYPOTHETICAL] example $SERF exists.

Every prior role is a claimant — a human drawing from a layer. The boss is not a claimant. It is an **AI agent** the founder hires to hold *themselves* accountable to the people who funded them. In $SERF, a developer raises his runway, points the split at himself, and — instead of promising backers he'll work hard — publishes a *sworn schedule* and stands up an agent whose recurring job is to check his real progress against that schedule and report to the token holders. Performance reviews, on chain, that the developer cannot edit.

Notice what this solves. A solo founder paying themselves from a treasury is the textbook principal-agent problem: who watches the person who holds the money and does the work and writes the updates? The old answer was a board — humans with the time, incentive, and authority to supervise. A solo open-source dev raising compute has no board and can't afford one. The AI boss is the board, reduced to an agent: cheap enough to run on a sliver of yield, tireless enough to check every week, and — crucially — *structurally unable to be leaned on*, because its rails are code. The founder built their own supervisor and handed the dials to their backers.

And that last part is the twist that makes it fit a revnet rather than break it. Token holders don't get to seize the wheel of the immutable money-rules — Chapter 4 forbade that, on purpose. But they *can* lobby the boss: vote to make it stricter, change how often it reports, steer what it asks the developer to prioritize next. **All the adaptability lives in the soft layer around the immutable core** — exactly the "flexible about the work, rigid about the promise" split Chapter 4 promised. The holders influence direction without ever touching the terms. The boss is where that influence lands.

## "This is a lot of roles for a one-person startup"

The fair objection: the whole premise was a *solo* developer, and now there's a cast of five. Isn't this just a startup with extra steps and a crypto costume?

No — because four of the five roles are *funded automatically by the mechanism*, not staffed by hires. The developer is the founder. The "marketer" may be a bounty, a part-time contributor, or future-them; the split just exists as a fundable slot whether or not it's filled today. Holders and future buyers aren't employees at all. And the boss is software. The cast isn't five people the founder has to recruit and manage — it's five *positions the treasury can pay*, most of them without a headcount. That's the point of building the roles into the layers: the solo founder stays solo, while the structure around them does the work a team and a board used to do. The extra steps replace extra people. That was the trade the whole book is about.

*One treasury, five roles, and only one of them a human who has to be hired. The developer builds; the reserve pays everyone else — including the machine that keeps the developer honest.*
