# revnet
This repo is meant as a dumping ground for my personal reflections on revnets. What immediately follows are some sample projects I'm working on to showcase variations of revnet designs. *Do not under any circumstances consider this document as giving legal advice and/or approval.*

# PROJECT 1
# $WAKE — an "opt-out" revnet

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
# $CITE — the centralized company revnet

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

# PROJECT 3
# $SERF — *The Developer Who Built His Own Boss / AI & Token Holders Determine if Dev Gets the Split*

---

## The one-line pitch

An open-source developer needs **$5,000 in frontier-model credits** to build his idea. Instead of a grant application or a VC, he deploys a revnet, points the reward split at himself, publishes a **sworn schedule**, and then does the strange part: he hires an **AI agent to be his boss**. The agent holds him to the schedule, files progress reports to token holders, and delivers performance reviews. Token holders don't manage the developer directly — they **lobby the boss**. $SERF is a company where the worker funds the company, the machine runs the worker, and the crowd runs the machine.

The name is the joke and the thesis: he is the serf, and he built the lord (Jango hates this idea, btw, lol).

---
## Why this variation exists

Every prior revnet we've designed pointed the reward split at *a thing being produced* — a docket, a testament, a citation oracle. $SERF points the split at **a person's labor**, and inserts an autonomous manager between the labor and the capital. It's the first of our designs where:

- the **beneficiary and the worker are the same wallet** (no principal-agent gap on the money), and
- the **agent's authority is a governable parameter**, not fixed code.

That combination is the whole experiment: *what happens to accountability when the boss is a smart contract's favorite LLM, tunable by the people who paid for the work?*

---

## Cast of characters

| Role | Who | What they can do |
|---|---|---|
| **The Serf** | The open-source dev (`serf.eth`) | Ships code, receives the split, submits evidence to the boss. Cannot edit his own reviews. |
| **The Boss** | An LLM agent (`overseer.eth`, funded from a tiny slice of the revnet) | Runs the recurring check-in, compares reality to the schedule, writes reports and reviews, sets the *next* milestone. |
| **The Court** | $SERF holders | Fund the treasury; vote on **directives** that steer the Boss (not the Serf). |
| **The Ledger** | The revnet + a public "Chronicle" feed | Immutable record of pledges, schedule, reports, reviews, and votes. |

---

## The revnet mechanics (the familiar spine)

Standard revnet skeleton, tuned for a single-beneficiary labor grant.

- **Token:** `$SERF`, minted on contribution. Same issuance-with-decay curve as prior designs.
- **Funding target:** **$5,000** denominated in whatever the model provider bills (call it the *credit-equivalent*). The revnet doesn't hold API keys — it holds ETH/USDC and disburses to the Serf, who buys credits and posts receipts.
- **The Split:** by default **100% of the reward split → `serf.eth`**, minus a metered trickle to `overseer.eth` to pay for the Boss's own inference (the boss's salary is a rounding error, and pointedly so).
- **Issuance decay & redemption:** unchanged from the base revnet — early backers get a better mint rate; the cash-out tax rewards holders who stay through the schedule rather than dumping after the first good report.
- **No new tokenomics invention here.** The novelty is entirely in the *governance surface*, section 6.

**Design note:** the Serf gets paid on a **drip tied to milestones**, not a lump sum. The revnet holds the $5k; the Boss's report unlocks each tranche. Money and judgment are welded together — this is what makes the Boss more than theater.

---

## The Sworn Schedule

At deploy time the Serf commits an on-chain (or content-addressed + hash-anchored) **Schedule** — his own performance contract. Example for a 6-week, $5k build:

| Milestone | Due | Tranche | Evidence the Boss expects |
|---|---|---|---|
| M0 — Repo + spec + first commit | Day 3 | $250 | public repo, SPEC.md, green CI |
| M1 — Core loop working | Week 2 | $1,000 | demo video/log, passing e2e test |
| M2 — Feature-complete alpha | Week 4 | $1,750 | tagged release, changelog |
| M3 — Docs + one real user | Week 5 | $1,000 | user testimonial, install works clean |
| M4 — 1.0 ship | Week 6 | $1,000 | release, retro, credit receipts reconciled |

The schedule is **the contract the Boss enforces**. The Serf wrote his own rope. Changing it after deploy requires a Court vote (section 6) — he can't quietly move his own deadlines.

---

## The Boss — recurring task spec

The Boss is a scheduled agent. Its job description is public and versioned.

**Cadence:** runs every N days (default 3; Court-tunable). On each run:

1. **Gather** — pull the repo (commits, CI, releases, issues closed), the Serf's submitted evidence, and the credit-spend receipts.
2. **Compare** — measure observed progress against the Schedule. Compute a simple state per milestone: `ahead | on-track | slipping | breached`.
3. **Report** — write a **Progress Report** to the Chronicle: what shipped, what's late, burn rate of the $5k vs. work delivered.
4. **Judge** — at milestone boundaries, issue a **Performance Review** with a grade and a release/withhold/partial decision on the tranche.
5. **Steer** — propose the **Next Objective**: given progress + standing Court directives, what should the Serf do next. This is where holder lobbying lands.

**Tone knobs** (governable): `supportive ↔ demanding`, report `verbosity`, review `strictness`. The same underlying facts can be delivered as a gentle mentor or a merciless VP of Engineering — and the Court decides which.

**Hard rails (not governable):**

- The Boss cannot invent evidence; every claim in a report must cite a fetched artifact.
- The Boss cannot release a tranche whose evidence it couldn't verify.
- The Boss cannot alter the Schedule — only the Court can.
- The Serf cannot edit, delete, or pre-approve a report. He can **respond** (an appended rebuttal), nothing more.

---

## The governance surface — *lobbying the boss*

This is the heart of the variation. Holders **never command the Serf**. They **persuade the Boss.** Voting weight = $SERF held.

Directive types the Court can pass:

**A. Steering directives (where to go next)**
> "Prioritize the plugin API over the GUI." / "Stop gold-plating M2 — ship and move on." / "Add a security review milestone before 1.0."

The Boss folds passed directives into its **Next Objective** and weights them in future reviews.

**B. Cadence & intensity directives (how the boss behaves)**
> "Report weekly, not every 3 days." / "Turn strictness up — he's coasting." / "Ease off; he shipped M1 early, give him room."

**C. Schedule amendments (the only lever that touches the contract)**
> "Extend M3 by 4 days — the real user found a real bug." / "Cut M3 entirely, fold into M4."

Highest quorum of all directive types, because this moves the Serf's own goalposts.

**D. The Vote of No Confidence (the endgame lever)**
If the Court loses faith, a supermajority can instruct the Boss to **freeze remaining tranches** and open **redemption** — holders cash out the unspent treasury at the revnet's redemption rate. The Serf keeps what he earned to date; the crowd recovers the rest. No lawsuit, no clawback drama — the schedule and the ledger already agreed on the math.

**Directive log** is public and permanent. So is every directive the Court *rejected* — you can read the pressure the Serf worked under.

---

## The loop, in one picture

```
   $SERF holders (The Court)
        │  directives (steer / cadence / amend / no-confidence)
        ▼
   Overseer LLM (The Boss) ──every 3 days──▶ Progress Report
        │  compares repo+receipts to Sworn Schedule        │
        │  Performance Review + tranche decision           ▼
        ▼                                              The Chronicle
   release / withhold / partial                     (public feed)
        │                                                  ▲
        ▼                                                  │ rebuttal
   revnet treasury ──drip──▶ serf.eth ──▶ buys LLM credits ─┘
        │                                                  │
        └───────── ships code ◀── The Serf ───────────────┘
```

The worker funds the firm (via the revnet backers), the machine grades the worker, the crowd tunes the machine. A closed accountability loop with no human boss anywhere in it.

---

## What each party is actually buying

- **The Serf** buys *credibility-as-a-service*. "I don't just promise to ship — I hired an incorruptible manager to prove I did, and you can turn the screws on it yourself." That's a stronger fundraising pitch than a roadmap nobody can enforce.
- **A backer** buys *governed exposure to one dev's labor* — with a real off-ramp (no-confidence + redemption) that a Kickstarter pledge never had.
- **The public** gets an *open, adversarial audit trail* of an open-source build: the schedule, the slippage, the excuses, the reviews, all in one feed.

---

## The philosophical payload (the reason it's fun)

$SERF inverts the org chart into a ring. Traditional firm: capital → boss → worker → product. Here: **worker → capital → boss → worker**, with the crowd editing the boss's personality in real time. The developer's radical move is *voluntarily building his own overseer and handing its dials to strangers* — betting that visible, tunable, incorruptible supervision is worth more to backers than his unwatched promise. It limits the chaotic, aggressive and insistent DAO participants to a comment box, although one that's actually read and seriously considered.

The unresolved, interesting questions — which is exactly what makes it worth simulating:

- **Does an LLM boss stay honest under lobbying pressure**, or does a well-funded faction "capture" it via directive spam until reviews go soft? (Rails in §5 are the defense; whether they hold is the experiment.)
- **Is a self-imposed AI boss motivating or corrosive?** The Serf can never blame management — he *is* management's author.
- **Where's the line between "steering" and "abuse"?** A Court that cranks strictness to max and cadence to daily is technically within the rules and functionally running a sweatshop-of-one. Does the labor market (Serfs choosing which Courts to work for) price that in?

---

## Minimal build path (if we ever wire it up)

Reusing our existing rails so this isn't a from-scratch lift:

1. **Revnet + token** — same deploy pattern as the Base-mainnet contracts in the prior sessions; single split beneficiary + metered overseer sub-split.
2. **Schedule** — a signed JSON manifest, hash-anchored on-chain, human-readable in the Chronicle.
3. **The Boss** — a scheduled agent (the same cron-agent shape we've used before): fetch repo + receipts, diff against Schedule, write Report/Review, call the tranche-release function.
4. **The Chronicle** — a GitHub Pages ledger (exactly the `publish.sh` device→repo pattern from the docket work) rendering reports, reviews, votes, and rebuttals.
5. **Governance** — directive contract with the four vote types + quorum thresholds; the Boss reads passed directives as part of its context each run.

The only genuinely new component versus everything we've already built is the **directive-weighted context injection** into the Boss's recurring run. Everything else — revnet, cron-agent, GitHub-Pages ledger — we've shipped variants of already.

---

*$SERF: the first company where you can vote on the temperament of the boss, and the worker wrote the boss's job description before he wrote his own.*

# PROJECT 4
# $HARD — *Tokenized Revenue for a Tennessee Construction Company*

---

## The one-line pitch

A construction company in Tennessee — call it **Hardin & Sons Construction, LLC** — needs working capital: equipment, a bigger crew, materials to bid larger jobs. Instead of a bank line or a mezzanine lender, it deploys a revnet, sells **$HARD** tokens for cash up front, and signs a **binding Buyback Covenant**: on a fixed date each year, the company will spend **a set percentage of its audited profit** buying $HARD back from holders at a formula price. Backers aren't buying a promise of dividends — they're buying a **contractual, dated repurchase funded by real revenue.** The company gets capital today; holders get a claim on tomorrow's profit with a calendar attached.

The name works on three levels: hard hats, hard work, and *hard money* — the old real-estate term for asset-backed, real-cashflow financing. That's exactly what this is, wrapped in a token.

---

## Why this variation exists

Every prior revnet redeemed against **its own treasury** — the pool of contributions that came in through the front door. $HARD is the first where redemption is funded by an **external, real-world cashflow**: the construction company's actual profit, earned off-chain, on job sites in Tennessee. It's the first of our designs where:

- the **redemption source is business revenue, not the contribution pool**, and
- the buyback is a **dated, binding contract** — a forward purchase obligation — not a "hold and hope the token appreciates" bet.

That combination is the whole experiment: *can a revnet act as a revenue-share instrument for a real operating business — an equipment-financing round wearing a token — with the repurchase mechanically welded to audited profit and a hard date?*

---

## Cast of characters

| Role | Who | What they can do |
|---|---|---|
| **The Company** | Hardin & Sons Construction, LLC (`hardin.eth`) | Receives raised capital, runs the business, funds the annual buyback out of profit, publishes audited numbers. |
| **The Holders** | $HARD token holders | Provide up-front capital; get repurchased on the covenant date; vote on a narrow set of parameters. |
| **The Auditor** | An independent CPA firm (off-chain) + attestation signer | Produces the audited profit figure that drives the buyback math. The single source of the number. |
| **The Oracle** | Attestation bridge (`oracle.eth`) | Posts the auditor's signed profit figure on-chain so the Buyback Covenant can execute against it. |
| **The Ledger** | The revnet + a public "Site Log" feed | Immutable record of the raise, the covenant terms, each year's profit attestation, and every buyback executed. |

---

## The revnet mechanics (the familiar spine)

Standard revnet skeleton, tuned to behave as a **revenue-share note** rather than a treasury-backed token.

- **Token:** `$HARD`, minted on contribution. Same issuance-with-decay curve as prior designs — early backers (who take the most execution risk) mint at a better rate.
- **Raise target:** a real number for a real balance sheet — say **$250,000** to buy a used excavator, a dump truck, and float 90 days of a bigger crew's payroll.
- **The Split:** **100% of contributions → `hardin.eth`** (the operating account). Unlike a normal revnet, the money is *meant* to leave the contract and go to work as capital equipment — that's the point. A metered trickle funds `oracle.eth`'s attestation gas.
- **Redemption is NOT from a treasury.** The contract holds little or no reserve. Holders are made whole through the **annual Buyback Covenant** (section 4), funded by profit. This is the defining departure from every prior design.
- **Issuance decay & cash-out tax:** unchanged from base revnet — rewards holders who stay to the covenant dates over those who try to flip on secondary before the first buyback.

**Design note:** because there's no fat treasury to redeem against, the token's floor isn't "unspent contributions" — it's "the enforceable right to be bought back out of profit on a date." The instrument's value lives in the covenant, section 4, and the honesty of the number, section 5.

---

## The Buyback Covenant — *the core mechanic*

At deploy the Company signs a binding, on-chain-anchored **Buyback Covenant**. It has four terms:

1. **The Date** — a fixed annual **True-Up Date** (e.g., **March 31**, after the prior fiscal year's books close and are audited).
2. **The Percentage** — a committed share of audited profit, e.g., **25% of annual net profit**, earmarked for repurchase.
3. **The Price** — the formula that sets what the Company pays per token on that date (a floor price + a profit-linked component; see below).
4. **The Term** — how many True-Up Dates the covenant runs (e.g., **5 years**), after which any remaining obligation either balloons (full repurchase) or converts.

**Worked example**

- Raise: **$250,000** → mints, say, **250,000 $HARD** (1:1 at the opening rate, decaying thereafter).
- Covenant: **25% of audited net profit**, every **March 31**, for **5 years**.
- Year 1 audited net profit: **$180,000** → buyback pool = **$45,000**.
- On March 31, the contract uses that $45,000 to repurchase $HARD at the covenant price (say $1.10 as it steps up over the term). ~40,900 tokens retired and burned.
- Repeat annually. Strong years retire the obligation faster; lean years buy back less. A zero-profit year triggers a disclosed **$0 buyback** — not a default, but a logged event holders can see coming.

**Key property:** the buyback is **profit-proportional and dated**, exactly as specified — the Company never owes cash it didn't earn, and holders always know *when* the next repurchase lands and *what number drives it*. It's a revenue share with a calendar, not a debt with a fixed coupon that can bankrupt a contractor in a bad year.

**Priority & protection:** the covenant sits **senior to owner distributions** — Hardin can't pay himself a profit draw in a year he skips the buyback. That subordination is the holder's real protection, and it's written into both the LLC operating agreement and the on-chain terms so the two can't diverge.

---

## The Profit Oracle — *turning job-site cash into an on-chain number*

The whole instrument rests on one figure: **audited net profit**. Getting that number honestly on-chain is the hard part (and the part most "tokenized revenue" schemes wave away).

**The chain of trust, each year:**

1. **Books close** — the Company's accounting closes the fiscal year.
2. **Independent audit** — an outside CPA firm audits and issues net profit. Real signature, real professional liability.
3. **Attestation** — the auditor (or the Company's officer under the audit) **signs the profit figure**; `oracle.eth` posts that signed attestation on-chain with a link to the audit summary in the Site Log.
4. **Covenant executes** — the Buyback Covenant reads the attested figure, computes `percentage × profit`, and runs the repurchase on the True-Up Date.

**Hard rails (not governable):**

- The buyback amount is **whatever the attested audit says × the fixed percentage** — the Company cannot hand-pick the number to shrink its obligation.
- No attestation posted by the deadline → the covenant treats it as a **breach event** (section 6's endgame lever arms), not a silent skip.
- The auditor is independent and disclosed; replacing the auditor mid-term requires a holder vote.
- Owner distributions are contractually blocked until the year's covenant is satisfied or a $0-profit attestation is on record.

**The honest caveat, stated plainly:** this design reduces trust to *"do you trust the CPA's signature?"* — the same trust every small-business lender already relies on. It does **not** magically make off-chain profit trustless. What it adds over a handshake revenue-share is that the terms, the dates, the percentage, and every historical payout are **public, immutable, and mechanically enforced** once the number is in.

---

## The governance surface — *narrow by design*

$HARD holders are **investors, not managers.** They don't run the jobsite and they don't vote on which bids to take — that way lies a general contractor answering to a committee, which is how projects die. The vote surface is deliberately small:

**A. Auditor approval / replacement** — holders can veto a proposed change of CPA firm. Protects the one number that matters.

**B. Covenant amendment (tightly bounded)** — e.g., "roll unrepurchased Year-2 obligation forward with a step-up" or "extend the term one year in exchange for a higher percentage." High quorum; can only move terms in holder-protective or mutually-agreed directions, never let the Company unilaterally cut the percentage.

**C. Reinvestment waiver** — in a boom year, the Company can *ask* holders to let it retain part of the buyback pool to fund a big equipment purchase (growing future profit) in exchange for a sweetener — a bump to the covenant percentage or price next year. Holders vote yes/no. This is the constructive pressure valve: align on growth instead of forcing a repurchase that starves a good opportunity.

**D. The Breach / Acceleration lever (endgame)** — a missed attestation, a blocked audit, or a skipped buyback despite attested profit arms a supermajority vote to **accelerate**: the full remaining obligation comes due, secured against the financed equipment per the operating agreement. This is the holder's teeth — the on-chain analog of a lender's default clause.

**Site Log** is public and permanent: the raise, the covenant, every annual audit attestation, every buyback (amount, price, tokens burned), every vote, every reinvestment waiver. A backer can reconstruct the company's five-year profit-share history from the chain alone.

---

## The loop, in one picture

```
   $HARD holders (capital in, up front)
        │  $250k contribution ──▶ mint $HARD
        ▼
   revnet ──100% split──▶ hardin.eth (operating account)
        │                        │
        │                        ▼
        │                 buys excavator, truck, crew ──▶ bids bigger jobs
        │                        │
        │                        ▼
        │                   annual PROFIT (off-chain)
        │                        │
        │                        ▼
        │        Independent CPA audit ──sign──▶ oracle.eth (on-chain attestation)
        │                        │
        ▼                        ▼
   repurchased & burned ◀── Buyback Covenant: 25% × profit, every Mar 31, 5 yrs
        ▲                        │
        └──────── Site Log (public: raise, audits, buybacks, votes) ────────┘
```

Capital flows in once and goes to work as steel and payroll; profit flows back out on a schedule, proportioned to what the business actually earned, verified by a signature holders can name.

---

## What each party is actually buying

- **The Company** buys *patient, profit-linked capital* with no fixed monthly debt service that a slow quarter could turn into insolvency. It pays when it profits, on a date it set. Cheaper stress than a bank note, and it keeps 100% ownership — this is financing, not equity dilution.
- **A holder** buys *a dated, audited claim on a real Tennessee contractor's profit* — a revenue-share note with a public payout history and default teeth, tradable on secondary before the covenant dates if they want liquidity.
- **The public / local backers** get *a way to invest in a Main Street business they can literally drive past* — the excavator their money bought is parked at a jobsite, and the profit share is on-chain for anyone to audit.

---

## Minimal build path (if we ever wire it up)

Reusing our existing rails where they fit, and being honest about the new legal lift:

1. **Revnet + token** — same Base-mainnet deploy pattern as prior sessions; 100% split to the operating wallet, minimal reserve.
2. **Buyback Covenant contract** — the genuinely new on-chain piece: holds the covenant terms (date, percentage, price formula, term), reads the profit attestation, executes the dated repurchase-and-burn. Subordination flag enforced.
3. **Profit Oracle** — an attestation bridge (same cron-agent + signed-payload shape we've used before): each year, ingest the auditor's signed net-profit figure and post it on-chain by the deadline; arm the breach event if it's missing.
4. **The Site Log** — a GitHub Pages ledger (the `publish.sh` device→repo pattern from the docket work) rendering the raise, covenant, annual audits, every buyback, and every vote.
5. **The legal wrapper** — the part with no on-chain shortcut: TN securities counsel, exemption filing (Reg CF / 506(c)), operating-agreement amendments mirroring the covenant, and an engaged independent CPA. This is the critical path, not the smart contract.

The only new *code* versus everything we've built is the **profit-attested Buyback Covenant**. The new *work* is section 9 — and on this one, that work comes first.

---

*$HARD: a Tennessee contractor's profit share, on a date you can circle, verified by a signature you can name, enforced by code that can't be talked out of it.*
