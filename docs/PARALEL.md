# PARALEL

**A transparent, on-chain auction platform for real-world assets.**

PARALEL is a Web3 auction prototype designed to make public auctions of physical assets more transparent, verifiable, and accessible. PARALEL combines off-chain custody and document verification with on-chain bidding, escrow, ranking, awarding, refunds, and settlement.

> **Project status:** Active prototype on Arbitrum Sepolia testnet. PARALEL is not yet a production financial service, marketplace operator, custodian, legal service, or tax service.

## Vision

Traditional auctions of physical assets often depend on fragmented records, limited visibility, and manual reconciliation between bidders, asset custodians, document reviewers, and auction operators.

PARALEL explores a hybrid model in which:

- physical custody and inspection remain off-chain;
- document and legal checks remain off-chain;
- auction rules and approvals are represented through verifiable records;
- bids and bidder stakes are handled by a smart contract;
- auction ranking and award progression are transparent;
- refunds and settlement follow deterministic rules.

The objective is not to move a physical asset onto a blockchain. The objective is to create a verifiable coordination and settlement layer around an auction involving a physical asset.

## Core Principles

### Transparent auction execution

On-chain activity provides a verifiable record of bidding, ranking, award progression, withdrawals, and settlement.

### Non-custodial user interaction

Users interact through their own wallets. Auction funds are handled by the smart contract according to the auction lifecycle rather than being held in a conventional platform account.

### Physical-world verification remains explicit

A blockchain cannot independently inspect a vehicle, verify a property document, or physically transfer an item. PARALEL therefore keeps custody, inspection, documentation, collection, and dispute handling within clearly defined off-chain responsibilities.

### Immutable auction snapshots

An auction uses the configuration recorded for that auction. Later platform-level configuration changes must not silently change the economic rules of an auction that has already been registered.

### Separation of authority

Operational services may coordinate application workflows, but they must not obtain unilateral control over participant funds.

## Participants

### Consignor

The consignor submits a physical asset for auction and provides the required asset information and supporting documents.

### Guarantor

The guarantor handles physical custody and inspection, confirms relevant physical milestones, and supports the collection process.

### Notary

The notary reviews the required documentation and legal or administrative readiness of an auction before it proceeds.

### Bidder

A bidder connects a wallet, participates in an eligible auction, and places bids backed by funds committed through the smart contract.

### Platform Administrator

The public prototype limits platform administration to controlled operational areas related to partner management, the tax wallet, and user administration. Financial authorization and auction settlement remain governed by the backend and smart-contract rules.

## Auction Lifecycle

A PARALEL auction moves through a structured lifecycle.

```text
CREATED
  -> PENDING
  -> REJECTED | CANCELED | SCHEDULED
  -> OPEN
  -> CLOSED
  -> AWARDING
  -> COLLECTION
  -> CLAIM_PERIOD
  -> SETTLED
```

Additional outcomes include:

- **PASSED_IN** when no eligible candidate completes the award process;
- **WITHDRAWN** when an eligible auction is withdrawn under the applicable rules;
- a new round when an auction is reused after an eligible prior outcome.

Some displayed statuses are time-derived. For example, an auction becomes effectively open or closed according to its configured schedule even when the underlying record remains anchored to the same auction round.

## Bidding Model

PARALEL uses cumulative bidding:

- each bidder builds a cumulative bid position;
- the highest cumulative position becomes the current leading bid;
- equal cumulative bids are ordered by which bidder reached the amount first;
- the contract maintains the leading ranks required by the award process;
- committed bid funds remain subject to the auction rules until they become refundable or are settled.

The prototype is designed around USDC-denominated auctions on Arbitrum Sepolia.

## Awarding and Default

Closing an auction does not immediately transfer the asset to the highest bidder. PARALEL uses a sequential award process:

1. the highest eligible candidate is invited to complete the award requirement;
2. the candidate receives a limited signing window;
3. successful completion moves the auction to collection;
4. failure moves the process to the next eligible candidate;
5. applicable default rules are applied to a candidate who fails the award requirement;
6. if no candidate completes the process, the auction becomes passed in.

This structure allows the auction to continue deterministically without privately renegotiating the ranking after the bidding period has ended.

## Collection and Settlement

After a successful award:

- the winner completes the physical collection process with the guarantor;
- the collection milestone is recorded;
- the applicable claim period begins;
- settlement distributes the winning stake according to the auction's immutable fee snapshot;
- eligible non-winning bidders can withdraw refundable balances according to their final position and auction state.

Physical handover, asset condition, legal transfer, and disputes remain real-world processes. PARALEL records and coordinates relevant milestones but does not claim that a smart contract can replace the necessary physical and legal procedures.

## Economic Model

The current prototype settlement model allocates the winning stake as follows:

| Recipient | Share |
|---|---:|
| Platform | 2.5% |
| Guarantor | 1.5% |
| Notary | 1.0% |
| Tax wallet | 10.0% |
| Consignor | 85.0% |

The current prototype also includes:

- a default fee applied when an awarded candidate fails the required award step;
- a fixed withdrawal fee for applicable withdrawals, capped by the available gross amount;
- currency-specific claimable balances;
- auction-specific snapshots so active auctions are not silently modified by later configuration changes.

These values describe the current testnet prototype and may change before any production launch, subject to legal, tax, security, and business review.

## On-Chain and Off-Chain Boundaries

### On-chain

- auction registration and round state;
- cumulative bid positions;
- bidder stake accounting;
- leading-rank maintenance;
- award progression;
- default handling;
- refundable balances;
- claimable balances;
- settlement distribution;
- document anchoring references.

### Off-chain

- identity and role administration;
- physical custody and inspection;
- document review;
- asset photos and supporting files;
- user-facing auction metadata;
- notifications and operational workflows;
- physical collection records;
- dispute handling;
- indexing and presentation of contract events.

The off-chain application projects and explains blockchain state, but it must not silently redefine finalized on-chain outcomes.

## Public Application Areas

The prototype includes public and role-based application areas for:

- auction discovery;
- auction details;
- wallet-based registration and sign-in;
- user dashboards;
- bidding and auction participation;
- a user's auction activity;
- guarantor workflows;
- notary workflows;
- restricted platform administration;
- collection and receipt workflows.

Availability may vary while the testnet prototype is under active development.

## Security Model

PARALEL follows several prototype security boundaries:

- participant funds are governed by smart-contract rules;
- privileged application features require role authorization;
- signed actions are bound to their intended operation and context;
- repeated requests use idempotency controls where required;
- auction economics are snapshotted for registered auctions;
- indexing must tolerate duplicate delivery and blockchain reorganization;
- secrets and signing keys are not part of the public frontend;
- public application code must not be treated as an authorization boundary.

The prototype has not been represented as having completed an independent production smart-contract or application security audit.

## Deliberate Prototype Boundaries

The current design does not silently add mechanisms that have not been approved for the prototype. In particular, the current scope does not claim support for:

- on-chain dispute adjudication;
- emergency withdrawal controlled by the platform;
- an automatic fallback consignor;
- anti-sniping extensions;
- shill-bidding detection;
- blockchain-managed physical delivery;
- production-grade KYC, AML, legal, or tax compliance.

These are material product and governance decisions, not minor interface features.

## Testnet Notice

PARALEL currently operates as a prototype on Arbitrum Sepolia. Testnet assets have no intended monetary value. Features, addresses, interfaces, rules, and data may be reset or changed during development.

Do not use the prototype for real asset transfers, real-money auctions, legal title transfer, tax reporting, custody commitments, or investment decisions.

## License

Refer to the repository's `LICENSE` file. If no license is present, no permission should be assumed beyond viewing the publicly available source code.

---

**PARALEL is an experimental testnet prototype. Nothing in this repository constitutes financial, legal, tax, custody, or investment advice.**
