# Sietch Vision

> **Version:** 1.2.0
> **Date:** June 2026
> **Status:** Public summary. Subject to refinement as the protocol matures.

> Sietch is a privacy-first payment network. This document explains what it does and why it exists. It is not investment advice. It does not promise any financial return, and it says nothing about token prices or fee volume. You do not need to hold SIETCH to deposit, send, or withdraw money on the network.

## Table of Contents

- [1. The Problem](#1-the-problem)
- [2. The Solution](#2-the-solution)
- [3. Who Sietch Is For](#3-who-sietch-is-for)
- [4. Core Principles](#4-core-principles)
- [5. What Sietch Is Not](#5-what-sietch-is-not)
- [6. Staying Clean Without Asking for Your ID](#6-staying-clean-without-asking-for-your-id)
- [7. Two Tokens, Two Jobs](#7-two-tokens-two-jobs)
- [8. The Name](#8-the-name)
- [9. Path Forward](#9-path-forward)

## 1. The Problem

When you pay someone on most blockchains, the whole world can watch. Your address, their address, and the exact amount are written into a public record that never gets erased. Anyone can read it: your employer, the person you bought a coffee from, a company that sells your spending history, or someone who simply wants to know how much money you have.

Imagine if every time you paid for groceries, the receipt was pinned to a public noticeboard with your name on it forever. That is roughly how today's blockchains work.

People expect their money to be private. Cash is private. A bank transfer is private from the public, even if the bank can see it. Public blockchains are not. That gap is the main reason normal people use crypto to gamble on prices instead of to actually pay for things.

This is not about hiding wrongdoing. It is about a default that was wrong from the very first block: everything visible to everyone, all the time.

## 2. The Solution

Sietch is a separate payment network that connects to the public blockchains people already use. It does one thing, and it tries to do it well: let you move money privately. There are only three steps.

- **Deposit.** You send your coins into a Sietch contract on whatever network they live on.
- **Send.** Inside Sietch, you send a private version of those coins to anyone. The sender, the receiver, and the amount are all hidden.
- **Withdraw.** You take your coins back out to any address on the network you started from.

Behind the scenes, everyone's funds sit together in one shared, hidden pool. When you send money, the network can prove the payment is valid without ever revealing who sent what to whom. That proof is what cryptographers call a **zero-knowledge proof**: a way to prove something is true while keeping the details secret. The classic example is proving you know a password without ever typing it out. Sietch uses the same idea to prove a payment is legitimate without showing the payment.

The private coins inside Sietch are not new assets to speculate on. Each one is backed one-for-one by the real coins locked in the contract you deposited into. Think of it as your money wearing an invisibility cloak while it is inside the network. When you withdraw, the cloak comes off and you get your ordinary coins back.

The first network Sietch supports is Ethereum, where you deposit ETH and it becomes pETH ("private ETH") inside the pool. The same design extends to other blockchains and their assets: Bitcoin, stablecoins like USDT and USDC, and others are planned, each shielded the same way (pBTC, pUSDT, and so on). The privacy machinery in the middle does not change from one network to the next.

There is a small flat fee when you deposit, and no percentage fee when you withdraw. Part of that deposit fee is set aside so that withdrawals can be paid for on your behalf, which means you do not need to keep spare coins around just to get your money out.

## 3. Who Sietch Is For

**Alice** does freelance work and pays **Bob**. She does not want her employer scrolling through a public ledger the next morning and seeing exactly who she paid and how much.

**Bob** receives the payment. He does not want his entire financial life on display to anyone who happens to know his wallet address.

Neither of them is doing anything wrong. They just want the everyday privacy they already get from a bank transfer or a handful of cash. That is the whole point of Sietch.

The same need shows up everywhere:

- A small business paying its suppliers without showing competitors what its costs are.
- Someone donating to a cause without broadcasting that support to the entire internet.
- A company making payroll or vendor payments without leaking its strategy through what flows in and out.
- A shop accepting crypto without publishing its daily sales figures to the world.

Sietch is built for ordinary, legitimate payments. It is not built to help anyone dodge the law.

## 4. Core Principles

| Principle | What it means |
|---|---|
| **Private by default** | Every payment inside Sietch is hidden. There is no privacy setting to switch on and no way to accidentally leave it off. |
| **No ID required** | The network never asks for your name, your documents, or any personal information. It does not have any to leak. |
| **Built to stand up legally** | Open code, a contract that nobody can raid, and built-in screening of deposits. No single company can freeze your money or quietly change the rules. |
| **Payments only** | Sietch is a way to pay people. It is not a trading platform, a lending app, or a place to chase returns. |
| **Secured by math, not by trust** | Your funds are protected by cryptographic proofs that the underlying blockchain itself checks before releasing anything. You do not have to trust an operator to behave. |
| **Open to everyone** | The code is public. Anyone can read it, run part of the network, check the proofs, or build their own version. |

## 5. What Sietch Is Not

- **Not a trading or lending platform.** No swaps, no loans, no yield, no liquidations.
- **Not a general blockchain.** It does not run arbitrary apps. Other networks already do that well.
- **Not a mixer.** A mixer just shuffles coins together to muddy the trail. Sietch is a payment network with clear rules: deposits are screened, and there is a short waiting period before funds become spendable. Same outcome of privacy, very different design and intent.
- **Not a new asset to bet on.** The private coins inside Sietch are always just your deposited coins in disguise, backed one-for-one. SIETCH is a separate token used to run the network, not to pay people.
- **Not a custodian.** No company holds your money. The contract is the only thing in charge of it, and even the team cannot reach in and take it.

## 6. Staying Clean Without Asking for Your ID

Most privacy tools face the same hard question: how do you keep out stolen or sanctioned money without spying on everyone else? Sietch answers it with a feature called **Private Proofs of Innocence**.

The plain-English version: when money enters the network, Sietch can prove that it did not come from a known-bad source, without revealing anything about you. It is like getting a clean bill of health from a doctor that you can show to anyone, while the doctor never tells them a single detail about your visit.

Here is roughly how it works:

1. When you deposit, there is a short waiting period while the public "bad address" lists (maintained by well-known security firms) have a chance to update.
2. The network builds a hidden proof that says, in effect, "this money is not on any of those lists." Your identity is never part of it.
3. As the money moves through later private payments, that clean-history proof travels along with it.
4. When you eventually withdraw, an exchange or business on the other side can check the proof and confirm the funds are clean. They never see your ID, and they do not have to trust any middleman.

Separately, addresses on official sanctions lists are blocked at the front door and cannot get in at all. The waiting period and the choice of which lists to use are decided by the network's governance, not by any one person or company.

The result: people who want privacy get it, and businesses that have to follow the rules can still do their checks.

## 7. Two Tokens, Two Jobs

Sietch uses two separate tokens so that paying and running the network never get tangled up.

- **Shielded coins** (pETH, and later pBTC, pUSDT, and others) are the money you actually spend. Each is your deposited asset made private, always backed one-for-one by the real coins in the contract. You use them to send and receive payments. That is their only job. They do not earn anything and they are not used for voting.
- **SIETCH** is the token that keeps the network running. The operators who do the heavy computation (generating and checking all those proofs) put up SIETCH as a commitment and are paid in SIETCH for that work. People who hold SIETCH can vote on how the network is configured. SIETCH is not money for payments, and you never need it to use Sietch.

Keeping these two apart is deliberate. Mixing "the money I spend" with "the token that governs the system" muddles incentives and creates legal grey areas. Sietch refuses to blur that line.

For details on SIETCH supply, distribution, vesting, governance, and how operators are compensated, see the [Tokenomics](/tokenomics) document.

## 8. The Name

**Sietch** (`SIETCH`) comes from Frank Herbert's novel *Dune*.

In the book, a sietch is a hidden desert community: invisible to outsiders, fiercely guarded by the people who live there, and somehow the foundation of an entire civilization in the harshest place imaginable. Outsiders never stumble onto one. You only find a sietch if someone who belongs there shows you the way.

The network works on the same idea. It is a private place to move money, unseen by outside observers, protected by cryptographic proof instead of desert rock. The open public blockchains are the exposed sand all around it. Sietch is the sheltered space inside, where the things that should stay private actually do.

We are not affiliated with the *Dune* franchise or its owners. The reference is cultural, not commercial.

## 9. Path Forward

Right now Sietch is running on a development network: the contracts, the proof circuits, and the supporting services are all live and being measured. A public test network is in active development. Ethereum is the first network Sietch connects to, so the first real launch will be there, but the privacy layer in the middle is built to plug into other blockchains afterward without being rebuilt. The launch will only happen after the system has passed outside security audits, survived serious attempts to break it, and proven it can run reliably under real load.

The order of priorities does not change:

1. **Keep funds safe.** Solid cryptography, audited code, and a design where nobody can seize your money.
2. **Stay on the right side of the law.** Screened deposits, the proof-of-clean-history system, and a defensible legal footing.
3. **Make it fast and cheap.** Proofs that generate quickly enough that paying with Sietch feels normal.
4. **Spread out control.** More independent operators over time, open onboarding, and no single point of failure.
5. **Reach more networks.** Add support for additional blockchains and assets once the core is proven, so privacy is not tied to any single chain.

For the architecture, the threat model, the details of the proof system, and the roadmap, see the [Whitepaper](/whitepaper). For supply and distribution, see the [Tokenomics](/tokenomics).
