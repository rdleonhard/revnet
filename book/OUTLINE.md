# OUTLINE — *Revnet in Venice* (working title)

**Status:** annotated outline, awaiting sign-off. No chapter prose written yet.
**Thesis (locked):** seed capital is changing substrate — in the AI age the scarce input is
compute/inference, not money; the new founder is a solo open-source dev with an idea and an
API bill; revnets (culminating in the productive-reserve / Venice model) are the honest,
repeatable mechanism for raising compute instead of capital.

**Legend for sources:** [LIVE] = a real prototype exists · [HYPO] = designed sample project ·
[PROPOSAL] = protocol design doc.

**Structural notes / proposed changes (for your sign-off):**
- Added a short **Chapter 0 (Preface)** so the book can carry the repo's "not legal advice"
  disclaimer and the LIVE-vs-HYPOTHETICAL reading contract up front, once, cleanly.
- Recommend **merging 13 + 14** if the risk material runs thin, or keeping them split if the
  security/counterparty surface earns its own chapter (my bet: keep split — Venice
  counterparty risk is distinct enough).
- Recommend **Ch. 12 (Venice, worked end-to-end) act as the book's spine** — everything
  before it is setup, everything after is stress-test and playbook. Consider promoting it
  earlier if early readers feel the payoff is buried; my current bet is to keep the build-up.
- Target total length: ~40,000–55,000 words (a tight, argument-driven book, not a doorstop).

---

## Chapter 0 — Preface: how to read this book
- **Status:** draft written → [`chapters/00-preface.md`](chapters/00-preface.md)
- **Purpose:** Set the reading contract in one page: what's live vs. designed, that nothing
  here is legal or investment advice, and that intellectual honesty (every hype line grounded
  or caveated) is the book's governing rule.
- **Key points:** (1) the LIVE/HYPO labeling convention; (2) the no-legal-advice disclaimer
  carried from the repo; (3) a one-paragraph statement of the thesis; (4) an invitation to the
  skeptic — "if a claim sounds too good, I owe you the catch in the same breath."
- **Draws on:** README.md disclaimer.
- **Target:** 600–900 words.
- **Open questions:** Do you want a named author voice ("I") or the repo's collective "we"?

---

## PART I — Compute Is the New Capital

### Chapter 1 — The founder has changed
- **Status:** draft written → [`chapters/01-the-founder-has-changed.md`](chapters/01-the-founder-has-changed.md)
- **Purpose:** Establish the protagonist of the whole book — the solo open-source dev with an
  idea and a model API bill — and show why their needs don't match the machinery built for the
  old founder (team, office, 18-month runway, VC).
- **Key points:** (1) what a 2020s founder actually needs on day one is inference + a little
  runway, not headcount; (2) the old capital stack (angels, seed rounds, dilution) is
  mis-sized and mis-shaped for them; (3) open source changes the trust model — the work is
  public, the believer can verify; (4) foreshadow: if the need is compute, raise compute.
- **Draws on:** $SERF [HYPO] as the archetype protagonist.
- **Target:** 1,800–2,400 words.
- **Open questions:** Do you want a real-named practitioner anecdote here, or keep it archetypal?

### Chapter 2 — Why money was the bottleneck, and inference is the new one
- **Status:** draft written → [`chapters/02-money-was-the-bottleneck.md`](chapters/02-money-was-the-bottleneck.md)
- **Purpose:** Make the substrate-shift argument rigorously — money was scarce because it
  bought scarce labor; AI collapses the labor cost, and the residual scarcity migrates to
  compute/inference.
- **Key points:** (1) the old cost curve (salaries dominate a seed budget); (2) the new cost
  curve (one dev + large inference spend); (3) inference as the true variable cost of an
  AI-native product (COGS); (4) therefore the natural thing to raise, reserve, and repay in
  is compute itself.
- **Draws on:** revnet-in-venice.md [PROPOSAL] (the COGS-hedge thesis, T2).
- **Target:** 2,000–2,600 words.
- **Open questions:** Need a defensible, sourced illustration of inference-cost-as-COGS; flag
  for verification rather than inventing numbers.

### Chapter 3 — A revnet in one breath
- **Status:** draft written → [`chapters/03-a-revnet-in-one-breath.md`](chapters/03-a-revnet-in-one-breath.md)
- **Purpose:** The primer. A reader who has never touched a token should finish this chapter
  able to explain a revnet to a friend: staged issuance, cash-out floor, no governance.
- **Key points:** (1) mint-on-contribution + issuance decay (early believers buy cheapest by
  rule); (2) the redemption floor / cash-out tax (never worth less than reserve backing);
  (3) no governance to rot; (4) why these three properties are exactly what an audacious,
  long-dated promise needs — the honesty argument.
- **Draws on:** README.md general revnet framing; $WAKE [LIVE prototype + designed token] for
  the "honest issuer for a long promise" point.
- **Target:** 2,000–2,800 words. **Must include an ASCII diagram** of the basic revnet loop.
- **Open questions:** How much bonding-curve math to expose vs. keep to an appendix?

---

## PART II — The Mechanics

### Chapter 4 — Staged issuance, the floor, and no governance
- **Status:** draft written → [`chapters/04-issuance-floor-governance.md`](chapters/04-issuance-floor-governance.md)
- **Purpose:** Deepen the primer into real mechanism design — why each property is
  incentive-compatible, and what breaks without it.
- **Key points:** (1) issuance decay as a fair, rules-based cap table; (2) the floor as
  anti-rug insurance and why it changes holder psychology; (3) no-governance as
  credibility-through-immutability; (4) the failure modes each property prevents.
- **Draws on:** README.md; $CITE [HYPO] for how immutability reads to a *company*, not a DAO.
- **Target:** 2,200–3,000 words. ASCII diagram of the issuance/redemption curve.
- **Open questions:** None major.

### Chapter 5 — From inert to productive reserves (the Venice leap)
- **Status:** draft written → [`chapters/05-inert-to-productive-reserves.md`](chapters/05-inert-to-productive-reserves.md)
- **Purpose:** The book's turning point — name the flaw in every prior revnet (the reserve
  just sits there) and introduce the fix (make it productive).
- **Key points:** (1) idle reserve = real opportunity cost; (2) the leap: a reserve that earns;
  (3) the special case that matters — a reserve that earns *the exact resource the product
  burns*; (4) separation of principal vs. yield as the enabling idea.
- **Draws on:** revnet-in-venice.md [PROPOSAL] §1–§3.
- **Target:** 2,000–2,600 words.
- **Open questions:** None.

### Chapter 6 — Raising inference: staking the treasury, VVV and Diem
- **Status:** draft written (grounded in Venice's 2026 live docs) → [`chapters/06-raising-inference-vvv-diem.md`](chapters/06-raising-inference-vvv-diem.md)
- **Purpose:** Concretely explain the productive-reserve machine — staked VVV, emission yield,
  and Diem (inference capacity) — as three separable value streams.
- **Key points:** (1) principal = holders' redeemable VVV claim; (2) emission yield funds the
  split without touching principal; (3) Diem funds development in kind; (4) the
  reserve-per-token ratchet and why it must be VVV-denominated, not USD-priced.
- **Draws on:** revnet-in-venice.md [PROPOSAL] §3–§4, §8 invariants.
- **Target:** 2,400–3,000 words. **ASCII diagram** of the three streams.
- **Open questions:** VERIFY against Venice's live docs — emission schedule, unbonding
  cooldown, Diem accrual/expiry, per-VVV inference dilution. Treat all as assumptions until confirmed.

### Chapter 7 — The cast: dev, marketer, holders, future buyers, and the AI boss
- **Status:** draft written → [`chapters/07-the-cast.md`](chapters/07-the-cast.md)
- **Purpose:** Show that one productive treasury can serve many roles at once, each drawing
  from a different layer — the human story of the mechanism.
- **Key points:** (1) the dev takes Diem; (2) the marketer takes the split; (3) holders keep a
  redeemable claim and bear only market risk; (4) future buyers enter at a ratcheted floor;
  (5) the AI boss ($SERF) as a new role — accountability without a human manager.
- **Draws on:** revnet-in-venice.md §6; $SERF [HYPO] for the boss/agent role.
- **Target:** 2,000–2,600 words. Roles table.
- **Open questions:** None.

---

## PART III — Case Studies (from the repo)

### Chapter 8 — $SERF: building your own boss to raise your own runway
- **Purpose:** The purest dramatization of "raise inference, not money" — a dev funds LLM
  credits via a revnet and hires an AI boss to hold himself accountable to token holders.
- **Key points:** (1) the sworn schedule as a self-imposed contract; (2) the split pointed at
  the dev, funded honestly; (3) token holders lobby the boss, not the dev; (4) what this proves
  about AI-mediated accountability.
- **Draws on:** $SERF [HYPO] (README PROJECT 3).
- **Target:** 2,200–2,800 words. ASCII of the boss loop.
- **Open questions:** Keep $SERF's monetary framing ($5k credits) or re-denominate in Diem to
  tie it to the Venice spine? (My recommendation: show both — dollars first for intuition,
  then the Diem-native version as the upgrade.)

### Chapter 9 — $HARD: when the revenue is real
- **Purpose:** Extend the model from a pre-revenue dev to a real operating business, and
  confront the hard part — getting off-chain profit honestly on-chain.
- **Key points:** (1) the Buyback Covenant (dated repurchase from % of audited profit); (2) the
  profit oracle / attestation and its trust assumptions; (3) redemption from external cashflow
  as the anti-ponzi proof; (4) the honest caveat — this reduces trust to "do you trust the CPA."
- **Draws on:** $HARD [HYPO] (README PROJECT 4).
- **Target:** 2,200–2,800 words.
- **Open questions:** How hard to lean on the oracle-trust problem without turning into a
  chapter on audits?

### Chapter 10 — $WAKE: issuing a promise longer than the promiser
- **Purpose:** Show the revnet as the only honest issuer for a *forever* product, and use the
  one genuinely live prototype to ground the whole book in something real.
- **Key points:** (1) the credibility problem of perpetuity businesses; (2) opt-out issuance;
  (3) the floor as "nobody holds a rug in a graveyard"; (4) what the live constellation
  actually demonstrates — and, honestly, what it does not yet.
- **Draws on:** $WAKE [LIVE prototype + designed token] (README PROJECT 1). **Label carefully.**
- **Target:** 2,000–2,600 words.
- **Open questions:** Exactly which parts of the Testament Network are live vs. designed — get
  a precise inventory so the chapter never overclaims.

### Chapter 11 — $CITE: the centralized company that still chose a revnet
- **Purpose:** Break the reflex that revnets are only for crypto-native DAOs — show a normal
  centralized company choosing one, and why.
- **Key points:** (1) what a centralized issuer gains from immutable rules; (2) how customers/
  backers read that credibility; (3) where centralization and revnet properties tension;
  (4) the boundary of the model.
- **Draws on:** $CITE [HYPO] (README PROJECT 2).
- **Target:** 1,800–2,400 words.
- **Open questions:** $CITE is the thinnest source doc — may need expansion in the README
  first, or the chapter carries more original argument. Flag which.

### Chapter 12 — Revnet in Venice: the keystone, worked end to end
- **Purpose:** The spine. Assemble everything into one worked example of a solo dev raising
  compute through a productive-reserve revnet, start to finish, with numbers.
- **Key points:** (1) the full lifecycle (raise → stake → route yield + Diem → ratchet →
  redeem); (2) a numeric walk-through; (3) the six invariants as the safety rails; (4) why this
  is the natural endpoint of the whole argument.
- **Draws on:** revnet-in-venice.md [PROPOSAL] in full; callbacks to $SERF, $HARD.
- **Target:** 3,000–3,800 words (the longest chapter). Full ASCII lifecycle diagram + a
  numeric table.
- **Open questions:** Same Venice-mechanics verifications as Ch. 6 — this chapter must not
  harden any unverified assumption into a stated fact.

---

## PART IV — Risks, Honestly

### Chapter 13 — The economic caveats
- **Purpose:** The honesty chapter that earns the reader's trust — lay out where the model can
  fail economically and how each risk is mitigated.
- **Key points:** (1) reserve concentration / VVV price risk; (2) yield decay + Diem dilution;
  (3) bank-run / unbonding mismatch; (4) reflexive valuation and the single design choice that
  neutralizes it (VVV-denominated ratchet).
- **Draws on:** revnet-in-venice.md §7 (economic) + §8 invariants.
- **Target:** 2,200–2,800 words. Caveat→mitigation table.
- **Open questions:** None — source is detailed.

### Chapter 14 — The security and counterparty surface
- **Purpose:** Cover the web/smart-contract and dependency risks a builder actually faces.
- **Key points:** (1) staking-integration attack surface + adapter isolation; (2) oracle
  manipulation and how VVV-unit redemption removes the oracle from the critical path; (3) MEV
  on the ratchet; (4) the irreducible one — Venice counterparty/centralization risk.
- **Draws on:** revnet-in-venice.md §7 (security + dependency).
- **Target:** 2,200–2,800 words.
- **Open questions:** Whether to include a short "questions to ask before you deploy" checklist.

### Chapter 15 — "Isn't this just…?" — the strongest objections, answered
- **Purpose:** Directly disarm the reflexive dismissals (ponzi, disguised equity, glorified
  Kickstarter, crypto-for-crypto's-sake) with the book's best arguments.
- **Key points:** (1) not a ponzi — ops from yield, redemption from external cashflow; (2) not
  equity — no ownership/governance transfer, redeemable floor instead; (3) not Kickstarter —
  liquid, floored, and repeatable; (4) the honest residual — what the skeptic is *right* about.
- **Draws on:** all prior chapters; revnet-in-venice.md anti-ponzi framing.
- **Target:** 2,000–2,600 words.
- **Open questions:** None.

---

## PART V — The Playbook

### Chapter 16 — How a solo dev raises compute, step by step
- **Purpose:** Convert the whole argument into an actionable sequence a reader could follow.
- **Key points:** (1) define the idea + the inference budget; (2) choose the reserve mode
  (inert vs. productive); (3) set issuance, split, and Diem routing; (4) publish the schedule /
  accountability structure; (5) launch, report, iterate.
- **Draws on:** revnet-in-venice.md §10 build path; $SERF schedule pattern.
- **Target:** 2,400–3,000 words. Numbered playbook + a decision table.
- **Open questions:** Keep tooling-agnostic, or name specific stacks (and risk dating the book)?

### Chapter 17 — Where this goes next
- **Purpose:** The closing horizon — multi-provider compute reserves, agent-run treasuries, and
  what "raising compute" becomes when it's normal.
- **Key points:** (1) beyond a single provider (Venice as v1, not forever); (2) agents as
  first-class treasury participants; (3) the cultural shift for open source; (4) an honest note
  on what still has to be proven.
- **Draws on:** revnet-in-venice.md counterparty-diversification mitigation; $SERF agent thread.
- **Target:** 1,800–2,400 words. Closing italic tagline for the whole book.
- **Open questions:** None.

---

## Appendices (proposed, optional)
- **A. Bonding-curve math** — the issuance/redemption formulas for readers who want them.
- **B. The six invariants** — lifted verbatim from revnet-in-venice.md as a quick reference.
- **C. Glossary** — see `book/GLOSSARY.md`.
- **D. To-verify register** — a running list of every Venice/VVV/Diem assumption flagged across
  chapters, so nothing ships to `final` unchecked.

---

**Next step:** review, adjust structure, then approve. On approval I'll draft **Chapter 0 →
Chapter 1** using the Per-Chapter Prompt in `AUTHORING-PROMPT.md`.
