# Sietch Vision

> **Version:** 1.0.0
> **Date:** April 2026
> **Status:** Public summary. Subject to refinement as the protocol matures.

> Sietch is a privacy-first payment network for Ethereum. This document describes the protocol's purpose, scope, and operating principles. It does not constitute investment advice, does not promise financial return, and does not forecast token price or fee volume. Users of the Sietch network do not need to acquire or hold SIETCH to deposit, transfer, or withdraw shielded assets.

## Table of Contents

- [1. The Problem](#1-the-problem)
- [2. The Solution](#2-the-solution)
- [3. Who Sietch Is For](#3-who-sietch-is-for)
- [4. Core Principles](#4-core-principles)
- [5. What Sietch Is Not](#5-what-sietch-is-not)
- [6. Compliance Without Identity Collection](#6-compliance-without-identity-collection)
- [7. Two-Token Design](#7-two-token-design)
- [8. The Name](#8-the-name)
- [9. Path Forward](#9-path-forward)

## 1. The Problem

Public ledgers expose every transfer. Sender address, receiver address, and amount are written in the clear and indexed by block explorers, analytics firms, employers, counterparties, and adversaries. For ordinary payments, that posture is closer to a billboard than to cash or a bank wire.

People expect financial privacy. Cash provides it. Bank transfers provide it. Public blockchains do not. The gap between expectation and reality is the single largest barrier to using cryptocurrency for everyday payments rather than for speculation.

The problem is not bad actors. The problem is that the default has been wrong since the first block.

## 2. The Solution

Sietch is a payment-focused privacy network anchored to Ethereum. The flow is intentionally narrow:

- **Deposit** ETH into the Sietch bridge contract on Ethereum.
- **Send** pETH (private ETH) to anyone inside the Sietch network. Sender, receiver, and amount are hidden.
- **Withdraw** ETH to any Ethereum address along with a cryptographic proof that the funds are not sourced from a screened list.

One unified shielded pool. One click to send. Zero knowledge of who sent what to whom. pETH is always backed 1:1 by ETH held in the non-custodial bridge contract; it is a shielded representation, not a separate asset.

Protocol fees are denominated as a flat deposit charge in the bridge contract. There is no withdrawal percentage fee. A portion of deposit fees funds an exit reserve so withdrawals can be sponsored, removing the need for users to hold gas at exit.

## 3. Who Sietch Is For

**Alice** wants to pay Bob for freelance work without her employer reading the transaction off a block explorer the next morning.

**Bob** wants to receive payment without his entire financial history becoming visible to anyone who looks up his address.

Neither is doing anything illegal. They simply expect the same baseline privacy they would have with a bank transfer or with cash. That is the gap Sietch fills.

The same applies to:

- A small business paying suppliers without disclosing margins to competitors.
- A donor supporting a cause without exposing affiliation to the public internet.
- A treasury making operational payments without revealing strategy from on-chain inflows and outflows.
- A merchant settling in stablecoins without publishing daily revenue to the world.

Sietch is built for these uses. It is not built for evading lawful obligations.

## 4. Core Principles

| Principle | What It Means |
|---|---|
| **Privacy by default** | Every transfer inside Sietch is fully shielded. Sender, receiver, and amount are hidden. There is no opt-in toggle. |
| **No KYC at the protocol** | The protocol does not collect, store, or require any personal identity information. Compliance is achieved cryptographically, not procedurally. |
| **Legally defensible** | Open-source code, a non-custodial bridge, and PPOI for deposit hygiene. No single operator can freeze, censor, or unilaterally upgrade user funds. |
| **Payment-focused** | Sietch is a payment network. Not DeFi, not a general-purpose smart contract platform, not a mixer. |
| **Mathematically trustless** | Fund security is enforced by zero-knowledge proofs verified on Ethereum, not by validators, multisigs, or trust in operators. |
| **Open by construction** | Contracts, circuits, indexers, and infrastructure code are open source. Anyone can run a node, validate proofs, or fork the network. |

## 5. What Sietch Is Not

- **Not a DeFi protocol.** No swaps, no lending, no yield farming, no liquidations.
- **Not a general-purpose smart contract platform.** That space is well-served by other networks.
- **Not a mixer.** Sietch is a network with explicit rules, screened deposits, and standby periods. Tornado Cash was a mixer; Sietch is a payment rail with cryptographic compliance.
- **Not a new asset.** pETH is always backed 1:1 by ETH in the bridge contract. SIETCH is a separate utility token used for validator staking, governance voting, and validator compensation; it is not a payment token.
- **Not a custodian.** The bridge contract is non-custodial. There is no operator who can freeze, seize, or redirect user balances.

## 6. Compliance Without Identity Collection

Sietch implements **Private Proofs of Innocence (PPOI)**: a cryptographic compliance layer that screens deposits against well-known list providers (Chainalysis, Elliptic, SlowMist, and others) without disclosing identity.

The flow:

1. A deposit enters a standby period while list providers update their datasets.
2. A blinded zero-knowledge proof is constructed asserting the deposit is not associated with screened addresses.
3. The proof follows the tokens through subsequent shielded transfers via recursive verification.
4. At withdrawal, an exchange or counterparty can verify the proof without seeing identity documents and without relying on a centralized intermediary.

OFAC-sanctioned addresses are screened at the bridge contract level and cannot enter the pool. The standby period and list-provider hooks are configurable by governance, not by any single operator.

This design lets Sietch serve users who require privacy while preserving the ability of regulated counterparties to perform their own compliance checks.

## 7. Two-Token Design

Sietch uses two distinct tokens with non-overlapping roles:

- **pETH** — shielded ETH. The unit of payment inside the network. Always backed 1:1 by ETH in the bridge contract. Holders use pETH to send and receive value. pETH is not staked, not governed, and not yield-bearing.
- **SIETCH** — utility and governance. Validators stake SIETCH to participate in network operation; SIETCH holders vote on protocol parameters; validators are compensated in SIETCH for the computational work of generating and verifying proofs. SIETCH is not a payment token and is not required to use the network.

The split is intentional. Confusing payment value with governance value pushes incentives in the wrong direction and creates regulatory ambiguity. Sietch keeps them separate.

For details on SIETCH supply, allocation, vesting, governance, and validator compensation, see the [Tokenomics](/tokenomics) document.

## 8. The Name

**Sietch** (`SIETCH`), from Frank Herbert's *Dune*.

A sietch is a hidden Fremen cave community: invisible to outsiders, fiercely protected by its inhabitants, and the foundation on which an entire civilization was built in the most hostile environment in the known universe. Nobody finds a sietch unless a Fremen shows them the way.

The Sietch network operates on the same principle. A private space for value transfer, invisible to outside observers, protected by cryptographic proof instead of desert rock. The sand around it is the public Ethereum chain; the network inside is a quieter place where the things that should be private actually are.

We are not affiliated with the *Dune* franchise or its licensors; the reference is cultural, not commercial.

## 9. Path Forward

The current phase is devnet: contracts, circuits, indexer, and watcher are operational and instrumented. Testnet is in active development. Mainnet TGE will happen once the system has passed third-party audits, sustained meaningful adversarial review, and demonstrated stable operation under load.

The order of priorities never changes:

1. **Safety of funds.** Cryptographic primitives, audited circuits, formally specified bridge logic, and a non-custodial design.
2. **Compliance posture.** PPOI integration, screened deposits, and a defensible legal framing for the operating entity.
3. **Performance.** Proof generation cost and latency that make payments feel ordinary.
4. **Decentralization.** Validator set growth, permissionless onboarding, and a credible exit for any single operator.

For the architecture, threat model, proof-system details, and roadmap milestones, see the [Whitepaper](/whitepaper). For supply and distribution mechanics, see the [Tokenomics](/tokenomics).
