# GLOSSARY — *Revnet in Venice*

Canonical definitions. Define each term once here; reuse consistently across chapters. When a
chapter uses a term for the first time, it should match this wording (or link here).

- **revnet** — a "revenue network": a token whose issuance and redemption rules are fixed in a
  smart contract and cannot be changed by anyone, including its creator. Contributions mint
  tokens; a reserve backs their redemption. The point is credibility through immutability.

- **staged issuance / issuance decay** — the rule that each successive contribution mints
  fewer tokens than the last, so the earliest believers get the best rate. A fair, rules-based
  cap table: no negotiation, no insider round.

- **cash-out tax / redemption floor** — the redemption mechanism. A holder can always cash out
  for a pro-rata share of the reserve (the *floor*); an exit fee (the *cash-out tax*) is left
  behind for remaining holders, rewarding duration over flipping. The token is never worth
  less than its reserve backing.

- **the split** — the portion of inflows (or, in the productive-reserve model, of yield) routed
  to a beneficiary — e.g., a developer or a marketer — rather than held in reserve.

- **reserve asset** — what backs redemption. Traditionally ETH or USDC sitting inert in the
  treasury. This book's argument is that it should instead be *productive*.

- **productive reserve** — a reserve asset that earns yield rather than sitting idle. The
  book's keystone: a reserve of **staked VVV** that yields both more VVV and inference capacity.

- **bonding curve** — the pricing function that sets how many tokens a contribution mints and
  how much a redemption returns, as a function of how much reserve is held. Issuance decay is
  one shape of bonding curve.

- **VVV** — the token of Venice (an AI/inference platform). Staking VVV is *productive*: it
  yields staking emissions (more VVV) and an entitlement to inference capacity (Diem). Used in
  this book as the productive reserve asset. *(All specific VVV mechanics — emission schedule,
  unbonding period — are modeling assumptions to verify against Venice's live docs, not settled
  facts.)*

- **Diem / inference capacity** — the daily allotment of inference (compute) that staked VVV
  entitles the treasury to. A *flow* that refreshes on a cadence, not a stored balance. In the
  model, Diem funds the developer's actual product usage in kind.

- **emission yield** — the staking rewards (denominated in more VVV) that accrue to staked VVV.
  Cash-like; used to fund the split without touching principal, or to compound the reserve.

- **reserve-per-token ratchet** — the mechanical rise in the redemption floor (and the price
  new buyers pay) as emission yield compounds into the reserve. **Load-bearing rule:** the
  ratchet must be sourced from *VVV-denominated* yield, never VVV's USD price, or it becomes
  reflexive and unsafe.

- **principal** — the staked VVV underlying holders' redeemable claims. Preserved; operating
  costs are paid from yield, not principal.

- **the boss / agent** — (from $SERF) an AI agent hired by a developer to hold themselves
  accountable to token holders — running progress reports and performance reviews against a
  sworn schedule. Token holders lobby the boss rather than manage the developer directly.

- **buyback covenant** — (from $HARD) a binding commitment to repurchase tokens on a fixed
  date using a set percentage of audited profit. Redemption funded by external cashflow.

- **oracle / attestation** — the bridge that carries an off-chain fact (e.g., audited profit)
  onto the chain via a signed statement, so a contract can act on it. Its trust reduces to
  trusting the signer.

- **counterparty risk** — the risk that an external party the model depends on (here, Venice
  continuing to honor Diem and maintain the network) changes terms or fails. The one
  irreducible risk in the productive-reserve model; mitigated by sizing, exit routes, and a
  swappable adapter, not eliminated.

- **LIVE / HYPOTHETICAL** — the book's labeling contract. LIVE = a real prototype exists
  (e.g., parts of $WAKE's Testament Network). HYPOTHETICAL = a designed sample project used to
  illustrate a mechanism (e.g., $SERF, $HARD, $CITE). Never let a hypothetical read as shipped.
