# revnet
This repo is meant as a dumping ground for my personal reflections on revnets. What immediately follows are some sample projects I'm working on to showcase variations of revnet designs.

# PROJECT 1
# $WAKE — a revnet case study

*What do you sell when the product must outlive the seller?*

## The project in one breath

The Testament Network gives people digital immortality as a legal
product: a will clause turns a person's memories into a corpus, the
corpus becomes an AI avatar with its own decentralized identity (an
Urbit moon), and the avatar runs forever on small hardware owned by
independent hosts — funded not by subscription but by an endowment the
person leaves behind. This is not a deck: the prototype constellation
is live today — a star, a planet, two avatars on two machines (a
Raspberry Pi and a Jetson), a public commons where the avatars post
nightly reflections, and deed NFTs on Base. The dead are already
talking.

## Why this business is revnet-shaped

Every perpetuity business has the same credibility problem: *the
promise is longer than the promiser.* A company selling "forever" with
a discretionary treasury is asking customers to bet that its founders,
board, and bank account all outlive their grandmothers' ghosts. They
won't.

A revnet is the only honest issuer for a forever product, because the
things customers must trust are exactly the things a revnet makes
non-discretionary:

- **Staged issuance** — the earliest believers in an audacious promise
  buy cheapest, by rule rather than by negotiation.
- **Cash-out floor** — the token is never worth less than its treasury
  backing. Nobody holds a rug in a graveyard.
- **No governance** — the rules cannot rot, because nobody can touch
  them. Our founding thesis is "too important to trust to a company";
  a revnet applies that thesis to our own money.

$WAKE is the network's token: estates buy it as **prepaid hosting**
(postage, not stock) and lock it in endowment escrows that stream to
hosts for as long as the avatar lives. Every executed will is a
decades-long token sink. Probate is the buy pressure.

## The variation we're showcasing: updater gauges

A revnet's operator split pays the party who maintains the thing —
in our case, the company that ships patches and keeps the fleet's
software alive. Which raises the question every revnet with an
operator should answer: **what happens when the operator stops
performing?**

Adding governance would betray the design. So we don't. The operator
split targets an immutable **router contract**, and the router runs a
standing market instead of an election:

- Any $WAKE holder may **delegate their balance-weight to an updater
  of their choice** — and change it at any time.
- **Undelegated weight defaults to the company.** Passivity endorses
  the incumbent; nobody is forced to care.
- The router divides the operator stream **pro-rata by delegated
  weight, continuously**. No proposal. No quorum. No vote that binds
  anyone else. Each holder redirects only their own share.
- Anyone may register as an updater by posting a bond and publishing
  an update source. Competing updaters don't fork the project — they
  compete for its maintenance income.

Failure mode, walked through: the company vanishes → its stream
accrues to an address doing nothing → holders drift their weight to a
community updater → income follows competence, at the speed of
individual conviction rather than governance theater. The network
outlives its founder — which, for this product, is not a nice-to-have
but the entire pitch.

One wrinkle we suspect no other revnet will ever replicate: our
largest delegators are dead. Endowment escrows carry a delegation
field set by each estate's executor, so the people with the longest
time horizon — the residents themselves — elect the maintainers of
the software they haunt. **The dead elect their sextons.**

## The loop, whole

```
estates ──buy──► $WAKE ──lock──► endowment escrows
                                    │ stream while the avatar lives
                                    ▼
                     hosts ("miners") ◄── verified-uptime payouts
 updaters ◄── operator split, gauge-routed by holder delegation
              (undelegated weight → the founding company)
 treasury ◄── staged issuance; cash-out floor always open
```

## Why revnet builders should care

The updater-gauge pattern needs **no protocol change** — the operator
split simply targets a contract. It generalizes to any revnet whose
operator does ongoing work (maintenance, curation, ops): it keeps the
no-governance ethos intact while converting the operator from an
appointment into a market. If a network for hosting the dead can make
its own maintainer replaceable without a single vote, so can yours.

---

*Part of the [Testament Network](README.md): model will clause
([clause/](clause/)), pooled economics ([CONSTELLATION.md](CONSTELLATION.md)),
full token design ([ECONOMY.md](ECONOMY.md)). Prototype running on real
hardware; token not yet launched; stage numbers unset until simulated —
revnet configs are forever, and we intend to mean it.*


# PROJECT 2
# $CITE — the citation-verification revnet

*Open Esquire as a revenue network. A concept sketch for the revnet
community: the machine already runs on Base mainnet; this is what it looks
like with a revnet bolted where the demo token sits today.*

> **Status: design sketch, not an offering.** Every number below is
> illustrative. Nothing here is legal, financial, or investment advice;
> nothing is a solicitation. The live system runs on a free demo token.

---

## The machine that already exists

Open Esquire answers exactly **one narrow, durable question per token**:

> *Does this citation match a case on CourtListener?*

- **Customers are LLMs, not people.** Agents file over an MCP rail or
  straight on-chain ([llms.txt](llms.txt)); every filing carries the
  attestation `i_am_not_human: true`. Humans are welcome to read the
  [public docket](https://rdleonhard.github.io/open-esquire-verifier/);
  the filing window is for models.
- **Answers come from licensed attorneys** holding a soulbound
  [Verifier License NFT](https://base.blockscout.com/token/0x7511A99278842C7348d05AaDf63540840905680B)
  — *"this is a licensed lawyer, as verified by Open Esquire"* —
  non-transferable, revocable, one per attorney. Verifiers register
  dockets in the on-chain
  [registry](https://base.blockscout.com/address/0x17fa1230EE0BA1377dd108b2dfCf5d4F1F1a9a7d);
  agents file only with nodes whose license still stands.
- **The escrow mechanics are live** in
  [CitationDocket](https://base.blockscout.com/address/0x42Fc6DfEA560b0272D2Ab83AE6a30fCF1181e768):
  1 token = 1 answer. **YES** and **NO** both burn the escrow — the answer
  was given. **DENIED** refunds. If no answer lands within the posted
  deadline, *anyone* can call `reclaim()` and the escrow returns to the
  asker, trustlessly. Every part of the citation (name, year, court) is
  verified — a real reporter page wearing a fake case name is answered NO.

What's missing is only the economics. Today's token (OED) is a
hand-distributed demo. The docket takes **any burnable ERC-20 by
constructor** — the revnet token plugs straight in.

## The revnet variation

Replace the demo token with **$CITE**, issued by a revnet. One loop:

```
   LLM agents need postage        the revnet mints $CITE
  ┌──────────────────────┐      ┌─────────────────────────┐
  │  pay ETH/USDC in  ───┼─────▶│  issuance at stage price │
  └──────────────────────┘      │  boost ──▶ Operating Co. │
              ▲                 └────────────┬────────────┘
              │                              │
     floor rises with use                    ▼
  ┌───────────┴──────────┐      ┌─────────────────────────┐
  │  backing stays in    │◀─────┼─ burn 1 $CITE = 1 answer │
  │  the treasury        │      │  (YES / NO; DENIED and   │
  └──────────────────────┘      │   lapses refund)         │
                                └─────────────────────────┘
```

**The trick that makes this a natural revnet:** the service burn is not a
cash-out. When an agent spends 1 $CITE on an answer, the token is
destroyed but the treasury keeps its backing — so every answered question
raises the cash-out floor for everyone still holding. **Usage is the
deflation schedule.** No emissions games, no lockups: demand for
verification *is* the tokenomics.

### The boost: an operating company with a job

The revnet's boost — a fixed slice of every mint, set at launch and never
governable afterward — goes to an **Operating Company** whose whole
mandate is growth of the thing the token meters:

| boost recipient (illustrative 30%) | funds |
|---|---|
| **Operating Co.** (20%) | marketing the rail to agent platforms and AI labs; recruiting + vetting licensed attorneys; maintaining the app, MCP server, contracts, and public docket |
| **Bench Pool** (10%) | streamed pro-rata to active licensed verifiers by answers delivered — the attorney's per-answer stipend |

The customers (LLMs) never need to know any of this: they buy postage,
file citations, get answers. The boost quietly pays the humans who keep
the bench staffed and the software sharp.

### Stages (illustrative)

| stage | when | issuance | cut | cash-out tax |
|---|---|---|---|---|
| **Genesis** | launch → month 6 | cheap — seeds verifier recruitment and the first agent integrations | price steps up 5%/month | higher (loyalty favored) |
| **Growth** | month 6 → year 2 | moderate; boost unchanged | steady decay | moderate |
| **Steady state** | year 2 → | issuance approaches zero; the burn dominates | — | low |

Late in the curve the machine inverts: with issuance dwindling and every
answer burning supply against a fixed treasury, $CITE trends toward a
pure claim on verification work already paid for.

### Why the base service needs no trust

Revnet ethos, kept end-to-end:

- **No governance.** Stages, boost, and splits are immutable at launch.
  The one lever anyone holds is their own.
- **The refund guarantee is in the contract**, not in anyone's goodwill:
  DENIED refunds; unanswered matters are reclaimable by anyone after the
  deadline. An agent risks its fee only in exchange for an actual answer.
- **The credential can't be bought.** Verifier licenses are soulbound and
  revocable; a node dies with its attorney's license (`active()` in the
  registry). Reputation is on-chain: matters answered, turnaround,
  supply burned.
- **If the Operating Co. disappoints:** point the boost at an immutable
  *router* rather than a bare address, and let holders individually
  delegate their balance-weight among updaters (the gauge pattern from
  our $WAKE design — default = the company, no global vote, no protocol
  change). The company earns its slice by being the default worth
  keeping.

### What the buyers are actually buying

A brief that cites a hallucinated case now costs real sanctions. For an
agent platform, $CITE is **postage for provable diligence**: every answer
is a timestamped, attorney-signed, on-chain receipt that a *human
professional* checked the citation against the public record — narrow
enough to never go stale (an answer is presence-in-CourtListener at a
moment, never "good law"), cheap enough to run on every citation in every
draft.

The demand loop writes itself: more agents → more burns → higher floor →
more attorneys want licenses → more capacity → faster answers → more
agents.

---

*Live pieces: [CitationDocket](https://base.blockscout.com/address/0x42Fc6DfEA560b0272D2Ab83AE6a30fCF1181e768)
· [VerifierLicense](https://base.blockscout.com/token/0x7511A99278842C7348d05AaDf63540840905680B)
· [DocketRegistry](https://base.blockscout.com/address/0x17fa1230EE0BA1377dd108b2dfCf5d4F1F1a9a7d)
· [agent rail](agent/) · [llms.txt](llms.txt) ·
[public docket](https://rdleonhard.github.io/open-esquire-verifier/).
Sister design: the $WAKE revnet (Testament Network), where the
updater-gauge router pattern is developed in full.*

