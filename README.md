# Federated Learning with Post-Quantum Cryptography Research

**Project Team:** Vaishnavi, Yasaswini, Hema Latha  
**Institution:** VIT-AP University  
**Research Focus:** Byzantine-Robust Federated Learning with Post-Quantum Security

---

## 🎯 Project Overview

We are working on a research paper that combines **Federated Learning (FL)** security with **Post-Quantum Cryptography (PQC)**. Our goal is to defend against Byzantine attacks in federated learning systems while ensuring quantum-safe communication.

**Current Paper Title:**  
*"Byzantine-Robust Federated Learning Under Non-IID Data: A Post-Quantum Three-Layer Defense Approach"*

**Key Results So Far:**
- 93.2% accuracy with 40% malicious clients
- Non-IID data distribution (Dirichlet α=0.5)
- Uses Kyber-512 + Dilithium-2 for encryption
- Three-layer defense: Gradient fingerprinting + Cosine similarity + Validation-based filtering

---

## 📚 What's in Each File?

### **brainstorm/** folder

#### 1. **01_what_is_federated_learning.md** (6,753 lines)
**Purpose:** Foundation document explaining Federated Learning  
**Contents:**
- What is FL with real-world analogies (hospitals sharing medical knowledge without patient data)
- How FedAvg algorithm works mathematically
- Types of FL: Horizontal, Vertical, Transfer Learning
- Real-world applications: Google Keyboard, Healthcare, Finance
- Why FL needs encryption and security

**Why it matters:** Understanding FL basics is essential before diving into Byzantine attacks and PQC integration.

---

#### 2. **02_post_quantum_cryptography_basics.md** (8,479 lines)
**Purpose:** Complete guide to Post-Quantum Cryptography  
**Contents:**
- Why quantum computers break RSA and ECC (Shor's algorithm)
- 5 PQC algorithm families: Lattice, Hash-based, Code-based, Multivariate, Isogeny
- NIST PQC standards (2024): Kyber-768, Dilithium-3, SPHINCS+
- **Kyber-512 details:** 1,184-byte keys, how it works, security levels
- **Dilithium-2 details:** 3,293-byte signatures
- Comparison tables: Classical vs PQC overhead

**Why it matters:** Our paper uses Kyber and Dilithium - you need to understand what they do and their limitations.

---

#### 3. **03_federated_learning_challenges.md** (14,654 lines)
**Purpose:** Deep dive into 10 major FL challenges  
**Contents:**
- **Communication Efficiency:** FL sends millions of parameters, bandwidth is bottleneck
- **Non-IID Data:** Clients have different data distributions (hospitals in different cities)
- **Byzantine Attacks:** Malicious clients poisoning the model
  - Label flipping (changing labels)
  - Gradient scaling (amplifying updates)
  - Backdoor attacks (hidden triggers)
- **Privacy vs Security trade-off:** Encryption hides attacks, detection becomes hard
- System heterogeneity, convergence theory, fairness, personalization

**Why it matters:** Chapter 3 of our paper directly addresses these challenges - especially Byzantine attacks and Non-IID data.

---

#### 4. **04_research_gaps_and_opportunities.md** (19,139 lines)
**Purpose:** Specific research gaps at FL + PQC intersection  
**Contents:**
- **Gap 1 (HIGHEST PRIORITY):** Efficient PQC Secure Aggregation Protocol
  - Current problem: Bonawitz et al. (2017) uses Diffie-Hellman (quantum-vulnerable)
  - What's needed: Replace DH with Kyber for quantum-safe aggregation
  - This is what we SHOULD be doing for true novelty
- **Gap 2:** PQC Homomorphic Encryption for FL
- **Gap 3:** Communication-efficient PQC protocols
- 3-year PhD timeline and success metrics
- Methodology: How to design, implement, evaluate PQC protocols

**Why it matters:** This identifies what REAL novel research looks like. Gap 1 is the big opportunity we're not currently addressing.

---

#### 5. **05_paper_discussion_byzantine_robust_fl.md** (Critical Analysis)
**Purpose:** Honest feedback on our current paper  
**Contents:**
- **10 Major Issues Identified:**
  1. **PQC contribution unclear** - Feels like add-on, not core innovation
  2. **Not implementing secure aggregation** - Just using encrypted communication (big difference!)
  3. **Missing PQC overhead analysis** - No comparison with RSA/ECC
  4. **Limited evaluation** - Only MNIST, only label-flipping, only 5 clients
  5. **No formal security proofs**
  6. Scalability concerns (gradient fingerprinting is O(n²))
  7. Validation set bias not addressed
  8. Missing ablation studies
  9. No comparison with PQC-specific defenses
  10. Writing/presentation issues

- **Critical Finding:** Our paper combines existing techniques without novel algorithmic contributions
  - Rejection risk: **70-80%** at top conferences
  - It's "incremental work" not "novel research"

- **Three Research Paths:**
  - **Path A (2-3 weeks):** Accept incremental nature, reframe for workshops, graduate quickly
  - **Path B (2-3 months):** Add ONE novel contribution (adaptive fingerprinting OR compact PQC)
  - **Path C (6-12 months):** Design full PQC secure aggregation protocol (Gap 1)

**Why it matters:** This is the most important document. It tells us our work needs improvement and gives us options.

---

#### 6. **06_compact_pqc_for_federated_learning.md** (Just created - 60KB)
**Purpose:** Understanding why current PQC is impractical for large-scale FL  
**Contents:**
- **The Problem:** Kyber-768 has 1,184-byte keys (37× larger than ECC's 32 bytes)
  - 100 hospitals × 10 rounds = **540 MB overhead** (17× classical crypto)
  - Makes 1000+ client FL impractical
- **Why keys are so large:** Lattice crypto needs high dimensions (n=768) for quantum resistance
- **12 Mathematical Clues** for breakthrough compact PQC:
  1. Non-abelian Hidden Subgroup Problems (most promising, ~100 byte keys)
  2. Algebraic Geometry beyond isogenies
  3. NP-hard problems with trapdoors (holy grail but risky)
  4. Quantum wasteland problems
  5. Non-linear algebraic structures
  6. And 7 more...
- **FL Requirements:** Need < 200 byte keys, < 1ms operations, scalable to 1000+ clients
- **Future research directions:** Short-term, medium-term, long-term plans

**Why it matters:** If we want to do PhD-level work, we need to understand that current PQC (Kyber/Dilithium) is NOT practical for large-scale FL. A breakthrough in compact PQC would be groundbreaking research.

---

## 🚨 Current Status & Critical Decisions

### Where We Are:
✅ Paper draft complete with 93.2% accuracy results  
✅ Comprehensive research on FL, PQC, and challenges  
✅ Identified research gaps and opportunities  
❌ **Paper lacks true novelty - combines existing techniques**  
❌ Not implementing actual secure aggregation (just encrypted communication)  
❌ Missing PQC overhead analysis  
❌ Limited experimental scope  

### The Big Question:
**What's the difference between what we're doing and true novelty?**

| What We're Doing | What True Novelty Looks Like |
|------------------|------------------------------|
| Using Kyber for encrypted communication | Designing PQC secure aggregation protocol |
| Applying existing gradient fingerprinting | Creating adaptive/lightweight Byzantine defense |
| Combining 3 existing techniques | Inventing new algorithm with theoretical proofs |
| Limited to 5 clients, 1 dataset | Comprehensive evaluation: 10/50/100 clients, 3+ datasets |
| No overhead analysis | Detailed comparison: RSA vs ECC vs Kyber overhead |

**Example:** Chen et al. (2024) designed a NEW hierarchical PQC aggregation scheme - that's novel. We're just using Kyber as drop-in replacement for RSA.

---

## 📋 Next Steps Plan

### **IMMEDIATE (This Week - Days 1-3):**

#### **Day 1-2: Team Alignment Meeting** 🎯
**Goals:**
- Everyone reads **05_paper_discussion_byzantine_robust_fl.md** (critical analysis)
- Understand the 10 issues with current paper
- Discuss honestly: What are our goals?
  - Quick graduation (3-4 months)? → Path A
  - Solid publication (5-6 months)? → Path B  
  - PhD-level contribution (12+ months)? → Path C

**Discussion Questions:**
1. How much time do we have before graduation deadline?
2. Are co-authors actively available for 3-6 months of work?
3. Interests: More ML/FL side or more cryptography/protocol design?
4. Can we accept that current paper might only get into workshops, not top conferences?

#### **Day 3: Decision & Action Plan**
Based on team meeting, choose ONE path:

---

### **PATH A: Quick Graduation (2-3 weeks)** ⚡
**Goal:** Accept incremental nature, polish current work, target workshops

**Week 1 Tasks:**
- [ ] **Vaishu:** Add PQC overhead analysis section
  - Measure: Key sizes (Kyber vs RSA vs ECC)
  - Measure: Computation time (key generation, encryption, signing)
  - Create comparison table
- [ ] **Yasaswini:** Run additional attack experiments
  - Gradient scaling attack
  - Add FEMNIST dataset (standard FL benchmark)
- [ ] **Hema Latha:** Add limitations section to paper
  - Acknowledge: "We use PQC for communication, not secure aggregation"
  - Acknowledge: "Scalability limited (O(n²) fingerprinting)"
  - Acknowledge: "Further work needed: Design PQC secure aggregation protocol"

**Week 2-3:**
- Polish writing, create better figures
- Target venues: IEEE FL Workshops, IJCAI Workshop on Federated Learning
- Submit and move on

**Pros:** Fast graduation, reduces stress  
**Cons:** Limited impact, lower-tier publication  

---

### **PATH B: Solid Publication (2-3 months)** 🎓
**Goal:** Add ONE novel contribution, target tier-2 conference

**Option B1: Novel Adaptive Byzantine Defense**
- Design gradient fingerprinting that adapts to attack patterns
- Use online learning to update similarity thresholds
- **Novel contribution:** "Adaptive Fingerprinting for PQC-encrypted FL"

**Option B2: Lightweight PQC Aggregation**
- Design simplified secure aggregation for small networks (< 100 clients)
- Use key amortization: One Kyber key exchange for multiple rounds
- **Novel contribution:** "Communication-Efficient PQC Aggregation Protocol"

**Month 1:** Design the novel algorithm (mathematical formulation + pseudocode)  
**Month 2:** Implement and integrate with existing system  
**Month 3:** Comprehensive evaluation (3 datasets, 3 attack types, scalability tests)

**Division of Work:**
- **Vaishu:** Algorithm design + mathematical proofs
- **Yasaswini:** Implementation + integration
- **Hema Latha:** Experiments + paper writing

**Target Venues:** IEEE ICDCS, ACM CODASPY, ESORICS

**Pros:** Respectable publication, learning experience  
**Cons:** 3 months extra work, moderate novelty  

---

### **PATH C: PhD-Level Research (6-12 months)** 🔬
**Goal:** Design full PQC secure aggregation protocol (Gap 1 from research doc)

**This is the "real" research:** Replace Bonawitz et al.'s Diffie-Hellman based secure aggregation with Kyber-based protocol.

**Phase 1 (Months 1-2): Protocol Design**
- Study Bonawitz et al. (2017) protocol deeply
- Design 4 phases with Kyber:
  - Phase 0: Setup (server generates params)
  - Phase 1: Pairwise key exchange (Kyber KEM between clients)
  - Phase 2: Masked model upload (encrypt gradients with shared masks)
  - Phase 3: Unmasking (reveal masks for aggregation)
  - Phase 4: Dropout resilience
- Write formal security proofs (IND-CPA security under Module-LWE)

**Phase 2 (Months 3-4): Implementation**
- Use `pqcrypto` or `liboqs` library for Kyber
- Implement in TensorFlow Federated or PySyft
- Optimize for communication (batch operations, compression)

**Phase 3 (Months 5-6): Evaluation**
- Overhead analysis: Compare with classical secure aggregation
- Byzantine robustness: Test with various attack types
- Scalability: Test with 10, 50, 100, 500 clients
- Multiple datasets: MNIST, FEMNIST, CIFAR-10

**Phase 4 (Months 7-8): Paper Writing**
- Write full conference paper (12-15 pages)
- Include: Threat model, protocol description, security proofs, implementation details, comprehensive evaluation
- Target top venues: IEEE S&P, USENIX Security, ACM CCS, NDSS

**Division of Work:**
- **All:** Study Bonawitz protocol together (Month 1)
- **Vaishu:** Protocol design + security proofs (Lead theorist)
- **Yasaswini:** Implementation + optimization (Lead engineer)
- **Hema Latha:** Evaluation + paper writing (Lead experimenter)

**Pros:** High-impact publication, PhD-worthy, addresses real unsolved problem  
**Cons:** 6-12 months commitment, high risk, requires deep crypto knowledge  

---

## 🎯 My Recommendation

Based on conversation history and analysis:

### **For Graduation in 2025:** Choose Path A
- Current paper as-is won't get into top conferences (70-80% rejection risk)
- Reframe as "empirical study" or "implementation experience"
- Add overhead analysis, limitations section, one more dataset
- Target workshops: Fast acceptance, lower bar, still counts as publication
- **Timeline:** Submit by mid-January 2025, decision by March

### **For Strong Publication:** Choose Path B
- Adds one genuine novel contribution (adaptive defense or lightweight aggregation)
- Significantly improves acceptance chances (50-60%)
- Doable in 2-3 months with focused work
- **Timeline:** Complete by March 2025, submit to May conferences

### **For PhD/Research Career:** Choose Path C
- This is what "real research" looks like in this area
- Addresses Gap 1 (highest priority from research gaps doc)
- Only 1 paper exists on PQC secure aggregation (Chen et al. 2024) - field is wide open
- But requires 6-12 months and deep commitment
- **Timeline:** Complete by mid-2025, submit to September conferences

---

## 📖 Reading Order for New Team Members

**Day 1 (4-5 hours):**
1. Read this README completely
2. Skim **01_what_is_federated_learning.md** (focus on FedAvg algorithm)
3. Skim **02_post_quantum_cryptography_basics.md** (focus on Kyber-512 and Dilithium-2)

**Day 2 (4-5 hours):**
1. Read **05_paper_discussion_byzantine_robust_fl.md** CAREFULLY (this is critical)
2. Understand the 10 issues
3. Think about which path (A/B/C) makes sense for you

**Day 3 (3-4 hours):**
1. Read **04_research_gaps_and_opportunities.md** (Gap 1 section especially)
2. Understand what "secure aggregation" means (we're NOT doing this currently)
3. Prepare for team meeting

**Optional (Future):**
- Read **03_federated_learning_challenges.md** for deep understanding of FL problems
- Read **06_compact_pqc_for_federated_learning.md** if choosing Path C (long-term research)

---

## 🔑 Key Concepts to Understand

### 1. **Federated Learning (FL)**
Hospitals train AI together without sharing patient data. Each hospital trains locally, only shares model updates.

### 2. **Byzantine Attacks**
Malicious hospitals send poisoned updates to sabotage the global model.

### 3. **Post-Quantum Cryptography (PQC)**
Encryption safe against quantum computers. Kyber (encryption) and Dilithium (signatures) are NIST standards.

### 4. **Secure Aggregation vs Encrypted Communication**
- **Encrypted Communication (what we do):** Client → [Kyber encrypt] → Server
- **Secure Aggregation (what we SHOULD do):** Clients collaborate to hide individual updates, server only sees sum
- **Big difference:** Secure aggregation is much harder but more private and secure

### 5. **Non-IID Data**
Not Identically and Independently Distributed. Hospital A has cancer patients, Hospital B has diabetes patients - different distributions.

### 6. **Gradient Fingerprinting**
Our defense: Project gradients to low dimensions (512D), check similarity between clients. Similar gradients = likely honest.

---

## 🛠️ Technical Setup (When We Start Coding)

### **Current Paper Implementation:**
- Framework: PyTorch or TensorFlow
- PQC Library: `pqcrypto` or `liboqs`
- Dataset: MNIST (handwritten digits)
- Attack: Label flipping (40% malicious clients)
- Metrics: Accuracy, detection rate, false positive rate

### **If We Do Path B/C - Need to Set Up:**
```bash
# Install dependencies
pip install torch torchvision tensorflow-federated
pip install pqcrypto  # For Kyber/Dilithium
pip install matplotlib pandas numpy scipy

# Clone our repo (if not already)
git clone <our-github-repo>
cd SDP
```

---

## 📞 Questions for Team Discussion

1. **Time Commitment:**
   - What's our graduation deadline?
   - Can we commit 3 months? 6 months?
   - Are we doing this full-time or alongside other courses?

2. **Skills & Interests:**
   - Who's comfortable with cryptography/math (proofs, protocol design)?
   - Who's strong at coding/implementation?
   - Who enjoys writing papers and running experiments?

3. **Goals:**
   - Do we want quick graduation or strong publication?
   - Are we considering PhD afterwards? (If yes, lean toward Path C)
   - Do we care more about learning or about CV/publication count?

4. **Realistic Assessment:**
   - Can we accept current paper might only be workshop-level?
   - Are we willing to do 3-6 months more work for novelty?
   - Do we have advisor support for extended timeline?

---

## 📚 Additional Resources

### **Key Papers to Read:**
1. **Bonawitz et al. (2017)** - "Practical Secure Aggregation for Privacy-Preserving Machine Learning" (CCS)
   - The classical secure aggregation protocol we should replace
2. **Chen et al. (2024)** - The ONE paper on PQC secure aggregation
3. **McMahan et al. (2017)** - "Communication-Efficient Learning of Deep Networks from Decentralized Data"
   - Original FedAvg paper

### **Tools & Libraries:**
- **TensorFlow Federated:** https://www.tensorflow.org/federated
- **PySyft:** https://github.com/OpenMined/PySyft
- **liboqs (Open Quantum Safe):** https://openquantumsafe.org/
- **NIST PQC Standards:** https://csrc.nist.gov/projects/post-quantum-cryptography

---

## 🎬 Next Immediate Actions

### **By End of This Week:**
- [ ] All team members read this README
- [ ] All read **05_paper_discussion_byzantine_robust_fl.md** (critical)
- [ ] Schedule 2-hour team meeting
- [ ] Each person comes prepared with: Time availability, preferred path (A/B/C), questions

### **Team Meeting Agenda:**
1. Discuss honestly: What's realistic given our constraints?
2. Vote on Path A / B / C
3. If Path A: Assign tasks (overhead analysis, new experiments, writing)
4. If Path B: Choose Option B1 (adaptive defense) or B2 (lightweight aggregation)
5. If Path C: Commit to 6-12 months, start with Bonawitz paper study group
6. Set next meeting date and deliverables

---

## 💬 Contact & Collaboration

- **GitHub Repo:** https://github.com/asneem1234/SDP.git
- **Main Branch:** `main`
- **Workflow:** Create feature branches, submit pull requests for review

**Branching Strategy:**
```bash
# For experiments
git checkout -b experiments/overhead-analysis

# For writing
git checkout -b paper/limitations-section

# For new features
git checkout -b feature/adaptive-fingerprinting
```

---

## 🎓 Final Thoughts

**The Honest Truth:**
Our current paper combines existing techniques (Kyber + gradient fingerprinting + validation). This is valuable work, but it's "incremental" not "novel." That's okay! Most research is incremental. But we need to:

1. **Be honest** about what we've done (implementation + empirical study)
2. **Set realistic expectations** (workshops not top conferences for current version)
3. **Decide together** how much more we want to invest

**The Opportunity:**
If we choose Path C, we'd be working on a genuinely unsolved problem. Only 1 paper exists on PQC secure aggregation. This is wide-open research space. But it requires serious commitment.

**No Wrong Choice:**
- Path A is smart if graduation is priority
- Path B is balanced for learning + publication
- Path C is ambitious for research career

Let's discuss and decide together! 🚀

---

*Last Updated: December 13, 2025*  
*Document Author: Team Lead (from conversation history & analysis)*  
*Status: Planning Phase - Decision Pending*
