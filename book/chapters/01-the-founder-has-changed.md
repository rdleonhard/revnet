---
title: "The Founder Has Changed"
part: "Part I — Compute Is the New Capital"
status: draft
summary: The protagonist of the book is the solo open-source dev with an idea and an API bill; the old capital stack is mis-sized for them, and the natural thing to raise is compute.
word_count: ~2,150
sources: ["$SERF (HYPOTHETICAL, README PROJECT 3)"]
open_questions:
  - Whether to anchor the cost comparison to a real, sourced seed-budget breakdown or keep it explicitly illustrative (currently illustrative).
  - Whether to add a named practitioner anecdote or keep the protagonist archetypal.
---

# The Founder Has Changed

*Picture the founder a seed round was invented to fund. Now picture who actually shows up to build things today. They are not the same person.*

**The unit of ambition used to be a team; now it is a person with an idea and an inference budget — and almost everything about how we fund ambition is still built for the team.**

In one breath: the seed round — the checks, the pitch decks, the board seats, the eighteen-month runway — is a machine for buying *labor you cannot yet afford*. It exists because turning an idea into working software used to require hiring five or ten people and paying them for a year before you learned whether the idea was any good. That was the bottleneck, and money was the thing that cleared it. Money bought engineers; engineers bought a shot at the idea.

That machine is now pointed at a founder who no longer exists in the numbers it assumes.

## The new protagonist

The founder this book is about is a single open-source developer. They have an idea that is genuinely good and genuinely hard, the kind that would have needed a team in 2015. They have a GitHub account with real work in it. What they do *not* have is a reason to hire five people, because the leverage that used to come from headcount now comes from models. One developer with frontier-model access can produce, in a week, what a small team produced in a quarter — not in every domain, not perfectly, but often enough that the economics have already tipped.

So what does this person actually need on day one? Not an office. Not a recruiter. Not a VP of Engineering. They need two things:

1. **The right to run a lot of inference** — because the product itself is model calls, and building it is model calls, and both are metered.
2. **A little runway** — enough that they can point their own hours at the idea instead of at a job.

Notice what is missing from that list: the single largest line item in a traditional seed budget. Salaries for people who are not the founder. When you remove it, the shape of what you need to raise changes so much that the instrument you raise it with should probably change too.

## Where the seed dollar used to go

Let me make this concrete, and let me be honest that the numbers are illustrative — a composite of how early budgets have historically broken down, not a citation. [The point is the *shape*, not the decimals.]

A conventional pre-seed / seed raise of, say, **$1,500,000** for an eighteen-month runway went roughly like this:

```
   OLD SEED DOLLAR (~$1.5M, 18 months)
   ┌──────────────────────────────────────────────┐
   │ engineering salaries (5 × ~$180k/yr) ~$900k   │ ██████████████████  ~60%
   │ founder salaries                     ~$250k   │ █████               ~17%
   │ office / ops / legal / misc          ~$200k   │ ████                ~13%
   │ software, cloud, infra               ~$100k   │ ██                  ~7%
   │ everything the *idea* needed         ~$50k    │ █                   ~3%
   └──────────────────────────────────────────────┘
   Roughly 94 cents of every dollar bought people and the rooms to hold them.
```

The idea — the actual novel thing — got the scraps, because the overwhelming cost was the human capacity to build it. That is not a criticism of anyone; it was simply the price of turning thought into software.

Now run the same idea through the new founder:

```
   NEW COMPUTE BUDGET (~$80k, 12 months)
   ┌──────────────────────────────────────────────┐
   │ inference to BUILD + RUN the product ~$60k    │ ████████████████    ~75%
   │ minimal founder runway               ~$18k    │ █████               ~22%
   │ everything else                      ~$2k     │ █                   ~3%
   └──────────────────────────────────────────────┘
   Roughly 75 cents of every dollar is compute — the variable cost of the product itself.
```

Two things jump out. First, the total is smaller by more than an order of magnitude, because the expensive thing — a team — is gone. Second, and more importantly, **the dominant cost is no longer labor; it is compute.** The new founder's biggest expense and the product's cost of goods are the same line. That single fact will drive the entire rest of this book, because it means the most natural thing to raise, hold in reserve, and eventually repay in is not dollars at all. It is inference.

## Open source changes who is allowed to believe in you

There is a second shift, quieter but just as important, and it is about *trust*.

A traditional seed investor is buying a promise from behind a curtain. The code is private, the metrics are self-reported, and the diligence is a series of conversations. The whole apparatus of term sheets and board seats exists partly to manage the fact that the investor cannot actually see the work.

The open-source developer has no curtain. The repository is public. The commit history is public. The issues, the tests passing or failing, the cadence of shipping — all public, all verifiable by anyone, without permission. This changes who is capable of backing them: not just accredited investors with access to the private room, but anyone who can read a repo and judge whether the work is real. The believer can verify before they believe.

That is a precondition for a very different kind of fundraising — one where the crowd of people who can sensibly back you is large, technically literate, and able to check your work continuously rather than trusting a quarterly update. Hold that thought. It is the soil the rest of the book grows in.

## "Isn't this just indie hacking with a new coat of paint?"

Here is the objection I would raise if I were you: solo developers building on a shoestring is not new. Indie hackers, bootstrappers, and one-person software businesses have existed for decades. What exactly has changed besides the marketing?

Two things, and they are structural, not cosmetic.

First, **the ceiling moved.** The old solo developer was capped at what one person could build by hand, which kept them to small tools and side projects. The new one, with models as leverage, can credibly attempt things that genuinely required a team — which means the *ambition* has scaled up to meet ideas that actually warrant outside capital, while the *headcount* has stayed at one. That gap — big idea, no team — is new, and it is precisely the gap old instruments handle badly.

Second, **the cost became fundable in kind.** An indie hacker's costs were mostly their own foregone salary — an unfundable, invisible thing. The new founder's costs are mostly inference — a *metered, externally-priced, purchasable* thing. You cannot easily raise "my time," but you can absolutely raise "compute." The cost shifting from invisible sweat to visible, denominated compute is what makes this founder fundable at all in a structured way.

So no — this is not indie hacking with a new name. It is the first time the solo builder's ambition and the solo builder's costs have *both* become large enough and legible enough to warrant, and to fit, a real funding primitive.

## What this founder should raise

If the need is compute, and the product's cost of goods is compute, and the believers who back you can verify your work in public — then the awkward move is to convert all of that into dollars, hand over equity, and re-buy the compute later at retail. The natural move is to raise the compute directly, from the people who can already see what you are building, on terms fixed in advance so no one has to trust anyone's discretion.

That instrument exists. It is called a revnet, and the next chapter builds it from zero. By the end of the book, we will have a version of it whose treasury is not idle dollars waiting to be spent, but staked compute that *produces the very inference the product runs on* — a founder raising, reserving, and repaying in the same substance the product is made of. Our recurring [HYPOTHETICAL] example, the developer who funds himself and hires an AI to hold him accountable ($SERF), is the first place we will watch it happen.

The founder changed. The funding hasn't caught up yet. This book is about closing that gap.

*The old founder raised money to buy a team. The new one raises compute to skip having one.*
