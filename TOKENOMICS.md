# SIETCH Tokenomics

> **Version:** 1.3.1
> **Date:** April 2026
> **Status:** Public summary. Subject to refinement before mainnet TGE.

> SIETCH is a functional protocol component used for validator staking, governance voting, and validator compensation for computational work. Nothing in this document is a promise of financial return, price projection, or revenue forecast. Users of the Sietch network do not need to acquire or hold SIETCH to deposit, transfer, or withdraw shielded assets.

## Table of Contents

- [1. Token Overview](#1-token-overview)
- [2. Genesis Allocation](#2-genesis-allocation)
- [3. Vesting Schedule](#3-vesting-schedule)
- [4. Founders Lockup](#4-founders-lockup)
- [5. Community and Ecosystem Programs](#5-community-and-ecosystem-programs)
- [6. Launch Liquidity](#6-launch-liquidity)
- [7. Custody and Vesting Infrastructure](#7-custody-and-vesting-infrastructure)
- [8. Governance](#8-governance)
- [9. Service Fees and Validator Compensation](#9-service-fees-and-validator-compensation)
- [10. TGE Circulating Supply](#10-tge-circulating-supply)
- [11. Public Disclosure](#11-public-disclosure)
- [Disclaimer](#disclaimer)

---

## 1. Token Overview

| Parameter | Value |
|:---|:---|
| Network | Sietch Network |
| Token | SIETCH |
| Total supply | 570,000,000 SIETCH |
| Supply policy | Fixed at genesis. No inflation. No tail emission. No mint authority after TGE. |
| Functional roles | Validator staking, on-chain governance, validator compensation for computational work |
| User interaction | Not required to deposit, transfer, or withdraw shielded assets |

The full 570,000,000 SIETCH is minted in a single transaction at the Network Launch Date (TGE). The token contract calls `finalizeMint()` in the same transaction, permanently renouncing mint authority. Total supply is fixed at the contract level; any future change requires a hard fork.

---

## 2. Genesis Allocation

| Bucket | % of supply | SIETCH |
|:---|---:|---:|
| Team and Advisors | 25.00% | 142,500,000 |
| Strategic Backer Pool | 19.00% | 108,300,000 |
| Treasury / DAO | 21.00% | 119,700,000 |
| Community / Ecosystem / Airdrops | 30.00% | 171,000,000 |
| Public Liquidity / Launch | 5.00% | 28,500,000 |
| **Total** | **100.00%** | **570,000,000** |

**Team and Advisors (25%)** is divided among the founders' grant, the employee and future-hire reserve, and the advisor cohort. No single advisor receives more than 0.50% of total supply. Per-cohort sub-allocations within this bucket are recorded on the public vesting registry at TGE.

**Strategic Backer Pool (19%)** is the fixed pool from which SAFE Side-Letter holders draw if they elect tokens (in lieu of, or in addition to, equity). The pool size is fixed regardless of election outcomes; any un-elected portion flows to Treasury at the close of the 60-day Election Window after TGE. There is **no public token sale**.

**Treasury / DAO (21%)** is held at TGE in a Foundation-controlled `TimelockController`. The on-chain Governor is added as a proposer by mainnet month 18, at which point the Foundation multisig is downgraded to a `canceller`-only role.

---

## 3. Vesting Schedule

All vesting is measured from mainnet TGE. Continuous (per-second) accrual via Sablier V2 streams; the monthly cadence below is the discretization used in public reporting. There is **no** retroactive lump-sum release at the cliff: at the cliff date vesting *starts*, and tokens accrue from that point forward.

| Cohort | Cliff (months) | Linear vest after cliff (months) | Total duration | TGE unlock |
|:---|---:|---:|---:|---:|
| Founders | 12 | 36 | 48 months | 0% |
| Employee + future-hire reserve | 12 | 36 | 48 months | 0% |
| Advisors | 6 | 18 | 24 months | 0% |
| Strategic Backer Pool | 12 | 24 | 36 months | 0% |
| Treasury / DAO | 0 | 60 | 60 months | Linear from TGE |
| Ecosystem Grants | 0 | 60 | 60 months | Linear from TGE |

Insider cohorts (Team, Strategic Backers, Advisors, Founders) receive **0% at TGE**. Insider unlock dates are deliberately staggered so they do not coincide.

---

## 4. Founders Lockup

The founders are subject to a contractual no-sell on **all founders' tokens** (vested or unvested) for **24 months from mainnet TGE**, regardless of vesting status.

- Vesting and lockup run in parallel: the founders vest into locked balances.
- At month 24, the portion of founders' tokens that has vested during the lockup window becomes transferable. The exact vested figures at release are computable from the founders' vesting streams on the public registry.
- The lockup is enforced on-chain via a single-purpose `LockupGate` wrapper contract that intercepts all withdrawals from the founders' vesting streams and reverts before the release timestamp.
- The wrapper supports a **one-way ratchet**: each founder may unilaterally extend their own lockup at any time before month 18 by signing a public on-chain commitment. The lockup cannot be shortened.
- Override only via a public, governance-ratified motion (after Foundation handoff). No private waiver.

**Disposal precommitment.** No later than month 18, each founder publicly precommits to a 90-day equal-tranche disposal schedule on their released balance, executed through a pre-published OTC and DEX execution plan, with each daily tranche posted on-chain.

---

## 5. Community and Ecosystem Programs

The 30% Community / Ecosystem / Airdrops bucket (171,000,000 SIETCH) is split across five programs.

| Program | % of supply | SIETCH | Schedule |
|:---|---:|---:|:---|
| Genesis airdrop | 5.00% | 28,500,000 | 25% at TGE; 75% linear over 12 months |
| Validator Delegation Program | 6.00% | 34,200,000 | 5% at TGE; 95% linear over 36 months |
| Ecosystem Grants | 9.00% | 51,300,000 | DAO-administered; quarterly tranches over 60 months; 0% at TGE |
| Liquidity Bootstrapping | 3.25% | 18,525,000 | 50% at TGE; 50% linear over 18 months, then sunsets |
| Retroactive distribution seasons | 6.75% | 38,475,000 | Three seasons at months 12, 24, 36 (12,825,000 each) |

**Genesis airdrop sybil rules:**

- Per-wallet hard cap: 0.05% of supply (285,000 SIETCH).
- Eligibility: at least 30 days of testnet activity AND at least 5 distinct testnet transactions, OR at least 1 contribution merged into the public repository.
- Quadratic scaling above the eligibility floor (claim proportional to the square root of testnet usage).
- Deposit address must have at least 90 days of mainnet Ethereum activity at snapshot time.
- Snapshot taken 30 days before TGE; ratios published only at TGE.

**Validator Delegation Program.** The Foundation (later DAO) delegates SIETCH stake to validators meeting published technical and uptime thresholds. Validators do **not** receive principal SIETCH; they receive validator compensation flows in pETH (ETH-denominated) per section 9. Delegated principal is recalled to the Foundation/DAO when a validator exits. This is operational stake, not gifted supply.

**Retroactive seasons.** Each season opens nominations to all addresses meeting an on-chain interaction threshold during the season window. Audited contributors and prior-season recipients vote on impact, weighted quadratically. A public retrospective is published within 90 days of each season close.

---

## 6. Launch Liquidity

The 5% Public Liquidity bucket (28,500,000 SIETCH) funds the operational infrastructure for initial exchange listings and on-chain liquidity at TGE. There is no public token sale.

| Recipient | % of supply | SIETCH | TGE state |
|:---|---:|---:|:---|
| Centralized exchange market-maker loans | 2.50% | 14,250,000 | Loaned under standard option-bearing master loan agreements; cycles back to the Foundation at term end (typically 12 months). |
| DEX seed liquidity | 1.75% | 9,975,000 | Live at TGE, paired with USDC on a primary venue; LP position migrates to Protocol-Owned Liquidity by month 12. |
| Foundation operational reserve | 0.75% | 4,275,000 | Liquid at TGE; restricted-purpose multisig; quarterly attestation to the DAO. |

**POL target.** 100% of native-pair DEX liquidity becomes Protocol-Owned Liquidity by month 18.

---

## 7. Custody and Vesting Infrastructure

| Component | Detail |
|:---|:---|
| Genesis mint | All 570,000,000 SIETCH minted in a single transaction at TGE; `finalizeMint()` renounces mint authority in the same transaction. |
| Reserve wallets | One reserve per allocation bucket: Team, Advisor, Strategic Backer, Treasury, Public Liquidity, plus a separate reserve for each of the five Community programs (ten reserves total). All multisigs are 4-of-7 or 3-of-5 with disjoint signer sets; **no two reserves share more than 1 signer**. Treasury sits behind a `TimelockController` rather than a bare multisig. |
| Vesting contract | Sablier V2 `LockupLinear` (audited by Cantina, Spearbit, Code4rena; in production at ENS, Lido, GitcoinDAO). Streams are continuous per-second, revocable by the funding reserve. |
| Founders lockup wrapper | Single-purpose `LockupGate` (~100 lines) that intercepts withdrawals before the release timestamp and exposes only a one-way `extendLockup` ratchet. No pause, no migrate, no upgrade path. |
| Public registry | An on-chain `SietchVestingRegistry` contract publishes every grant: beneficiary, cohort, stream ID, reserve source, amount, cliff, total duration, release timestamp, and revocation status. Indexed by token-unlock dashboards from TGE - 30 days. |

**Bounded clawback.** Default Sablier behavior on cancellation transfers all currently-vested-but-unwithdrawn tokens to the recipient; unvested tokens revert to the reserve. Clawback authority is bounded by cohort:

- **Founders:** no at-will clawback. Only on court order or public governance vote ratifying material breach.
- **Strategic Backers (Side Letter holders):** restricted. Only on loss of eligibility under Side Letter section 5 (sanctions, KYC failure post-grant) or demonstrated breach of Side Letter terms.
- **Employee and Advisors:** clawback on documented material breach, voluntary departure with cause-equivalent terms, or loss of eligibility under Side Letter section 5.
- **Community programs:** per program (e.g., airdrop streams clawed back only on sanctions/KYC trigger; grant streams on milestone failure per the grant agreement).

All clawbacks are public events emitted on-chain, mirrored on the vesting registry within 24 hours, with a written justification posted on the DAO forum.

**Anti-rug guarantees.** Mint authority is renounced. No single multisig compromise touches more than 25% of supply. Founders cannot shorten the lockup. The Strategic Backer pool is sized to exactly 108,300,000 at TGE with no mechanism to refill. Treasury sits behind a `TimelockController` from genesis; Foundation control over Treasury is bounded by the 7-day timelock and is handed off to the on-chain Governor by month 18.

---

## 8. Governance

| Parameter | Value |
|:---|:---|
| Voting power source | Snapshot at proposal-creation block |
| Voting weight (v1) | 1 SIETCH = 1 vote |
| Proposal threshold | 0.10% of circulating supply |
| Quorum (parameter changes) | 6% of circulating supply |
| Quorum (treasury moves greater than 1% of treasury value) | 10% of circulating supply with supermajority of at least 60% |
| Voting period | 7 days |
| Timelock (parameter changes) | 48 hours |
| Timelock (treasury moves) | 7 days |
| Timelock (contract upgrades) | 14 days |
| Emergency multisig | 5-of-9, geographically distributed; no two signers share a cloud or HSM provider |
| Emergency multisig powers | (a) pause the bridge contract, (b) cancel queued malicious proposals, (c) trigger a 30-day grace pause on upgrades. **Cannot mint, transfer treasury, or upgrade contracts unilaterally.** |
| Emergency multisig sunset | After mainnet month 24 OR upon DAO supermajority of at least 66% (whichever later), converts to a 7-day-veto-only role with a 7-of-9 threshold. |
| Reference contracts | OpenZeppelin v5 `Governor`, `TimelockController`, Safe (Gnosis) |

Quarterly treasury attestations (balances, inflows, outflows, runway in months) are published on the DAO forum and the public dashboard.

---

## 9. Service Fees and Validator Compensation

The protocol charges a 15 bps service fee on bridge deposits. A governance-set share of that fee (initially 30-40%) funds validator compensation, denominated in **pETH** (ETH-denominated, since deposits are ETH).

| Element | Detail |
|:---|:---|
| Fee source | 15 bps on bridge deposits (per the bridge contract) |
| Validator compensation | Paid in pETH for computational work: proof verification, state root production, and block consensus participation |
| SIETCH role for validators | Stake required for eligibility; SIETCH itself is not the compensation asset |
| Operational cost coverage | Service fees sustain network operations; remaining fee share funds protocol development and gas sponsorship per governance |
| Non-validator holder distributions | None. There is no SIETCH buyback, no fee redistribution to non-validating SIETCH holders, and no fee-share mechanism for SIETCH holders who do not operate validator infrastructure. |

Fee parameters (the 15 bps rate, the validator share, and the destinations of the remaining share) are set by governance and can be adjusted by on-chain vote subject to the timelocks in section 8.

---

## 10. TGE Circulating Supply

| Quantity | Value |
|:---|---:|
| Total supply | 570,000,000 SIETCH |
| Circulating at TGE | 46,597,500 SIETCH (8.175%) |
| Insider portion at TGE | 0% (Team, Founders, Advisors, Strategic Backers, Treasury all have 0% TGE unlock) |

| Source | SIETCH at TGE | % of total |
|:---|---:|---:|
| Public Liquidity (CEX MM loans, DEX seed, Foundation operational reserve) | 28,500,000 | 5.000% |
| Genesis airdrop TGE portion (25% of bucket) | 7,125,000 | 1.250% |
| Validator Delegation Program TGE portion (5% of bucket) | 1,710,000 | 0.300% |
| Liquidity Bootstrapping TGE portion (50% of bucket) | 9,262,500 | 1.625% |
| Insider buckets (Team / Strategic Backers / Advisor / Treasury) | 0 | 0.000% |
| **Total TGE circulating** | **46,597,500** | **8.175%** |

The full month-by-month unlock waterfall (first 24 months and beyond) is published on the public unlock dashboard at TGE - 30 days and indexed by `token.unlocks.app`-equivalent services. Months in which the unlock event represents a larger share of then-circulating supply are flagged in advance, and structured updates are posted at months 9, 12, 18, 21, 23, and 24.

---

## 11. Public Disclosure

| Item | Status |
|:---|:---|
| Per-cohort vesting schedule | Published before TGE |
| Genesis allocation table (this document) | Published before TGE |
| On-chain vesting registry | Deployed and populated at TGE; queryable by any third party |
| Reserve multisig signer policy | Published before TGE - 60 days |
| Quarterly treasury attestations | Published on the DAO forum from quarter 1 onward |
| Distribution health dashboard | Published before TGE; updated daily |
| Audit scope | OpenZeppelin v5 reference contracts for Governor, Timelock, Safe; Sablier V2 (already audited); custom `LockupGate` wrapper requires its own audit before TGE |

**Distribution health targets** (for the post-vest steady state, around mainnet month 48):

| Metric | Target |
|:---|:---|
| Top-10 holders (excluding contracts and Treasury) | less than 40% of supply |
| Top-100 holders (excluding contracts and Treasury) | less than 70% of supply |
| Validator stake distribution | top-3 validators hold less than 33% of stake |
| Supply held by addresses with at least 30 days holding | greater than 60% |

---

## Disclaimer

This document is a public summary of the SIETCH token's operational role and distribution structure. It is not an offer to sell or a solicitation to buy any security, token, or financial instrument. SIETCH is a functional protocol component required for validator participation in network consensus, on-chain governance voting, and the receipt of validator compensation for computational work performed.

Acquisition and use of SIETCH is restricted in certain jurisdictions and may be limited to specific categories of participants under applicable law. Nothing in this document should be read as a forecast of token price, protocol fee volume, network adoption, or any financial outcome. The Sietch network is open-source software; participation is voluntary, non-custodial, and subject to the operational risks documented in the project whitepaper.

Public-facing copy in this document is derived from the canonical internal specification maintained by Kaynetik LLC and reviewed for compliance with the SEC/CFTC joint interpretive framework on digital commodities. The SAFE and Token Side Letter forms governing accredited participation are private instruments executed under Reg D 506(b)/(c) and Reg S; their terms are not summarized here.
