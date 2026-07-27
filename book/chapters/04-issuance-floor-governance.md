---
title: "Staged Issuance, the Floor, and No Governance"
part: "Part II — The Mechanics"
status: draft
summary: Deepens the three revnet properties from primer to mechanism design — why each is incentive-compatible, what breaks without it, and how immutability reads to a centralized company, not just a DAO.
word_count: ~2,600
sources:
  - "README.md — general revnet framing"
  - "$CITE (HYPOTHETICAL, README PROJECT 2)"
open_questions:
  - "$CITE is the thinnest source doc; this chapter carries more original argument as a result. Consider expanding the README $CITE section."
---

# Staged Issuance, the Floor, and No Governance

*Chapter 3 gave you the three properties as promises. This chapter asks the harder question a builder actually cares about: are they promises the math will keep?*

**A revnet's three rules aren't features bolted on for marketing — each one closes a specific way that funding a stranger's idea normally goes wrong, and you can see the failure it prevents by imagining it removed.**

In one breath: staged issuance prevents the insider land-grab; the floor prevents the rug; no-governance prevents the slow capture. Take any one away and a predictable exploit walks back in. The best way to understand why these three, in this combination, is to break them on purpose and watch what happens.

## Staged issuance, as a mechanism

Recall the rule: each contribution mints fewer tokens per dollar than the last, so early backers get more tokens for their money. In the primer that was a fairness story. As mechanism design, it is something sharper — it is a **rules-based cap table that cannot be gamed by timing or access.**

Here is the curve, drawn crudely. The horizontal axis is cumulative money contributed over the project's life; the vertical axis is how many tokens a fixed contribution — say $1,000 — mints at that point.

```
   tokens minted per $1,000 contributed
   ^
   │██
   │███
   │ ████            issuance DECAYS as more capital arrives:
   │  ██████         the earlier you back the idea, the more
   │    █████████    tokens your dollar mints — by rule, not
   │       █████████████        by negotiation
   │            ████████████████████
   └────────────────────────────────────────▶ cumulative contributions
     day one                          later
```

Now remove the rule — make issuance flat, everyone mints at the same rate regardless of when they show up. What breaks? The reward for early risk vanishes. The person who backed the idea when it was dangerous gets exactly the same deal as the person who waited until it was safe. Rational backers respond by *all waiting* — why take day-one risk for no premium? The result is a project that can't bootstrap, because the incentive to be early has been zeroed out.

Now instead make issuance *discretionary* — the founder hands out favorable rates to whomever they choose. What breaks? You've reinvented the private round, the insider allocation, the friends-and-family tier — the exact opacity a revnet exists to abolish. Whoever is close to the founder wins; everyone else takes worse terms decided in a room they weren't in.

Staged issuance threads between these. **The premium for being early is real (so bootstrapping works) but it is set by a public curve (so no one can be favored).** You can read, before committing a dollar, exactly what that dollar mints right now and exactly how that rate will decay for those who follow. The cap table is a function, and the function is visible to everyone.

## The floor, as a mechanism

The rule: a holder can always redeem for a pro-rata share of the reserve, minus a small exit tax left to remaining holders. In the primer this was "you can never hold a rug." As mechanism, it is a **hard lower bound on the token price, enforced without anyone's cooperation.**

This matters more than it first appears, because of what it does to *behavior* in a panic. In an ordinary token with no floor, bad news triggers a race: everyone rushes to sell before the price falls further, and the rush itself is what makes the price fall — a self-fulfilling collapse. The floor defuses the race. If you know you can always redeem for your share of the reserve, there is no point trampling anyone on the way out; the bottom isn't going anywhere. The floor doesn't just protect the individual holder — **it removes the mechanism by which token panics feed themselves.**

The exit tax adds a second-order effect. Because a slice of every redemption stays behind and is redistributed to those who remain, the floor per token actually *rises* slightly each time someone leaves. Holders who stay are compensated by the departures of holders who go. This quietly sorts the cap table over time toward people who mean to stay for the thing being built — and it is the same lever, we'll see later, that can defend against faster forms of extraction like front-running.

What the floor does *not* do — and honesty demands saying it here, not later — is protect you from the reserve asset itself losing value. If the reserve is USDC, the floor is stable. If the reserve is a volatile token, the floor is denominated in that token and moves with it. The floor guarantees you your *share*, not a *price in dollars*. Hold that distinction; Part II's later chapters and all of Part IV turn on it.

## No governance, as a mechanism

The rule: the issuance curve, the floor, and the tax are fixed at launch and cannot be changed by anyone — not holders, not the founder. In the primer this was "the rules can't rot." As mechanism, it is the deliberate *destruction of a control surface* — and the reason is that a control surface is exactly what an attacker needs.

Walk the attack. A revnet accumulates a real reserve. If there existed a governance vote that could redirect that reserve, then the reserve is only as safe as the vote — and votes can be bought. An attacker accumulates tokens, reaches a threshold, and passes a proposal to drain the treasury to themselves. This is not hypothetical paranoia; governance-token treasuries have been captured this way. The vulnerability is structural: *a treasury that can be moved by a decision can be moved by whoever captures the decision.*

No-governance removes the surface entirely. There is no proposal that can mint new tokens, no vote that can touch the reserve, no parameter anyone can turn. The attacker who buys up tokens finds there is nothing to seize the wheel *of.* You cannot capture a machine that has no controls.

The cost, restated plainly because it is real: you also cannot *fix* anything. A parameter set wrong at launch is wrong forever. This is why the founder's pre-launch design work is the whole ballgame — there is no patch. The discipline this forces (get it right the first time, because there is no second) is unusual and uncomfortable, and it is the price of the credibility.

## Where the flexibility actually lives

If the rules can't change, how does anything adapt? The answer — developed fully in the $SERF chapter — is that **immutability is applied to the money, not the work.** The contract fixes issuance, floor, and tax. It says nothing about what the founder builds, how they pivot, what the roadmap is, or even how token holders might *influence* direction. All of that lives in a soft layer wrapped around the immutable core. You get a rigid promise and a flexible product, which is precisely the combination a long-dated bet needs: certainty about the terms, freedom about the execution.

## Immutability reads differently to a company than to a DAO

One more move, because it's the one most people miss. The instinct is that revnets are a crypto-native, DAO-shaped thing — for leaderless collectives, not for normal companies. The repo's [HYPOTHETICAL] example $CITE exists to break that instinct.

$CITE imagines a *centralized* company — a real firm, with a CEO, a bank account, and employees — choosing to raise through a revnet anyway. Why would it? Precisely *because* it is centralized. A centralized company's core credibility problem is the mirror image of a DAO's: everyone knows a company *can* change the deal, spend the treasury, and act in its own interest, because a company is exactly the kind of entity that has the power to do so. When such a company tells backers "your terms are safe with us," the backers have every reason to doubt it.

By issuing through an immutable revnet, the centralized company does something it otherwise cannot: it *ties its own hands in public.* It converts "trust us" into "you don't have to." The rules the company most wants backers to believe — your rate is fair, your floor is real, we can't dilute you — become things the company is provably unable to violate, because it handed away the ability to. For a centralized issuer, no-governance isn't a philosophy; it's a way to borrow credibility it couldn't generate on its own.

```
   DAO's problem:    "no one is in charge — can I trust the collective?"
   Company's problem:"someone IS in charge — and they can change the deal on me"

   Revnet's answer to BOTH: the deal is in immutable code.
   → the DAO gets rules that can't be captured
   → the company gets to prove it won't abuse power it visibly gave up
```

So the three properties are not a DAO aesthetic. They are a general-purpose way to make a promise credible when the promiser — collective *or* company — would otherwise be trusted at their word and shouldn't be.

## "Fine for money — but my project needs to evolve its terms"

The objection a thoughtful founder raises here: "My situation will change. Locking my economic terms forever is a straitjacket. Surely *some* adaptability in the terms is prudent." 

The reply is that this confuses two things that should never be merged: the *terms of the promise* and the *conduct of the work.* Every adaptation a founder actually needs — new strategy, new features, new markets, new ways to involve their backers — lives in the conduct of the work, which a revnet leaves completely free. The one thing you're asking to keep adjustable is the terms of the promise, and that is the one thing whose adjustability destroys its value. A promise you can revise is not a promise; it is an intention. Backers fund the former and are wary of the latter. If you find yourself wanting a lever to change the deal later, that wanting is the exact instinct the no-governance rule exists to bind — including binding it against *you*, on your best-intentioned day.

## What Part II does next

You now hold the three properties not as slogans but as mechanisms, each understood by the failure it prevents. But notice that everything so far has treated the reserve as a passive thing — a pile that sits there, backs the floor, and does nothing else. That passivity has been the unquestioned assumption under every revnet ever built.

The next chapter questions it. What if the reserve didn't sit there? What if it *worked* — and, for our compute-raising founder, worked by producing the very inference the product runs on? That question is the turn the whole book has been walking toward.

*Immutability isn't rigidity for its own sake. It's the founder proving a promise by making themselves incapable of breaking it — and that proof is worth more than the flexibility it costs.*
