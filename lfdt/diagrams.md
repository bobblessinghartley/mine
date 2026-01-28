# Panel Diagrams and Visual Aids

## 1. Privacy-Performance-Decentralization Trilemma

```mermaid
graph TD
    subgraph "Privacy-Performance-Decentralization Trilemma"
    Privacy[Privacy<br/>ZK Proofs, Confidential Execution]
    Performance[Performance<br/>Throughput, Latency, Costs]
    Decentralization[Decentralization<br/>Validator Distribution, Censorship Resistance]

    Privacy -.->|"Trade-off"| Performance
    Performance -.->|"Trade-off"| Decentralization
    Decentralization -.->|"Trade-off"| Privacy
    end

    style Privacy fill:#9370DB
    style Performance fill:#4682B4
    style Decentralization fill:#3CB371
```

### Positioning Different Systems

```mermaid
graph LR
    subgraph Triangle["Pick Your Trade-offs"]
        A[Public L1s<br/>Ethereum, Cardano<br/>⭐⭐⭐ Performance<br/>⭐⭐⭐ Decentralization<br/>⭐ Privacy]
        B[Permissioned<br/>Hyperledger, Corda<br/>⭐⭐⭐ Performance<br/>⭐ Decentralization<br/>⭐⭐ Privacy]
        C[Privacy L2s<br/>Aztec, zkSync<br/>⭐⭐ Performance<br/>⭐⭐ Decentralization<br/>⭐⭐⭐ Privacy]
        D[Privacy L1<br/>Midnight, Aleo<br/>⭐⭐ Performance<br/>⭐⭐⭐ Decentralization<br/>⭐⭐⭐ Privacy]
    end

    style A fill:#FFE4B5
    style B fill:#FFB6C1
    style C fill:#98FB98
    style D fill:#87CEEB
```

---

## 2. Midnight Dual-State Architecture

```mermaid
graph TB
    subgraph Public["Public Layer"]
        Consensus[AURA + GRANDPA]
        State[Public State<br/>Commitments, Nullifiers, Merkle Roots]
        Settlement[Settlement & Finality]
    end

    subgraph Private["Private Compact Execution"]
        Contract[Compact Smart Contracts]
        Witness[Witness Generation<br/>Private Inputs]
        Proof[PLONK Proof Generation]
    end

    subgraph Disclosure["Selective Disclosure Layer"]
        Rules[Programmable Disclosure Rules]
        Verify[Proof Verification]
        Audit[Authorized Auditor Access]
    end

    User[User/Application] --> Contract
    Contract --> Witness
    Witness --> Proof
    Proof --> Verify
    Verify --> State
    State --> Consensus
    Consensus --> Settlement

    Rules -.->|"Compliance"| Audit
    Proof -.->|"ZK Properties"| Rules

    style Public fill:#E6F3FF
    style Private fill:#F0E6FF
    style Disclosure fill:#E6FFE6
```

---

## 3. Privacy Spectrum and Regulatory Fit

```mermaid
graph LR
    subgraph Spectrum["Privacy Spectrum"]
        direction LR
        A[Full Transparency<br/>Public Blockchains<br/>✅ Easy Compliance<br/>❌ No Privacy]
        B[Access Control<br/>Permissioned DLT<br/>✅ Some Privacy<br/>⚠️ Centralization]
        C[Selective Disclosure<br/>ZK + Programmable<br/>✅ Privacy + Compliance<br/>⚠️ Complexity]
        D[Full Anonymity<br/>Mixers, Anonymous Coins<br/>✅ Maximum Privacy<br/>❌ Regulatory Issues]
    end

    A --> B --> C --> D

    Institutional[Institutional<br/>Use Cases] -.->|"Optimal Balance"| C
    Regulatory[Regulatory<br/>Requirements| -.->|"Acceptable"| C

    style A fill:#FFB6C1
    style B fill:#FFE4B5
    style C fill:#98FB98
    style D fill:#FFB6C1
    style Institutional fill:#87CEEB
    style Regulatory fill:#DDA0DD
```

---

## 4. Selective Disclosure Flow

```mermaid
sequenceDiagram
    participant User
    participant Contract as Compact Contract
    participant Prover as ZK Prover
    participant Chain as Midnight Chain
    participant Regulator as Authorized Auditor

    User->>Contract: Private Transaction Input<br/>(amount, counterparty, etc.)
    Contract->>Contract: Generate Witness<br/>(private data)
    Contract->>Prover: Create PLONK Proof

    Note over Prover: Prove properties without<br/>revealing details:<br/>- Amount > threshold<br/>- Valid signature<br/>- Sufficient balance

    Prover->>Chain: Submit Proof + Public Inputs<br/>(commitments, nullifiers)
    Chain->>Chain: Verify Proof<br/>(~6 second blocks)
    Chain->>Chain: Update State<br/>(nullifier set, commitments)

    alt Regulatory Request
        Regulator->>Contract: Request Disclosure<br/>(with authorization)
        Contract->>Regulator: Selective Disclosure<br/>(only authorized data)
        Note over Regulator: Sees transaction details<br/>per programmed rules
    end

    Note over Chain: Public sees: commitments, nullifiers<br/>Public does NOT see: amounts, parties, purposes
```

---

## 5. Use Case Privacy Matching Matrix

```mermaid
graph TB
    subgraph UseCases["Use Case Privacy Requirements"]
        direction TB

        subgraph HighPrivacy["High Privacy Required"]
            H1[Healthcare Data]
            H2[Competitive Procurement]
            H3[Private Credentials]
            H4[Financial Transactions]
        end

        subgraph SelectivePrivacy["Selective Privacy Required"]
            S1[Regulated Securities]
            S2[Supply Chain Pricing]
            S3[Cross-Org Workflows]
            S4[Multi-Party Computation]
        end

        subgraph LowPrivacy["Low/No Privacy Required"]
            L1[Public Registries]
            L2[Transparent Governance]
            L3[Public Auctions]
            L4[Open Supply Chain]
        end
    end

    subgraph Solutions["Technology Solutions"]
        ZK[ZK Proofs + Private Execution]
        SD[Selective Disclosure]
        Public[Public Blockchain]
    end

    HighPrivacy --> ZK
    SelectivePrivacy --> SD
    LowPrivacy --> Public

    style HighPrivacy fill:#FFB6C1
    style SelectivePrivacy fill:#FFE4B5
    style LowPrivacy fill:#98FB98
    style ZK fill:#9370DB
    style SD fill:#4682B4
    style Public fill:#3CB371
```

---

## 6. Midnight Technology Stack

```mermaid
graph TB
    subgraph Application["Application Layer"]
        SDK[Midnight.js TypeScript SDK<br/>Node 22+ | Turbo + Yarn]
        Wallet[Midnight Wallet<br/>Night Keys Management]
    end

    subgraph Contract["Contract Layer"]
        Compact[Compact Smart Contracts<br/>Privacy-Preserving Logic]
        Compiler[Compact Compiler<br/>Chez Scheme → TypeScript + ZKIR]
    end

    subgraph Proof["Proof System"]
        PLONK[PLONK Proof System]
        Witness[Witness Generation]
        Circuit[Circuit Constraints]
    end

    subgraph Runtime["Substrate Runtime Layer"]
        Pallets[FRAME Pallets<br/>Privacy Operations]
        Weights[Block Weights & Benchmarks]
        Storage[State: Commitments, Nullifiers]
    end

    subgraph Consensus["Consensus Layer"]
        AURA[AURA Block Production<br/>6-second blocks]
        GRANDPA[GRANDPA Finality]
        BEEFY[BEEFY Light Client]
    end

    subgraph Indexer["Indexer Infrastructure"]
        Micro[Microservices Architecture]
        DUST[DUST Tracking Service]
        Null[Nullifier Management]
    end

    SDK --> Compact
    Wallet --> Compact
    Compact --> Compiler
    Compiler --> Witness
    Witness --> PLONK
    PLONK --> Circuit
    Circuit --> Pallets
    Pallets --> Weights
    Weights --> Storage
    Storage --> AURA
    AURA --> GRANDPA
    GRANDPA --> BEEFY

    Storage -.->|"Index"| Micro
    Micro --> DUST
    Micro --> Null

    style Application fill:#E6F3FF
    style Contract fill:#F0E6FF
    style Proof fill:#FFE6F0
    style Runtime fill:#E6FFE6
    style Consensus fill:#FFF9E6
    style Indexer fill:#F0F0F0
```

---

## 7. Privacy vs Transparency Trade-off Timeline

```mermaid
gantt
    title Evolution of Privacy Approaches in DLT
    dateFormat YYYY

    section Public Transparency
    Bitcoin/Ethereum Era                    :2009, 2015

    section Access Control
    Hyperledger/Corda                       :2015, 2020

    section Cryptographic Privacy
    Zcash/Monero (Anonymous)                :2016, 2024

    section Selective Disclosure
    Privacy L1s/L2s (Compliant)            :2020, 2026

    section Programmable Privacy
    Compact + ZK (Institutional)            :2023, 2027
```

---

## 8. Institutional Privacy Model Preferences

```mermaid
pie title "What Institutions Need from Privacy"
    "Confidentiality from Competitors" : 40
    "Selective Regulatory Disclosure" : 30
    "Auditability (Internal/External)" : 15
    "Data Sovereignty/Residency" : 10
    "Anonymity from Regulators" : 5
```

---

## 9. Performance Bottlenecks in Privacy Systems

```mermaid
graph LR
    subgraph Client["Client-Side"]
        Input[Transaction Input]
        WGen[Witness Generation<br/>⚠️ BOTTLENECK]
        PGen[Proof Generation<br/>⚠️ BOTTLENECK]
    end

    subgraph Network["Network Layer"]
        Broadcast[Proof Broadcast<br/>✅ Fast]
    end

    subgraph Chain["On-Chain"]
        Verify[Proof Verification<br/>✅ Optimized]
        State[State Update<br/>✅ Fast]
    end

    Input --> WGen
    WGen --> PGen
    PGen --> Broadcast
    Broadcast --> Verify
    Verify --> State

    Note1[Client hardware<br/>is the limiting factor]
    Note2[Opt-level=3<br/>critical for performance]

    WGen -.-> Note1
    PGen -.-> Note2

    style WGen fill:#FFB6C1
    style PGen fill:#FFB6C1
    style Verify fill:#98FB98
    style State fill:#98FB98
```

---

## 10. Compliance Architecture Pattern

```mermaid
graph TB
    subgraph Transaction["Private Transaction"]
        User[User Intent]
        Private[Private Data<br/>Amount, Parties, Purpose]
        Public[Public Data<br/>Commitments, Nullifiers]
    end

    subgraph Proof["Zero-Knowledge Proof"]
        Property1[Prove: Amount > $10k<br/>without revealing amount]
        Property2[Prove: Valid AML Check<br/>without revealing identity]
        Property3[Prove: Authorized Party<br/>without revealing credentials]
    end

    subgraph Compliance["Compliance Layer"]
        Rules[Programmable Rules<br/>Travel Rule, AML, KYC]
        Disclosure[Selective Disclosure<br/>to Authorized Auditors]
        Audit[Audit Trail<br/>Who accessed what, when]
    end

    User --> Private
    User --> Public
    Private --> Property1
    Private --> Property2
    Private --> Property3

    Property1 --> Rules
    Property2 --> Rules
    Property3 --> Rules

    Rules --> Disclosure
    Disclosure --> Audit

    Public --> Chain[On-Chain State]
    Property1 --> Chain
    Property2 --> Chain
    Property3 --> Chain

    style Transaction fill:#E6F3FF
    style Proof fill:#F0E6FF
    style Compliance fill:#E6FFE6
```

---

## Usage Notes for Panel

### When to use each diagram:

1. **Trilemma** - Opening remarks, framing the challenge
2. **Dual-State Architecture** - Explaining Midnight's approach
3. **Privacy Spectrum** - Discussing regulatory fit
4. **Selective Disclosure Flow** - Answering "how does it work?"
5. **Use Case Matrix** - Matching privacy to use cases
6. **Tech Stack** - Performance and operational considerations
7. **Timeline** - Regulator education, industry evolution
8. **Institutional Preferences** - What enterprises actually want
9. **Performance Bottlenecks** - Scaling challenges
10. **Compliance Pattern** - Bringing it all together

### Presentation tips:

- Keep diagrams on screen while discussing
- Point to specific components when making technical points
- Use colors to emphasize trade-offs
- Refer back to trilemma throughout discussion
