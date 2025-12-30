# Novel PQC + Federated Learning Research Ideas

> **Last Updated:** December 30, 2025  
> **Status:** Brainstorming / Potential Research Directions

---

## 🚨 Major Challenges in PQC + FL

### 1️⃣ Communication overhead (Key & ciphertext size)

**The Problem:**
- PQC keys/signatures are significantly larger than RSA/ECC
- FL has many clients × many rounds

**Why major:**
👉 Directly affects scalability and training time.

---

### 2️⃣ Computation overhead on edge devices

**The Problem:**
- Lattice-based PQC requires heavy math
- Edge devices are resource-constrained

**Why major:**
👉 Causes latency, battery drain, and client dropout.

---

### 3️⃣ PQC-compatible secure aggregation

**The Problem:**
- Existing secure aggregation assumes classical crypto
- Naive replacement breaks privacy or efficiency

**Why major:**
👉 Secure aggregation is central to FL privacy.

---

### 4️⃣ Long-term privacy (Harvest-now-decrypt-later)

**The Problem:**
- FL updates are stored long-term
- Classical crypto fails against future quantum attacks

**Why major:**
👉 Breaks the core privacy promise of FL.

---

### 5️⃣ Client heterogeneity

**The Problem:**
- Devices vary widely in compute, power, and network
- Uniform PQC policies exclude weaker clients

**Why major:**
👉 Impacts fairness, participation, and model quality.

---

## 🔥 1. Hybrid Multi-Primitive PQC Framework for FL

### Novelty
Most current work uses single PQC primitives. Create a **dynamic adaptive system** that:

- Combines multiple PQC families (lattice, code-based, hash-based, isogeny-based)
- Automatically selects optimal primitives based on:
  - Client device capabilities
  - Network conditions
  - Threat model evolution

### Gap Addressed
Current research lacks **adaptive, context-aware PQC selection mechanisms**.

### Key Contribution
Develop a framework that balances **security, efficiency, and heterogeneity** in resource-constrained FL environments.

### Potential Architecture
```
┌─────────────────────────────────────────────────────┐
│            Adaptive PQC Selection Engine            │
├─────────────────────────────────────────────────────┤
│  Input: Device specs, Network latency, Threat level │
│  Output: Optimal PQC primitive selection            │
├─────────────────────────────────────────────────────┤
│  Kyber (fast, small keys) ──► Mobile devices        │
│  McEliece (large keys) ──► High-bandwidth servers   │
│  SPHINCS+ (hash-based) ──► Long-term signatures     │
└─────────────────────────────────────────────────────┘
```

### Feasibility: ⭐⭐⭐⭐ (High)
- Good fit for 4-month timeline
- Can demonstrate on Raspberry Pi testbed

---

## 🔥 2. Code-Based PQC for Federated Learning

### Novelty
Almost **ALL current PQC-FL work uses lattice-based cryptography**. Code-based alternatives (like Classic McEliece) are virtually unexplored in FL contexts.

### Research Questions
1. Can code-based encryption provide better efficiency for specific FL aggregation protocols?
2. How do code-based schemes perform compared to lattice-based ones for gradient encryption?
3. Can you design novel FL-specific code-based protocols?

### Why Novel
Recent reviews note: *"Limited attempts to build ciphers based on error-correcting code-based problems"* — creating a significant gap.

### Challenges
| Challenge | Impact |
|-----------|--------|
| Large public keys (~1 MB for McEliece) | High bandwidth overhead |
| Limited library support | Implementation difficulty |
| Less studied in applied contexts | Higher research risk |

### Feasibility: ⭐⭐⭐ (Medium)
- High novelty but implementation challenges
- May need simulation for large-scale experiments

---

## 🔥 3. Post-Quantum Secure Gradient Compression with Provable Privacy

### Novelty
Combine **gradient compression techniques with PQC** while maintaining provable privacy guarantees.

### The Problem
```
FL Communication Cost Problem:
├── High bandwidth for gradient updates
├── Gradient compression reduces costs BUT
│   └── Interacts poorly with encryption
└── PQC adds additional overhead
```

### Your Contribution
Design quantum-resistant compression-friendly encryption schemes that:

- ✅ Enable homomorphic operations on compressed gradients
- ✅ Maintain differential privacy guarantees in the quantum era
- ✅ Reduce communication overhead by **60-80%** compared to naive PQC-FL

### Technical Approach
| Technique | Purpose |
|-----------|---------|
| Quantized gradients | Reduce precision (32-bit → 8-bit) |
| Sparsification | Only send top-k% gradients |
| PQC-friendly encoding | Design compression compatible with Kyber/Dilithium |

### Feasibility: ⭐⭐⭐⭐ (High)
- Practical impact
- Measurable results on Raspberry Pi

---

## 🔥 4. Quantum-Resistant Split Learning with Asymmetric Cryptography

### Novelty
**Split learning** (where models are split between client and server) with PQC is barely explored.

### What is Split Learning?
```
Traditional FL:          Split Learning:
┌─────────┐              ┌─────────┐
│ Client  │              │ Client  │
│ [Full   │              │ [Layers │
│  Model] │              │  1-3]   │
└────┬────┘              └────┬────┘
     │ gradients              │ activations
     ▼                        ▼
┌─────────┐              ┌─────────┐
│ Server  │              │ Server  │
│ [Aggreg]│              │ [Layers │
└─────────┘              │  4-10]  │
                         └─────────┘
```

### Key Innovation
- Design PQC protocols specifically for split learning's unique communication patterns
- Leverage the split architecture to **reduce PQC overhead**
- Create novel key exchange mechanisms for continuous model splitting

### Research Angle
- Split learning sends **activations** instead of gradients
- Different privacy/security requirements
- Can optimize PQC for this specific pattern

### Feasibility: ⭐⭐⭐ (Medium)
- Interesting niche
- Less established baseline to compare

---

## 🔥 5. Post-Quantum Verifiable Aggregation with Byzantine Resilience

### Novelty
Most PQC-FL work assumes **honest-but-curious adversaries**. Design quantum-resistant protocols that:

- ✅ Detect and exclude Byzantine (malicious) clients
- ✅ Provide verifiable computation proofs using PQC
- ✅ Use lattice-based zero-knowledge proofs for aggregation verification

### Gap
Current Byzantine fault tolerance mechanisms rely on **quantum-vulnerable algorithms**.

### Technical Components
| Component | PQC Alternative |
|-----------|-----------------|
| Commitment schemes | Lattice-based commitments |
| Zero-knowledge proofs | Post-quantum ZK-SNARKs |
| Signature verification | Dilithium signatures |
| Byzantine detection | PQC-secured Krum/Median |

### Protocol Sketch
```
1. Client signs update with Dilithium
2. Client provides ZK proof of honest computation
3. Server verifies proofs using PQC
4. Byzantine clients detected via robust aggregation
5. Aggregation result is verifiable
```

### Feasibility: ⭐⭐⭐⭐⭐ (Very High)
- **BEST FIT for your project**
- Combines your Byzantine + PQC interests
- Demonstrable on Raspberry Pi
- Clear military application

---

## 🔥 6. Hybrid Quantum-Classical FL with PQC Communication

### Novelty
Bridge **quantum federated learning** with post-quantum classical cryptography.

### Research Direction
```
┌──────────────────────────────────────────────────┐
│          Hybrid Quantum-Classical FL             │
├──────────────────────────────────────────────────┤
│  Clients: Quantum circuits for local training    │
│  Communication: Secured with PQC                 │
│  Server: Quantum-enhanced aggregation            │
└──────────────────────────────────────────────────┘
```

### Key Question
How to efficiently secure quantum gradient communication with PQC?

### Challenges
- Requires access to quantum hardware (or simulators)
- Highly theoretical at current stage
- Limited practical deployments

### Feasibility: ⭐⭐ (Low)
- Very novel but requires quantum computing resources
- Better suited for theoretical paper

---

## 🔥 7. Post-Quantum Secure Cross-Silo FL with Forward Secrecy

### Novelty
Design PQC schemes with **perfect forward secrecy** for long-term FL collaborations.

### Key Features
- **Ratcheting mechanisms** for key rotation across FL rounds
- **Post-compromise security** guarantees
- Minimize key management overhead

### Why It Matters for Military
```
Military FL Scenario:
├── Long-term collaborations (years)
├── High-value targets for "harvest now, decrypt later"
├── Need: Even if keys compromised later,
│         past communications remain secure
└── Solution: Forward secrecy with PQC
```

### Technical Approach
| Feature | Implementation |
|---------|----------------|
| Key ratcheting | Double Ratchet with Kyber |
| Session keys | Ephemeral Kyber key exchange |
| Long-term keys | Dilithium for identity |

### Gap
Some work addresses ratcheting mechanisms but **comprehensive frameworks are missing**.

### Feasibility: ⭐⭐⭐⭐ (High)
- Well-defined problem
- Clear implementation path
- Strong military relevance

---

## 🔥 8. PQC for Federated Learning on NISQ Devices

### Novelty
Secure federated learning on **Noisy Intermediate-Scale Quantum (NISQ)** hardware using PQC.

### Unique Challenge
```
NISQ Constraints:
├── 50-100 noisy qubits
├── Limited coherence time
├── High error rates
└── Need: Extremely lightweight PQC
```

### Research Questions
- Can we run FL on NISQ devices?
- What's the minimum PQC overhead acceptable?
- How does quantum noise affect both computation AND cryptography?

### Feasibility: ⭐⭐ (Low)
- Requires quantum hardware access
- Highly speculative
- Better for future research

---

## 📊 Summary: Feasibility vs. Novelty Matrix

```
                    High Novelty
                         │
     ┌───────────────────┼───────────────────┐
     │   6. Quantum FL   │  2. Code-based    │
     │   8. NISQ FL      │  4. Split Learning│
     │                   │                   │
Low ─┼───────────────────┼───────────────────┼─ High
Feas │                   │                   │ Feasibility
     │                   │  5. Byzantine+PQC │
     │                   │  1. Hybrid Multi  │
     │                   │  3. Compression   │
     │                   │  7. Forward Secr. │
     └───────────────────┼───────────────────┘
                         │
                    Low Novelty
```

---

## 🎯 Recommended for Your Project

### Top 3 Recommendations (4-month timeline, 3 Raspberry Pis, Military focus):

| Rank | Idea | Why |
|------|------|-----|
| **#1** | 5. Byzantine + PQC Verifiable Aggregation | Combines your interests, high feasibility, clear military application |
| **#2** | 7. Forward Secrecy for Cross-Silo FL | Strong military relevance, well-defined scope |
| **#3** | 3. Gradient Compression + PQC | Practical impact, measurable on Raspberry Pi |

### Suggested Combination
**Merge ideas 5 + 7**: 
> *"Post-Quantum Secure Byzantine-Resilient FL with Forward Secrecy for Military Applications"*

This gives you:
- Byzantine attack detection (interesting experiments)
- PQC security (quantum-safe)
- Forward secrecy (military requirement)
- Verifiable aggregation (trust in distributed systems)

---

## 📚 References to Explore

1. NIST PQC Standards: https://csrc.nist.gov/Projects/post-quantum-cryptography
2. Byzantine FL survey: MDPI journals
3. Ratcheting mechanisms: Signal Protocol + PQC adaptations
4. Code-based crypto: Classic McEliece submission
5. Split Learning: MIT Media Lab papers

---

## Next Steps

1. [ ] Choose 1-2 ideas to focus on
2. [ ] Deep literature review for chosen direction
3. [ ] Design system architecture
4. [ ] Implement baseline on Raspberry Pi
5. [ ] Add PQC layer
6. [ ] Run experiments
7. [ ] Write paper
