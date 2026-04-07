# EYEKON Protocol

## The Open Standard for Decentralized Digital Identity and Verifiable Credentials

**Version 1.0 — April 2026**

---

## Abstract

Digital identity on the internet remains fundamentally broken. Despite decades of progress in cryptography, distributed systems, and blockchain technology, no single protocol has emerged to unify the fragmented landscape of identity management, credential verification, and reputation tracking. Existing solutions — from W3C Decentralized Identifiers (DIDs) and Verifiable Credentials (VCs) to Soulbound Tokens (SBTs) and platform-specific approaches like ENS and Worldcoin — each solve a narrow slice of the problem while introducing new forms of vendor lock-in, technical complexity, or incomplete functionality.

EYEKON Protocol is an open-source, composable protocol for decentralized digital identity that unifies identity registration, credential issuance and verification, reputation scoring, and a novel concept we call the **Evolution Timeline** — a permanent, append-only record of how an identity grows and changes over time. Built on EVM-compatible blockchains, EYEKON Protocol provides a complete stack: smart contracts, a TypeScript SDK, a subgraph indexer, a REST API gateway, and a public verification service.

The protocol is designed so that anyone can implement it. EYEKON (eyekonit.com) serves as the first and reference implementation — the "Chrome" to the protocol's "HTTP." This white paper presents the protocol's design, architecture, technical specification, competitive positioning, monetization framework, and phased roadmap for development and adoption.

---

## Table of Contents

1. Introduction
2. The Problem: A Fragmented Identity Landscape
3. Design Philosophy
4. Protocol Architecture
5. Core Smart Contracts
6. The Evolution Timeline
7. Reputation System
8. SDK and Developer Experience
9. Subgraph and Data Indexing
10. Verification and Trust
11. Competitive Analysis
12. Use Cases
13. Monetization and Sustainability
14. Governance
15. Security Model
16. Roadmap
17. Conclusion
18. References

---

## 1. Introduction

### 1.1 The Identity Crisis

The internet was built without an identity layer. Protocols like TCP/IP, HTTP, and SMTP were designed to move packets, documents, and messages — not to answer the question "who are you?" This architectural gap has been filled, over the past three decades, by centralized identity providers: governments issuing passports, corporations issuing employee badges, universities issuing diplomas, and platform companies issuing usernames and passwords.

Each of these systems is siloed. A LinkedIn profile cannot verify a university degree. A passport cannot prove employment history. A GitHub contribution graph cannot serve as a professional credential in a DAO governance vote. The result is a world where identity is fragmented across dozens of incompatible systems, each controlled by a different authority, each with its own verification process, and each vulnerable to a different set of failures.

### 1.2 The Blockchain Opportunity

Blockchain technology introduced a paradigm shift: the ability to create tamper-proof, publicly verifiable records without a central authority. This is precisely what identity needs — a shared, neutral infrastructure where credentials can be issued by any authority, held by any individual, and verified by any party, without requiring trust in a single intermediary.

Yet the blockchain identity space remains fragmented. The W3C published standards for Decentralized Identifiers (DIDs) and Verifiable Credentials (VCs), but these remain primarily specifications without dominant implementations. Vitalik Buterin proposed Soulbound Tokens (SBTs) as non-transferable identity primitives, but no protocol has standardized their issuance and verification. Platform-specific solutions like Ethereum Name Service (ENS), Lens Protocol, and Worldcoin each address narrow subsets of the identity problem.

### 1.3 EYEKON Protocol: The Missing Standard

EYEKON Protocol fills this gap by providing a complete, open, composable standard for decentralized digital identity. Rather than solving one piece of the puzzle, the protocol provides an integrated stack that handles the full identity lifecycle: creation, credentialing, evolution, reputation, and verification.

The protocol follows a "protocol-first" philosophy. Just as HTTP is a standard that anyone can implement (with Chrome, Firefox, and Safari as implementations), and ERC-20 is a token standard that anyone can deploy (with USDT, USDC, and DAI as implementations), EYEKON Protocol is an identity standard that anyone can build on. The EYEKON application at eyekonit.com is the first and reference implementation — but it is explicitly not the only one.

---

## 2. The Problem: A Fragmented Identity Landscape

### 2.1 The Current State of Digital Identity

Digital identity today is characterized by fragmentation, centralization, and incompleteness. To understand why EYEKON Protocol is necessary, it helps to examine the existing landscape in detail.

**Centralized Identity Providers.** The vast majority of digital identity today flows through centralized providers: Google, Apple, Facebook, and government agencies. These systems are efficient but fragile. A single account suspension can erase years of digital history. Data breaches expose millions of records simultaneously. And users have no meaningful ownership of or sovereignty over their identity data.

**W3C Decentralized Identifiers (DIDs).** The W3C published the DID specification in 2022, defining a standard for decentralized, self-sovereign identifiers. DIDs are an important conceptual advance, but adoption has been limited. The specification is complex, implementations are fragmented across dozens of "DID methods," and there is no dominant developer toolkit that makes DIDs easy to use in practice. Most DID implementations remain enterprise-focused and difficult for individual developers to integrate.

**W3C Verifiable Credentials (VCs).** The companion VC specification defines a standard for cryptographically signed credentials that can be verified without contacting the issuer. Like DIDs, VCs are conceptually sound but practically underdeveloped. The ecosystem is dominated by enterprise vendors selling expensive, closed-source solutions. The average developer cannot issue or verify a VC without navigating a complex maze of libraries, standards, and infrastructure.

**Soulbound Tokens (SBTs).** Introduced by Vitalik Buterin, Glen Weyl, and Puja Ohlhaver in their 2022 paper "Decentralized Society: Finding Web3's Soul," SBTs are non-transferable tokens that represent commitments, credentials, and affiliations. The concept resonated widely, but no standard has emerged. SBT implementations are scattered across individual projects with incompatible interfaces, no shared verification infrastructure, and no mechanism for credential revocation or evolution.

**Platform-Specific Solutions.** ENS provides human-readable names for Ethereum addresses but does not handle credentials or reputation. Lens Protocol provides social identity within its own ecosystem but is not a general-purpose identity standard. Worldcoin provides proof-of-humanity through iris scanning but does not handle the broader credential and reputation lifecycle.

### 2.2 What's Missing

The common thread across all existing solutions is incompleteness. No single protocol handles the full identity lifecycle:

- **Creation**: Minting a unique, self-sovereign digital identity
- **Credentialing**: Issuing, holding, and presenting verifiable credentials
- **Evolution**: Recording how an identity grows and changes over time
- **Reputation**: Aggregating on-chain activity into a meaningful trust score
- **Verification**: Providing a simple, universal mechanism for any party to verify any credential

EYEKON Protocol addresses all five of these dimensions in a single, composable stack.

### 2.3 The Cost of Fragmentation

The fragmentation of digital identity is not merely an inconvenience — it creates real economic and social costs.

**For individuals**, fragmentation means maintaining dozens of accounts, repeatedly proving the same credentials, and losing identity data when platforms shut down or accounts are suspended.

**For organizations**, fragmentation means building custom verification pipelines for each type of credential, paying multiple vendors for identity services, and accepting the liability of storing sensitive identity data.

**For developers**, fragmentation means navigating an alphabet soup of standards (DID, VC, SBT, ERC-721, ERC-1155, ERC-4337) with no clear path to a unified implementation.

**For the ecosystem**, fragmentation means slower adoption of decentralized identity overall, as potential users and builders are deterred by complexity and lack of interoperability.

---

## 3. Design Philosophy

EYEKON Protocol is guided by five core principles that inform every architectural and design decision.

### 3.1 Open by Default

The protocol specification, smart contracts, SDK, subgraph, and documentation are all open-source under permissive licenses (MIT for code, CC-BY for documentation). Anyone can implement, extend, fork, or build on the protocol without permission or payment.

This is not altruism — it is strategy. Open protocols win by becoming standards. TCP/IP won because it was open. HTTP won because it was open. ERC-20 won because it was open. EYEKON Protocol aims to win the same way.

### 3.2 Composable and Modular

The protocol is designed as a set of independent, composable modules rather than a monolithic system. The Identity Registry can be used without the Credential Engine. The Credential Engine can be used without the Evolution Timeline. Each module exposes clean interfaces (Solidity interfaces prefixed with `I`) that any implementation must satisfy.

This composability means that adopters can use exactly the pieces they need, and that the protocol can evolve over time without breaking backward compatibility.

### 3.3 Developer-First

The protocol prioritizes developer experience above all else. The TypeScript SDK allows developers to create an identity, issue a credential, and verify it in three to five lines of code. The REST API gateway provides an alternative for teams that prefer not to interact with the blockchain directly. Comprehensive documentation, examples, and tutorials lower the barrier to entry.

The thesis is simple: protocols win through developer adoption. If building on EYEKON Protocol is easier than building a custom solution, developers will choose the protocol.

### 3.4 Chain-Agnostic (EVM-First)

The protocol is designed for deployment on any EVM-compatible blockchain. The initial deployment targets Polygon (for low transaction costs and fast finality), but the contracts are compatible with Ethereum, Base, Arbitrum, Optimism, Avalanche, BNB Chain, and any other EVM chain.

Future versions of the protocol may extend to non-EVM chains through bridge contracts and cross-chain messaging, but the EVM ecosystem is the initial focus given its dominant developer community and infrastructure.

### 3.5 Identity Evolves

The most distinctive principle of EYEKON Protocol is the belief that identity is not static — it evolves. A university degree is issued once, but a professional reputation is built over years. A company is founded on a specific date, but its track record grows with every project completed.

This principle is embodied in the Evolution Timeline, a first-of-its-kind on-chain construct that records the growth of an identity over time. The Evolution Timeline is what makes EYEKON Protocol fundamentally different from every existing identity solution.

---

## 4. Protocol Architecture

### 4.1 Three-Layer Design

EYEKON Protocol is organized into three distinct layers, each with a clear responsibility:

```
┌─────────────────────────────────────────────────────┐
│  LAYER 3: APPLICATION                                │
│  EYEKON app, third-party apps, wallets, DAOs,        │
│  enterprise portals, government services              │
├─────────────────────────────────────────────────────┤
│  LAYER 2: PROTOCOL (open-source)                     │
│  ┌──────────────┐  ┌──────────────┐                  │
│  │  Identity     │  │  Credential  │                  │
│  │  Registry     │  │  Engine      │                  │
│  ├──────────────┤  ├──────────────┤                  │
│  │  Evolution    │  │  Reputation  │                  │
│  │  System       │  │  Oracle      │                  │
│  ├──────────────┤  ├──────────────┤                  │
│  │  Verification │  │  Access      │                  │
│  │  Oracle       │  │  Control     │                  │
│  └──────────────┘  └──────────────┘                  │
├─────────────────────────────────────────────────────┤
│  LAYER 1: BLOCKCHAIN                                 │
│  Polygon, Ethereum, Base, Arbitrum, any EVM chain    │
└─────────────────────────────────────────────────────┘
```

**Layer 1: Blockchain.** The settlement and data availability layer. EYEKON Protocol does not operate its own blockchain — it deploys on existing EVM-compatible chains, leveraging their security, decentralization, and infrastructure.

**Layer 2: Protocol.** The core logic layer, consisting of smart contracts that define how identities are created, credentials are issued and verified, timelines evolve, and reputations are calculated. This layer is the protocol itself — the open-source standard that anyone can implement.

**Layer 3: Application.** The user-facing layer where applications interact with the protocol. EYEKON (eyekonit.com) is the reference application, but any application can interact with the protocol through the SDK, REST API, or direct smart contract calls.

### 4.2 Data Flow

A typical interaction with the protocol follows this path:

1. A **user** interacts with an **application** (Layer 3)
2. The application calls the **SDK** or **REST API** (Layer 2 interface)
3. The SDK constructs and submits a **transaction** to the smart contracts (Layer 2 core)
4. The transaction is confirmed on the **blockchain** (Layer 1)
5. The **subgraph** indexes the event for efficient querying
6. The application reads the updated state through the subgraph or direct contract calls

### 4.3 Key Design Decisions

**Why EVM?** The Ethereum Virtual Machine has the largest developer community, the most mature tooling (Hardhat, Foundry, ethers.js, viem), and the widest deployment across L1 and L2 chains. Building on EVM maximizes the protocol's addressable developer base.

**Why not a standalone chain?** Running a separate blockchain introduces bootstrap problems (validator recruitment, token distribution, bridge security) that distract from the core mission of identity standardization. Deploying on existing chains lets the protocol inherit their security and network effects.

**Why Polygon first?** Polygon offers sub-cent transaction costs, two-second block times, and Ethereum-compatible security through its proof-of-stake consensus. These properties make it ideal for identity operations, which should be inexpensive and fast.

---

## 5. Core Smart Contracts

### 5.1 Contract Overview

The protocol consists of six core smart contracts, each responsible for a distinct function:

| Contract | Purpose | Standard |
|---|---|---|
| `IdentityRegistry.sol` | Mint and manage digital identities | ERC-721 + ERC-1155 |
| `CredentialEngine.sol` | Issue, verify, and revoke credentials | Custom + ERC-1155 |
| `EvolutionTimeline.sol` | Append-only identity growth record | Custom |
| `ReputationOracle.sol` | On-chain reputation aggregation | Custom |
| `AccessControl.sol` | Role-based permissions | OpenZeppelin RBAC |
| `PaymentSplitter.sol` | Protocol fee distribution | Custom |

### 5.2 IdentityRegistry

The IdentityRegistry is the foundation of the protocol. It manages the creation, storage, and retrieval of digital identities.

**Identity Model.** Each identity is represented as a non-fungible token (NFT) conforming to the ERC-721 standard, with optional ERC-1155 extensions for batch operations. An identity has the following on-chain properties:

```solidity
struct Identity {
    uint256 id;              // Unique identifier
    address owner;           // Controlling wallet address
    string metadataURI;      // Off-chain metadata (IPFS/Arweave)
    uint256 createdAt;       // Block timestamp of creation
    IdentityType idType;     // INDIVIDUAL, ORGANIZATION, or ENTITY
    bool transferable;       // Whether the identity can be transferred
    bool active;             // Whether the identity is currently active
}
```

**Identity Types.** The protocol supports three identity types: `INDIVIDUAL` (a person), `ORGANIZATION` (a company, university, DAO, or government), and `ENTITY` (a device, bot, or abstract entity). Each type may have different rules for credential issuance and reputation calculation.

**Transferability.** Unlike pure Soulbound Tokens, EYEKON Protocol allows identity creators to choose whether their identity is transferable or non-transferable. This flexibility supports use cases where identity transfer is legitimate (e.g., company acquisitions) while preserving the non-transferability needed for personal credentials.

**Key Interface:**

```solidity
interface IIdentityRegistry {
    function mintIdentity(
        address owner,
        string calldata metadataURI,
        IdentityType idType,
        bool transferable
    ) external returns (uint256 identityId);

    function getIdentity(uint256 identityId)
        external view returns (Identity memory);

    function deactivateIdentity(uint256 identityId) external;

    function updateMetadata(
        uint256 identityId,
        string calldata newMetadataURI
    ) external;

    event IdentityMinted(
        uint256 indexed identityId,
        address indexed owner,
        IdentityType idType
    );
    event IdentityDeactivated(uint256 indexed identityId);
    event MetadataUpdated(uint256 indexed identityId, string newURI);
}
```

### 5.3 CredentialEngine

The CredentialEngine handles the full lifecycle of verifiable credentials: issuance, verification, revocation, and expiration.

**Credential Model.** Each credential is a structured record linking an issuer identity to a subject identity, with a specific claim, an optional expiration, and a revocation status.

```solidity
struct Credential {
    uint256 id;              // Unique credential ID
    uint256 issuerId;        // Identity of the issuer
    uint256 subjectId;       // Identity of the subject
    bytes32 credentialType;  // Hashed type (e.g., "DEGREE", "EMPLOYMENT")
    bytes32 claimHash;       // Hash of the credential claim data
    string metadataURI;      // Off-chain credential details
    uint256 issuedAt;        // Timestamp of issuance
    uint256 expiresAt;       // Expiration timestamp (0 = no expiry)
    bool revoked;            // Revocation status
}
```

**Credential Types.** The protocol defines a set of standard credential types (DEGREE, EMPLOYMENT, CERTIFICATION, MEMBERSHIP, ACHIEVEMENT, KYC, KYB) while allowing custom types for specific use cases.

**Delegation.** The CredentialEngine supports delegation, allowing an identity to authorize another identity to issue credentials on its behalf. For example, a university (the delegator) might authorize its registrar's office (the delegate) to issue degree credentials.

**Key Interface:**

```solidity
interface ICredentialEngine {
    function issueCredential(
        uint256 issuerId,
        uint256 subjectId,
        bytes32 credentialType,
        bytes32 claimHash,
        string calldata metadataURI,
        uint256 expiresAt
    ) external returns (uint256 credentialId);

    function verifyCredential(uint256 credentialId)
        external view returns (bool valid, Credential memory credential);

    function revokeCredential(uint256 credentialId) external;

    function delegateIssuance(
        uint256 issuerId,
        uint256 delegateId,
        bytes32 credentialType
    ) external;

    event CredentialIssued(
        uint256 indexed credentialId,
        uint256 indexed issuerId,
        uint256 indexed subjectId
    );
    event CredentialRevoked(uint256 indexed credentialId);
}
```

### 5.4 AccessControl

The AccessControl contract implements role-based permissions for the protocol. It defines four standard roles:

- **Admin**: Can configure protocol parameters, pause/unpause contracts, and manage roles.
- **Issuer**: Can issue and revoke credentials. Must be registered in the IdentityRegistry.
- **Verifier**: Can query credential validity. Open to any address by default.
- **Oracle**: Can submit external verification data (e.g., KYC results).

The contract extends OpenZeppelin's AccessControl with protocol-specific modifiers and a registration process for issuers.

### 5.5 PaymentSplitter

The PaymentSplitter manages protocol fees and their distribution. When a credential is issued, a configurable fee (denominated in the chain's native token or a stablecoin) is collected and split between the protocol treasury and the credential issuer.

Fee parameters are configurable by the Admin role and can be set to zero for specific credential types or issuers (e.g., to subsidize early adoption).

---

## 6. The Evolution Timeline

### 6.1 Concept

The Evolution Timeline is EYEKON Protocol's most distinctive feature and its primary technical innovation. It is an append-only, chronological record of milestones, achievements, and credential events associated with a specific identity.

Think of it as a blockchain-native resume that builds itself automatically. When a university issues a degree credential, an entry is added to the subject's Evolution Timeline. When an employer adds an employment credential, another entry appears. When a project is shipped, a community recognition credential is issued, a DAO membership is granted — each event becomes a permanent node in the timeline.

No existing identity protocol offers this functionality. W3C VCs are point-in-time attestations with no temporal relationship. SBTs are isolated tokens with no built-in sequencing. EYEKON Protocol's Evolution Timeline is the first on-chain construct that captures the narrative arc of an identity over time.

### 6.2 Data Model

```solidity
struct TimelineEntry {
    uint256 id;              // Entry ID
    uint256 identityId;      // Associated identity
    uint256 credentialId;    // Linked credential (0 if standalone)
    bytes32 entryType;       // MILESTONE, ACHIEVEMENT, CREDENTIAL, CHAPTER
    string title;            // Human-readable title
    string metadataURI;      // Detailed description and media
    uint256 timestamp;       // When the event occurred
    uint256 addedAt;         // When the entry was recorded on-chain
    address addedBy;         // Who added the entry
}
```

### 6.3 Entry Types

The Evolution Timeline supports four entry types:

**CREDENTIAL**: Automatically generated when a credential is issued to or by the identity. These entries are system-generated and cannot be manually created or modified.

**MILESTONE**: A significant event in the identity's history, such as "Founded Company X" or "Published Paper Y." Milestones can be self-attested or attested by a third party.

**ACHIEVEMENT**: A recognition or accomplishment, such as "Completed Hackathon Z" or "Reached 1000 Contributions." Achievements are typically attested by the organizing entity.

**CHAPTER**: A temporal grouping that organizes timeline entries into periods, such as "University Years (2020-2024)" or "Series A Phase (2024-2025)." Chapters provide narrative structure to the timeline.

### 6.4 Append-Only Guarantee

The Evolution Timeline is strictly append-only. Once an entry is recorded, it cannot be modified or deleted. This immutability is enforced at the smart contract level and is essential to the timeline's value as a trustworthy record.

If a credential is revoked, the original credential entry remains in the timeline, and a new entry of type CREDENTIAL is appended recording the revocation. This preserves the full history while accurately reflecting the current state.

### 6.5 Timeline Queries

The Evolution Timeline supports efficient queries through the subgraph:

- **Full timeline**: All entries for an identity, sorted chronologically
- **By type**: Filter entries by CREDENTIAL, MILESTONE, ACHIEVEMENT, or CHAPTER
- **By time range**: Entries within a specific date range
- **By credential type**: All credential-related entries of a specific type (e.g., all EMPLOYMENT credentials)
- **By attester**: All entries attested by a specific identity

### 6.6 Why This Matters

The Evolution Timeline transforms identity from a static snapshot into a dynamic narrative. Consider the difference:

**Without Evolution Timeline**: "This person has a degree from MIT and works at Google." Two isolated facts, no context, no progression.

**With Evolution Timeline**: "This person studied CS at MIT (2018-2022), interned at a startup during summers, graduated with honors, joined Google as a junior engineer, shipped three major features, was promoted to senior engineer, and recently began contributing to an open-source AI project." A complete, verifiable story of growth.

This richer identity model unlocks use cases that are impossible with existing protocols, from nuanced reputation assessment to automated credential pathways (e.g., "grant senior developer status to anyone with 5+ years of verified employment and 3+ open-source contributions").

---

## 7. Reputation System

### 7.1 Design Goals

The ReputationOracle computes a composite reputation score for each identity based on their on-chain activity, credential history, and Evolution Timeline. The system is designed to be:

- **Transparent**: The scoring algorithm is open-source and deterministic
- **Composable**: Different applications can weight factors differently
- **Sybil-resistant**: Score calculation incorporates anti-gaming mechanisms
- **Contextual**: Reputation can be scoped to specific domains (e.g., "developer reputation" vs. "academic reputation")

### 7.2 Scoring Model

The reputation score is a weighted composite of several on-chain signals:

```
ReputationScore = w1 * CredentialScore
                + w2 * TimelineScore
                + w3 * ActivityScore
                + w4 * EndorsementScore
                + w5 * ConsistencyScore
```

**CredentialScore**: Based on the number, type, and quality of credentials. Credentials from verified issuers carry more weight. Expired or revoked credentials reduce the score.

**TimelineScore**: Based on the length, density, and diversity of the Evolution Timeline. A timeline with entries spanning multiple years and multiple domains scores higher than a sparse or narrow timeline.

**ActivityScore**: Based on on-chain interactions with the protocol, including credential verifications performed, credentials issued (for issuer identities), and protocol governance participation.

**EndorsementScore**: Based on endorsements received from other identities, weighted by the endorser's own reputation (similar to PageRank).

**ConsistencyScore**: Based on the consistency and coherence of the identity's credential and timeline data. Identities with logically consistent histories (e.g., employment dates that don't overlap impossibly) score higher.

### 7.3 Domain-Specific Reputation

Applications can request reputation scores scoped to specific domains by adjusting the weight vector. For example:

- A hiring platform might weight CredentialScore (employment, education) heavily
- A DAO governance system might weight ActivityScore and EndorsementScore heavily
- An academic journal might weight CredentialScore (publications, peer reviews) heavily

The protocol provides default weight vectors for common domains while allowing applications to define custom vectors.

### 7.4 Anti-Gaming Mechanisms

Reputation systems are inherently vulnerable to gaming. The protocol employs several countermeasures:

- **Issuer verification**: Credentials from unverified issuers carry minimal weight
- **Time decay**: Recent activity contributes more to the score than historical activity
- **Diminishing returns**: The marginal value of each additional credential decreases logarithmically
- **Graph analysis**: The endorsement graph is analyzed for suspicious patterns (e.g., circular endorsement rings)
- **Stake requirements**: Issuers must stake tokens to issue credentials, creating an economic cost to spam

---

## 8. SDK and Developer Experience

### 8.1 Design Principles

The `@eyekon/sdk` TypeScript package is the primary developer interface to the protocol. It is designed around three principles:

1. **Three-line operations**: The most common operations (create identity, issue credential, verify credential) should require no more than three to five lines of code.
2. **Framework agnostic**: The SDK works with any JavaScript/TypeScript environment — React, Vue, Angular, Node.js, Deno, or plain browser JavaScript.
3. **Provider flexible**: The SDK supports ethers.js, viem, and wagmi out of the box, with an adapter pattern for other providers.

### 8.2 Quick Start

```typescript
import { EyekonSDK } from "@eyekon/sdk";

// Initialize
const eyekon = new EyekonSDK({
  chainId: 137,  // Polygon
  provider: window.ethereum,
});

// Create an identity
const identity = await eyekon.createIdentity({
  type: "INDIVIDUAL",
  metadata: { name: "Alice", bio: "Software Engineer" },
});

// Issue a credential
const credential = await eyekon.issueCredential({
  issuerId: universityId,
  subjectId: identity.id,
  type: "DEGREE",
  claim: { degree: "BSc Computer Science", honors: "summa cum laude" },
  expiresAt: null,  // No expiration
});

// Verify a credential
const result = await eyekon.verifyCredential(credential.id);
console.log(result.valid);  // true
```

### 8.3 SDK Modules

The SDK is organized into modules that mirror the protocol's smart contracts:

- `eyekon.identity` — Create, read, update, deactivate identities
- `eyekon.credentials` — Issue, verify, revoke, query credentials
- `eyekon.timeline` — Read and add entries to Evolution Timelines
- `eyekon.reputation` — Query reputation scores
- `eyekon.verify` — Standalone verification utilities

### 8.4 Gasless Transactions

The SDK supports meta-transactions (EIP-2771) for gasless user experiences. Applications can sponsor gas costs so that end users never need to hold native tokens. This is critical for mainstream adoption — most users should not need to understand gas fees to use the protocol.

### 8.5 Event Subscriptions

The SDK provides real-time event subscriptions for monitoring protocol activity:

```typescript
eyekon.on("CredentialIssued", (event) => {
  console.log(`New credential ${event.credentialId} issued`);
});

eyekon.on("TimelineUpdated", (event) => {
  console.log(`Identity ${event.identityId} timeline updated`);
});
```

---

## 9. Subgraph and Data Indexing

### 9.1 The Indexing Problem

Blockchain data is optimized for writes, not reads. Querying the current state of an identity's credentials, timeline, and reputation directly from smart contracts is slow, expensive, and limited in expressiveness. The protocol requires an indexing layer that transforms on-chain events into an efficiently queryable data store.

### 9.2 TheGraph Integration

EYEKON Protocol uses TheGraph, a decentralized indexing protocol, to provide a subgraph that indexes all protocol events in real-time. The subgraph exposes a GraphQL API with rich query capabilities:

```graphql
query GetIdentityProfile($id: ID!) {
  identity(id: $id) {
    id
    owner
    type
    createdAt
    credentials {
      id
      type
      issuer { id metadata }
      issuedAt
      expiresAt
      revoked
    }
    timeline {
      id
      entryType
      title
      timestamp
      credential { id type }
    }
    reputation {
      overall
      credentialScore
      timelineScore
      activityScore
    }
  }
}
```

### 9.3 Query Patterns

The subgraph supports common query patterns out of the box:

- **Identity lookup**: Full profile including credentials, timeline, and reputation
- **Credential verification**: Check validity, issuer, and claim data for a credential
- **Timeline browsing**: Paginated, filtered timeline entries for an identity
- **Issuer analytics**: All credentials issued by a specific identity
- **Global statistics**: Total identities, credentials, and verifications on the protocol

### 9.4 Self-Hosted Indexing

While EYEKON hosts a public subgraph instance, anyone can deploy their own instance of the subgraph using TheGraph's tooling. This ensures that the indexing layer is not a centralization point and that the protocol remains fully decentralized.

---

## 10. Verification and Trust

### 10.1 The Verification Service

EYEKON Protocol includes a public verification service that provides a simple, embeddable interface for credential verification:

```
https://verify.eyekon.io/credential/{credentialHash}
```

This URL returns a human-readable verification page showing the credential's status (valid, expired, or revoked), the issuer's identity, the issuance date, and the credential claim summary. The page includes a machine-readable JSON response for programmatic access.

### 10.2 Verification Badge

Organizations can embed a "Verified by EYEKON Protocol" badge on their websites, applications, or documents. The badge links to the verification service and provides real-time credential validation.

```html
<a href="https://verify.eyekon.io/credential/{hash}">
  <img src="https://eyekon.io/badge/verified.svg" alt="Verified" />
</a>
```

### 10.3 KYC/KYB Bridge

The Verification Oracle provides a bridge between on-chain identity and off-chain verification processes (KYC for individuals, KYB for businesses). Authorized Oracle operators can submit verification attestations that are recorded on-chain without exposing the underlying personal data.

The bridge follows a privacy-preserving design:

1. A user completes KYC through an authorized provider (off-chain)
2. The provider submits a zero-knowledge proof or hashed attestation to the Verification Oracle (on-chain)
3. The attestation confirms "this identity has passed KYC" without revealing personal details
4. Any application can check the attestation status through the protocol

### 10.4 Trust Levels

The protocol defines a hierarchy of trust levels for credentials:

- **Self-attested**: The identity owner made the claim about themselves. Lowest trust.
- **Peer-attested**: Another identity endorsed the claim. Medium trust.
- **Issuer-verified**: An authorized issuer issued the credential. High trust.
- **Oracle-verified**: An external oracle (KYC provider, government API) confirmed the claim. Highest trust.

Applications can filter credentials by trust level to match their security requirements.

---

## 11. Competitive Analysis

### 11.1 Feature Comparison

| Feature | W3C DID/VC | Soulbound Tokens | ENS | Lens | Worldcoin | EYEKON Protocol |
|---|---|---|---|---|---|---|
| On-chain identity | Optional | Yes | Yes | Yes | Yes | Yes |
| Credential issuance | Yes (complex) | No standard | No | No | No | Yes (simple) |
| Credential revocation | Varies | No standard | N/A | N/A | N/A | Yes |
| Evolution Timeline | No | No | No | No | No | **Yes** |
| Reputation score | No | No | No | Partial | No | **Yes** |
| Multi-chain | Complex | Per-chain | Ethereum only | Polygon only | Optimism only | **EVM universal** |
| Developer SDK | Fragmented | None | ethers.js only | Lens SDK | WorldID SDK | **Unified SDK** |
| Verification service | Complex | Manual | N/A | N/A | Partial | **Built-in** |
| Transferability | N/A | No | Yes | Yes | No | **Configurable** |
| Monetization | None | None | Registration fees | None | Token | **Fees + royalties** |
| Open source | Specs only | Scattered | Yes | Yes | Partial | **Full stack** |

### 11.2 Positioning

EYEKON Protocol occupies a unique position in the identity landscape: it is the only solution that combines all five elements of the identity lifecycle (creation, credentialing, evolution, reputation, verification) in a single, open, composable protocol.

Existing solutions are either too narrow (ENS handles only naming, Worldcoin handles only proof-of-humanity), too complex (W3C DID/VC requires navigating multiple specifications and vendors), or too immature (SBTs have no standardized implementation).

EYEKON Protocol is designed to be the "one standard to rule them all" — not by replacing existing solutions, but by providing a composable layer that can incorporate and extend them.

---

## 12. Use Cases

### 12.1 Higher Education

A university deploys a credential issuance portal using the EYEKON SDK. When a student graduates, the university issues a DEGREE credential to the student's identity. The credential is permanently recorded on-chain and added to the student's Evolution Timeline. Employers can verify the degree instantly through the verification service, without contacting the university.

### 12.2 Professional Credentials

A professional certification body (e.g., AWS, Google Cloud, or a medical licensing board) issues CERTIFICATION credentials through the protocol. These credentials include expiration dates and are automatically flagged when they expire. Professionals maintain a living timeline of their certifications, with automatic reminders for renewal.

### 12.3 DAO Governance

A DAO uses EYEKON Protocol for member verification and reputation-weighted voting. Members' reputation scores — derived from their on-chain contributions, credential history, and community endorsements — determine their voting weight. This creates a more nuanced governance model than one-token-one-vote.

### 12.4 Hiring and Recruitment

A job board integrates EYEKON Protocol to verify candidate credentials automatically. Instead of manual reference checks, the platform queries the candidate's on-chain credentials and Evolution Timeline. The timeline provides a rich, verified narrative of the candidate's career progression.

### 12.5 Government Digital ID

A government agency adopts EYEKON Protocol as the foundation for a national digital identity system. Citizens receive INDIVIDUAL identities with KYC-verified credentials. Government agencies issue credentials (driver's license, tax ID, voter registration) that are verifiable by any authorized party. The open protocol prevents vendor lock-in and ensures interoperability with international systems.

### 12.6 Supply Chain Verification

A manufacturer uses ENTITY-type identities to represent products in a supply chain. Each product receives credentials at each stage of production (manufactured, inspected, shipped, delivered). The Evolution Timeline provides a complete, tamper-proof provenance record that consumers can verify by scanning a QR code.

### 12.7 Creator and Freelancer Portfolios

A freelance developer or designer uses EYEKON Protocol to build a verified portfolio. Each completed project is recorded as a MILESTONE in their Evolution Timeline, with client endorsements serving as ACHIEVEMENT credentials. Potential clients can browse the timeline and verify every claim without relying on self-reported information.

---

## 13. Monetization and Sustainability

### 13.1 Revenue Model

EYEKON Protocol generates revenue through five channels, ensuring long-term sustainability without compromising its open-source nature.

**Protocol Fees.** A small, configurable fee is charged on credential issuance. The default fee is set low enough to encourage adoption (targeting sub-$0.01 on Polygon) but high enough to generate meaningful revenue at scale. Fee parameters are governed by protocol governance and can be adjusted based on network conditions and strategic priorities.

**Hosted Services.** EYEKON operates hosted instances of the REST API gateway, verification service, and subgraph indexer. These services are offered as SaaS products with tiered pricing based on usage. Self-hosting remains an option for organizations that prefer full control.

**Enterprise Support.** Custom deployment, integration, and support packages for universities, governments, and large enterprises. This includes dedicated infrastructure, custom credential schemas, compliance consulting, and SLA-backed support.

**Premium Application Features.** The EYEKON application (eyekonit.com) offers premium features including bulk credential issuance, advanced analytics, custom branding, and white-label options. These features are application-level monetization and do not restrict protocol access.

**Governance Token (Future).** A protocol governance token may be introduced in a future phase to decentralize protocol governance, incentivize participation, and create a sustainable funding mechanism through treasury management.

### 13.2 Fee Structure

```
Credential Issuance Fee
├── 70% → Protocol Treasury
├── 20% → Issuer Reward (incentivizes credential issuance)
└── 10% → Verifier Pool (rewards verification activity)
```

### 13.3 Open Source Economics

The protocol's open-source nature might seem at odds with monetization, but this tension is well-understood and well-resolved in the software industry. Linux is open-source, but Red Hat generates billions in revenue from enterprise support. Kubernetes is open-source, but cloud providers generate billions from managed Kubernetes services. EYEKON Protocol follows the same playbook: the protocol is free, but the services, support, and premium features built on top of it generate sustainable revenue.

---

## 14. Governance

### 14.1 Initial Governance

During the initial phases (Phase 1 and Phase 2), protocol governance is centralized with the EYEKON core team. This is a deliberate choice to enable rapid iteration and decisive technical direction during the protocol's formative period.

### 14.2 Progressive Decentralization

The protocol follows a progressive decentralization model, gradually transferring governance authority to the community:

**Phase 1-2: Core Team Governance.** The EYEKON team controls protocol upgrades, fee parameters, and issuer registration. Community input is welcomed through GitHub issues and public RFC processes.

**Phase 3: Council Governance.** A Protocol Council is established, consisting of major issuers, developers, and community representatives. The Council has veto power over protocol changes and participates in fee-setting decisions.

**Phase 4+: Token Governance.** If a governance token is introduced, token holders gain voting rights over protocol parameters, treasury allocation, and upgrade proposals. The core team retains emergency powers (a time-locked multisig) for security-critical situations.

### 14.3 Upgrade Mechanism

Smart contracts are deployed behind transparent proxy contracts (following the UUPS pattern) that allow upgrades through governance-approved proposals. Each upgrade goes through a public review period, a security audit, and a time-locked execution delay to ensure community oversight.

---

## 15. Security Model

### 15.1 Threat Model

The protocol considers the following threat categories:

- **Identity spoofing**: An attacker creates a fake identity to impersonate a real person or organization.
- **Credential forgery**: An attacker issues fake credentials without authorization.
- **Sybil attacks**: An attacker creates many fake identities to manipulate reputation scores.
- **Data tampering**: An attacker attempts to modify existing credentials or timeline entries.
- **Denial of service**: An attacker attempts to make the protocol unusable.
- **Key compromise**: An identity owner's private key is stolen.

### 15.2 Mitigations

**Identity spoofing** is mitigated through the Verification Oracle's KYC/KYB bridge. High-trust applications can require Oracle-verified identities, ensuring that on-chain identities correspond to real-world entities.

**Credential forgery** is mitigated through the AccessControl contract's issuer registration and role-based permissions. Only registered, verified issuers can issue credentials, and their issuance activity is transparently recorded on-chain.

**Sybil attacks** are mitigated through the reputation system's anti-gaming mechanisms (issuer verification, time decay, diminishing returns, graph analysis, stake requirements) and through the KYC bridge for applications that require proof of unique humanity.

**Data tampering** is inherently mitigated by the blockchain's immutability. Once a credential or timeline entry is recorded, it cannot be modified. The Evolution Timeline's append-only design further prevents retrospective tampering.

**Denial of service** is mitigated by deploying on established, high-throughput blockchains (Polygon) with their own DDoS protections. The protocol's multiple access points (SDK, API, direct contract calls) provide redundancy.

**Key compromise** is mitigated through social recovery mechanisms, multi-signature wallet support, and the ability to deactivate a compromised identity and migrate credentials to a new identity through a governance-approved process.

### 15.3 Audit Strategy

The protocol commits to the following security assurance process:

1. **Internal review**: All code is reviewed by at least two core team members.
2. **Automated analysis**: Static analysis (Slither), formal verification (Certora), and fuzz testing (Echidna) are run on all contracts.
3. **External audit**: A minimum of two independent security audits from reputable firms (e.g., Trail of Bits, OpenZeppelin, Consensys Diligence) before mainnet deployment.
4. **Bug bounty**: A public bug bounty program with meaningful rewards (up to $100,000 for critical vulnerabilities) to incentivize ongoing security research.
5. **Incident response**: A documented incident response plan with designated security contacts, a disclosure timeline, and a patch deployment process.

---

## 16. Roadmap

### 16.1 Phase 1: Foundation (Weeks 1-3)

**Objective**: Deploy the core protocol on testnet and establish the open-source project.

**Deliverables**:
- IdentityRegistry.sol and CredentialEngine.sol — fully tested and documented
- AccessControl.sol with role-based permissions
- Basic `@eyekon/sdk` (v0.1) — identity creation, credential issuance, and verification
- Deployment on Polygon Mumbai testnet
- Protocol specification document (this white paper)
- GitHub repository with comprehensive README, contribution guidelines, and code of conduct
- Initial developer documentation and integration examples

**Success Metrics**: Smart contracts deployed on testnet, SDK published to npm, 10+ external developers testing the protocol.

### 16.2 Phase 2: Evolution (Weeks 4-8)

**Objective**: Complete the protocol's distinctive features and launch the reference implementation.

**Deliverables**:
- EvolutionTimeline.sol — append-only timeline with all entry types
- PaymentSplitter.sol — protocol fee collection and distribution
- TheGraph subgraph — full protocol indexing with GraphQL API
- SDK v1.0 — complete API coverage, meta-transactions, event subscriptions
- EYEKON app (eyekonit.com) integrated with the protocol
- EIP draft submission for EYEKON identity standard
- REST API gateway (v1.0)
- Verification service (verify.eyekon.io)

**Success Metrics**: Protocol fully functional on testnet, EYEKON app live with protocol integration, EIP draft submitted, 50+ external developers using the SDK.

### 16.3 Phase 3: Scale (Months 3-6)

**Objective**: Launch on mainnet, onboard first institutional issuers, and build the ecosystem.

**Deliverables**:
- ReputationOracle.sol — reputation scoring system
- Security audits (minimum two independent audits)
- Mainnet deployment on Polygon
- Multi-chain deployment (Ethereum, Base, Arbitrum)
- Cross-chain credential verification
- First 10 institutional issuers onboarded (universities, certification bodies, DAOs)
- Bug bounty program launch
- Developer grants program

**Success Metrics**: Mainnet deployment, 10+ institutional issuers, 1,000+ identities created, 5,000+ credentials issued.

### 16.4 Phase 4: Ecosystem (Months 6-12)

**Objective**: Grow the ecosystem, decentralize governance, and establish the protocol as the industry standard.

**Deliverables**:
- Protocol Council establishment
- Governance framework and voting mechanisms
- Advanced reputation features (domain-specific scoring, cross-protocol reputation)
- Mobile SDK (React Native, Flutter)
- Enterprise deployment toolkit
- Compliance framework for regulated industries (healthcare, finance, government)
- Strategic partnerships with major platforms

**Success Metrics**: 100+ issuers, 50,000+ identities, 250,000+ credentials, active Protocol Council, recognized as a leading identity standard.

---

## 17. Conclusion

Digital identity is one of the most fundamental and most broken layers of the internet. Despite billions of dollars invested and years of standardization effort, no protocol has emerged that handles the full identity lifecycle in an open, composable, developer-friendly way.

EYEKON Protocol fills this gap. By combining identity registration, credential management, the Evolution Timeline, reputation scoring, and universal verification into a single open standard, the protocol provides the foundation for a new era of decentralized identity.

The protocol-first approach ensures that EYEKON Protocol's value is not tied to any single application. Even if competitors build better UIs, more specialized tools, or more efficient implementations, they will build on the EYEKON standard. That is the real moat — not a product moat, but a protocol moat.

The smart contracts are the beginning. The real challenge — and the real opportunity — is adoption. Getting the first ten organizations to issue credentials through the protocol. Getting the first hundred developers to build on the SDK. Getting the first thousand individuals to create on-chain identities with Evolution Timelines.

The identity layer of the internet is waiting to be built. EYEKON Protocol is the blueprint.

---

## 18. References

1. W3C. "Decentralized Identifiers (DIDs) v1.0." W3C Recommendation, July 2022.
2. W3C. "Verifiable Credentials Data Model v1.1." W3C Recommendation, March 2022.
3. Buterin, V., Weyl, G., and Ohlhaver, P. "Decentralized Society: Finding Web3's Soul." May 2022.
4. Ethereum Foundation. "ERC-721: Non-Fungible Token Standard."
5. Ethereum Foundation. "ERC-1155: Multi Token Standard."
6. Ethereum Foundation. "EIP-2771: Secure Protocol for Native Meta Transactions."
7. Ethereum Foundation. "ERC-4337: Account Abstraction Using Alt Mempool."
8. The Graph Protocol. "The Graph: An Indexing Protocol for Querying Networks."
9. OpenZeppelin. "OpenZeppelin Contracts: Access Control."
10. Polygon Technology. "Polygon PoS: Scalable and Sustainable Ethereum Scaling."

---

**EYEKON Protocol** | eyekonit.com | April 2026

*This document is released under the Creative Commons Attribution 4.0 International License (CC-BY-4.0). You are free to share and adapt this material for any purpose, provided you give appropriate attribution.*
