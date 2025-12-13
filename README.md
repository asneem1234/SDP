# Hey Vaishu and Yasaswini! 👋

So we're doing our **SDP (Senior Design Project)** together for the next **4 months** and I wanted to give you both a complete picture of what we're working on and where everything is.

---

## 🎯 Our Problem Statement

**"Byzantine-Robust Federated Learning with Post-Quantum Cryptography"**

I know that sounds like a lot of buzzwords lol, but let me break it down from scratch...

---

## 🤖 Quick ML Recap (The Problem)

You know how machine learning works right? We collect tons of data, train a model, and boom - we have an AI that can predict stuff.

**But here's the issue:** All that data needs to be in one place. Like imagine:
- Hospitals want to train an AI to detect cancer
- Hospital A has 10,000 patient records
- Hospital B has 15,000 patient records
- Hospital C has 8,000 patient records

**Traditional ML approach:** Send all patient data to one central server, train the model there.

**The problem?** 
- 🚫 **Privacy violation:** Patient data is SUPER sensitive. You can't just send it around.
- 🚫 **Security risk:** If that central server gets hacked, 33,000 patient records are exposed.
- 🚫 **Legal issues:** GDPR, HIPAA - there are laws against sharing medical data like this.

So basically, **the data is NOT secure** in traditional ML. We're putting everything in one basket and hoping nobody steals it.

---

## 🌐 Enter Federated Learning (2016)

In **2016**, Google researchers said "wait, what if we DON'T send the data?"

**Federated Learning** is this genius idea:
- Each hospital keeps their data LOCAL (never leaves their building)
- Each hospital trains the model on THEIR OWN data
- They only send the **model updates** (like, "increase this weight by 0.3") to a central server
- The server combines all updates to improve the global model
- Nobody sees anyone else's raw data! 🎉

**It's like:** 3 students study for an exam separately at home, then they meet and share only their notes/tips (not their personal study materials). Everyone benefits but privacy is maintained.

Cool right? This changed everything for privacy-preserving AI.

---

## 📂 What's in Our Files?

Let me walk you through what I've researched and documented so far...

### **brainstorm/01_what_is_federated_learning.md** (6,753 lines)

**This is THE intro document.** It explains:

**Why we need FL in the first place:**
- Traditional ML = send all data to central server (privacy nightmare)
- FL = keep data local, only share model updates (privacy preserved!)
- Real examples: Google uses this for your phone keyboard (learns your typing without seeing your messages)

**How FL actually works:**
- The **FedAvg algorithm** (Federated Averaging) - the main algorithm from 2016
- Mathematical formulation (don't worry, it's explained with analogies)
- Each client trains locally, sends weights/gradients to server
- Server averages them and sends back the global model

**Types of FL:**
- **Horizontal FL:** Everyone has same features but different data (like different hospitals with same patient record format)
- **Vertical FL:** Different features (like bank has financial data, hospital has health data about SAME people)
- **Transfer Learning:** Learn from one domain, apply to another

**Real-world applications:**
- Google Gboard (keyboard predictions)
- Healthcare (hospitals collaborating without sharing patient data)
- Finance (banks detecting fraud together)

**The challenges we face:**
- Communication is expensive (sending millions of parameters over network)
- Non-IID data (everyone's data is different)
- Security issues (malicious clients can attack)
- Privacy concerns

**Read this first!** It's the foundation for everything else.

---

### **brainstorm/02_post_quantum_cryptography_basics.md** (8,479 lines)

**Ok so after understanding FL, we need to understand WHY we need Post-Quantum Crypto.**

**The quantum threat:**
- Right now, we use RSA and ECC for encryption (that's what HTTPS uses)
- Problem: When quantum computers arrive (maybe 10-15 years), they'll break ALL current encryption in minutes
- Shor's algorithm (quantum algorithm) can factor large numbers super fast → breaks RSA
- We need **quantum-safe** encryption NOW before it's too late

**What's Post-Quantum Cryptography (PQC)?**
- New encryption algorithms that even quantum computers can't break
- Based on hard math problems: Lattices, Hash functions, Codes, Multivariate polynomials
- NIST (US govt) standardized these in 2024

**The algorithms we're using:**
- **Kyber-512:** For encryption (key exchange)
  - 1,184-byte public keys (vs 32 bytes for traditional ECC)
  - Based on "lattice" math - very hard for quantum computers
- **Dilithium-2:** For digital signatures
  - 3,293-byte signatures (way bigger than RSA!)
  - Also lattice-based

**The problem:** PQC has HUGE keys and signatures (10-50× bigger than current crypto). This is a big deal for FL where we're sending stuff over networks constantly.

This file has all the technical details, comparison tables, security levels, etc.

---

### **brainstorm/02a_quantum_computing_and_pqc_algorithms.md** (~1,199 lines)

**Deep dive into quantum computing and PQC algorithms.**

**Part 1: Quantum Computing Basics**
- What is superposition? (Coin spinning = both heads & tails simultaneously)
- What is entanglement? (Magic coins linked across distance)
- Why exponential speedup? (3 qubits = all 8 states at once)
- Decoherence problem (qubits are fragile, need -273°C)

**Part 2: Shor's Algorithm - The RSA Killer**
- How factoring works (91 = 7×13 is easy, 617-digit numbers are impossible)
- Period-finding trick
- RSA-2048: 300 trillion years classically → 8-10 hours with quantum! ❌
- Breaks RSA, ECC, Diffie-Hellman

**Part 3: Grover's Algorithm - The Search Speedup**
- √N speedup for search
- AES-128: 2^128 → 2^64 (INSECURE!)
- AES-256: 2^256 → 2^128 (still safe) ✅

**Part 4: PQC Algorithms (The Solutions)**
- **Kyber-768** (encryption): 1,184 byte keys, lattice-based, NIST standard
- **Dilithium-3** (signatures): 1,952 byte keys, lattice-based, NIST standard
- **SPHINCS+** (hash-based): 7,856 bytes, slow but ultra-secure
- **Classic McEliece** (code-based): 1.3 MB keys (impractical)
- Full comparison table + why lattice crypto wins

**Part 5: How PQC Secures FL**
- Security proofs (breaking Kyber = solving LWE = impossible)
- Why quantum computers can't break lattice problems
- Concrete FL example with 10-year timeline

**Part 6: 8 Major Challenges in PQC**
1. Large keys (37× bigger) → bandwidth explosion
2. Slower ops (2-14×) → battery drain
3. Immaturity (only 8 years old vs RSA's 48) → unknown attacks possible
4. Implementation complexity → side-channel vulnerabilities
5. Slow deployment → industry inertia
6. Patents → legal uncertainty
7. Timeline uncertainty → when to migrate?
8. **PQC Secure Aggregation** → No good solution yet! (Our research gap)

**Includes 2 video resources at the end**

---

### **brainstorm/03_choosing_our_research_direction.md** (~489 lines) ⭐ **READ THIS**

**DECISION TIME!** This is where we figure out what to actually work on.

**The Brutal Truth:**
- FL is NOT perfect (12 challenges)
- PQC is NOT perfect (8 challenges)
- Byzantine defenses are NOT perfect (accuracy loss, no guarantees)

**The Major Trade-offs:**
1. **Security vs Privacy vs Efficiency** (Can only pick 2!)
2. **PQC Security vs Bandwidth** (37× larger keys)
3. **Byzantine Defense vs Accuracy** (7% accuracy drop)
4. **Research Depth vs 4-Month Timeline** (What's realistic?)

**4 Options with Full Analysis:**

**Option 1: Byzantine + PQC** ✅ **RECOMMENDED**
- Combine Byzantine-robust FL with PQC without exploding communication
- Realistic for 4 months (Path B)
- Novel (nobody's done this efficiently)
- Satisfies crypto requirement
- Clear 16-week plan included

**Option 2: Compact PQC**
- Design smaller keys specifically for FL
- ⚠️ Too math-heavy for 4 months
- PhD-level difficulty

**Option 3: Byzantine + Non-IID**
- Byzantine defense that works with Non-IID data
- ❌ No cryptography component (doesn't satisfy requirement)

**Option 4: Privacy + Byzantine**
- Detect attacks while preserving privacy
- ❌ Unsolved research problem, impossible in 4 months

**Includes:**
- Detailed trade-off analysis
- Concrete 16-week timeline for Option 1
- Discussion questions to help decide
- Risk assessment for each option

**THIS FILE HELPS US DECIDE WHAT TO WORK ON!**

---

### **brainstorm/03_choosing_our_research_direction.md** (~489 lines) ⭐ **READ THIS**

**DECISION TIME!** This is where we figure out what to actually work on.

**The Brutal Truth:**
- FL is NOT perfect (12 challenges)
- PQC is NOT perfect (8 challenges)
- Byzantine defenses are NOT perfect (accuracy loss, no guarantees)

**The Major Trade-offs:**
1. **Security vs Privacy vs Efficiency** (Can only pick 2!)
2. **PQC Security vs Bandwidth** (37× larger keys)
3. **Byzantine Defense vs Accuracy** (7% accuracy drop)
4. **Research Depth vs 4-Month Timeline** (What's realistic?)

**4 Options with Full Analysis:**

**Option 1: Byzantine + PQC** ✅ **RECOMMENDED**
- Combine Byzantine-robust FL with PQC without exploding communication
- Realistic for 4 months (Path B)
- Novel (nobody's done this efficiently)
- Satisfies crypto requirement
- Clear 16-week plan included

**Option 2: Compact PQC**
- Design smaller keys specifically for FL
- ⚠️ Too math-heavy for 4 months
- PhD-level difficulty

**Option 3: Byzantine + Non-IID**
- Byzantine defense that works with Non-IID data
- ❌ No cryptography component (doesn't satisfy requirement)

**Option 4: Privacy + Byzantine**
- Detect attacks while preserving privacy
- ❌ Unsolved research problem, impossible in 4 months

**Includes:**
- Detailed trade-off analysis
- Concrete 16-week timeline for Option 1
- Discussion questions to help decide
- Risk assessment for each option

**THIS FILE HELPS US DECIDE WHAT TO WORK ON!**

---

### **brainstorm/05_paper_discussion_byzantine_robust_fl.md** ⚠️ **OPTIONAL - Advanced**

**⚠️ NOTE:** This file discusses a previous paper draft and is NOT essential for getting started. Only read this if you want deep context on past work. **Skip this initially and focus on files 01, 02, 02a, and 03 first!**

**What's in here (if you're curious later):**
- Previous paper analysis: "Byzantine-Robust FL with PQC"
- 10 issues identified with that approach
- Why it lacked novelty
- Path A/B/C discussion (now superseded by file 03)

**What we have so far:**
- Paper title: "Byzantine-Robust Federated Learning Under Non-IID Data: A Post-Quantum Three-Layer Defense"
- Results: 93.2% accuracy with 40% malicious clients
- Defense: Gradient fingerprinting + Cosine similarity + Validation filtering
- PQC: Using Kyber-512 and Dilithium-2

**The 10 issues I identified:**

1. **PQC contribution is unclear** - We're just using Kyber for encrypted communication (like using HTTPS). That's not a research contribution, that's just... using a library lol.

2. **We're NOT doing secure aggregation** - Big difference between "encrypted communication" and "secure aggregation protocol". We're doing the first, not the second.

3. **Missing PQC overhead analysis** - We don't compare: How much slower/bigger is Kyber vs RSA/ECC? What's the bandwidth overhead? This is critical!

4. **Limited evaluation:**
   - Only MNIST dataset (too simple)
   - Only label-flipping attack (need gradient scaling, backdoor)
   - Only 5 clients (need 50, 100 for scalability)

5. **No formal security proofs** - We're not proving anything mathematically, just showing experimental results

6. **Scalability concerns** - Gradient fingerprinting is O(n²) complexity (every client compared with every other client). With 100 clients = 10,000 comparisons!

7. **Validation set bias** - Where does validation data come from? We don't address this.

8. **Missing ablation studies** - What if we remove fingerprinting? What if we change similarity threshold? Need to test each component.

9. **No comparison with PQC-specific defenses** - We compare with non-PQC methods only

10. **Writing/presentation issues** - Need better structure, clearer contribution statement

**The harsh truth:**
Our paper **combines existing techniques without novel algorithmic contributions.**
- Gradient fingerprinting = existing (Shen et al.)
- Kyber encryption = just using NIST standard
- Validation filtering = existing
- Combining them = incremental work, not novel research

**Rejection risk: 70-80%** at top conferences (IEEE S&P, USENIX Security, CCS)

**BUT** this doesn't mean it's worthless! It means we need to either:
- Accept it's incremental and target workshops (lower bar)
- OR add real novelty (spend 3-6 more months)

**Three paths forward:**

**Path A (2-3 weeks):** Polish current work, reframe as "empirical study", submit to workshops
- Pros: Fast graduation, low stress
- Cons: Lower-tier publication

**Path B (2-3 months):** Add ONE novel contribution
- Option 1: Design adaptive fingerprinting (learns attack patterns)
- Option 2: Design lightweight PQC aggregation (for <100 clients)
- Pros: Solid publication, good learning
- Cons: 3 months extra work

**Path C (6-12 months):** Design full PQC secure aggregation protocol
- This is Gap 1 - the big unsolved problem
- Requires deep crypto knowledge and 6-12 months
- Pros: PhD-level work, high impact, addresses real problem
- Cons: Major commitment, might delay graduation

**We need to decide together which path makes sense for us.**

---

### **brainstorm/06_compact_pqc_for_federated_learning.md** (~60KB) ⚠️ **OPTIONAL - Very Advanced**

**⚠️ NOTE:** This is PhD-level deep dive into lattice mathematics and compact PQC design. **NOT required for our 4-month SDP!** Only read if you have deep interest in cryptography theory or are considering Option 2 from file 03. **Definitely skip this initially!**

**What's in here (if you're very interested):**

**The memory/communication problem:**
- Kyber-768 has 1,184-byte public keys
- Traditional ECC-256 has 32-byte keys
- That's **37× bigger!**

**Impact on FL:**
- 100 hospitals doing 10 rounds of FL
- Classical crypto: 32 MB total overhead
- Kyber-768: **540 MB overhead** (17× more!)
- With 1000 clients? Completely impractical.

**Why are PQC keys so large?**
- Lattice crypto needs high dimensions (n=768) for security
- Need to add noise to hide the secret
- All that data = big keys

**What we need for FL:**
- < 200 byte keys (vs 1,184 bytes now)
- < 1 ms operations
- Quantum-safe
- Scalable to 1000+ clients

**The 12 mathematical clues:**
This file explores 12 areas of math where we MIGHT find compact PQC:
1. Non-abelian Hidden Subgroup Problems (most promising, could give ~100 byte keys)
2. Algebraic Geometry beyond isogenies
3. NP-hard problems with trapdoors (holy grail but historically failed)
4. Quantum wasteland problems
5. Non-linear algebraic structures
... and 7 more

Each clue is explained with: What it is, why it could work, current status, potential for FL.

**This is long-term research** - not for our current 4-month SDP, but good to understand if we're considering PhD work later.

---

## 🚨 So Where Are We?

**Current status:**
✅ We have a paper draft  
✅ We have results (93.2% accuracy)  
✅ We have lots of research documentation  
❌ **Paper lacks true novelty**  
❌ Missing overhead analysis  
❌ Limited experiments  
❌ Not doing actual secure aggregation  

**The key question for our team:**
Given we have **4 months for SDP**, which path do we take?

---

## 📋 My Thoughts on Timeline

Since we have **4 months** (not 6-12), I think **Path B is most realistic:**

**Month 1 (Weeks 1-4):** Both of you read all the files, understand FL and PQC basics, align on what we're doing

**Month 2 (Weeks 5-8):** Design ONE novel contribution
- Option: Adaptive gradient fingerprinting (learns attack patterns over rounds)
- OR: Lightweight key amortization for PQC (reuse keys across rounds)

**Month 3 (Weeks 9-12):** Implement + run comprehensive experiments
- Add FEMNIST and CIFAR-10 datasets
- Add gradient scaling and backdoor attacks
- Test with 10, 20, 50 clients
- Measure PQC overhead

**Month 4 (Weeks 13-16):** Paper writing + polishing
- Rewrite contribution section
- Add ablation studies
- Create better figures/tables
- Submit to conference/journal

**Target venues** (for Path B):
- IEEE ICDCS (International Conference on Distributed Computing Systems)
- ACM CODASPY (Conference on Data and Application Security and Privacy)
- Or a good journal if we have more time

---

## 🎯 What You Both Need to Do NOW

### **Week 1 Tasks:**

**Vaishu:**
1. Read this README completely ✅
2. Read **01_what_is_federated_learning.md** (understand FL fundamentals + all 12 challenges) ✅
3. Read **02_post_quantum_cryptography_basics.md** (why PQC is needed) ✅
4. Read **03_choosing_our_research_direction.md** (understand our 4 options) ✅
5. Think: Which option (1-4) makes sense? What are your goals?
6. *(Optional: 02a for quantum deep dive, 05 for paper context)*

**Yasaswini:**
1. Read this README completely ✅
2. Read **01_what_is_federated_learning.md** (FL fundamentals) ✅
3. Read **02_post_quantum_cryptography_basics.md** (crypto fundamentals + quantum threat) ✅
4. Read **03_choosing_our_research_direction.md** (our decision point!) ✅
5. Think: Which option resonates? ML/FL side or crypto/security side?
6. *(Optional: 02a for algorithms deep dive, 05 for paper discussion)*

**All of us:**
- Schedule team meeting (2-3 hours) by end of Week 1
- Discuss honestly: What's realistic in 4 months?
- Decide on Path A or B (Path C is too long for 4-month SDP)
- Align on who does what (I'm thinking Vaishu on algorithm design, Yasaswini on implementation, me on experiments/writing)

---

## 💭 My Honest Opinion

Looking at our 4-month timeline, here's what I think:

**Path A (workshops)** feels like giving up. We've already done so much research, why settle for lower-tier publication?

**Path B (add novelty)** is doable. If we focus on ONE thing:
- Like adaptive fingerprinting that changes thresholds based on detected attack patterns
- Or key amortization (one Kyber exchange for 10 rounds instead of every round)
  
We can make it genuinely novel without needing 6 months.

**Path C (full secure aggregation)** is what I'd LOVE to do if we had more time or were doing PhD. But for SDP? Too risky.

So I'm leaning toward **Path B** - let's add one solid novel contribution and aim for a good conference.

**But this is OUR decision together.** I want to hear what both of you think!

---

## 🤔 Discussion Questions for Our Meeting

1. **Goals:** What do we each want from this SDP?
   - Just graduate with decent project?
   - Strong publication for CV/grad school applications?
   - Deep learning experience even if risky?

2. **Time:** Can we realistically commit to 15-20 hours/week for 4 months?
   - Other courses?
   - Internships/placements?
   - Personal commitments?

3. **Interests:** What excites each of us?
   - More ML/algorithm design side?
   - More crypto/security side?
   - More implementation/coding?
   - More experiments/evaluation?

4. **Skills:** What are we good at?
   - Math/proofs (for novel algorithm design)?
   - Python/PyTorch (for implementation)?
   - Writing/presentation (for paper)?

5. **Risk tolerance:**
   - Are we ok with aiming high and maybe failing?
   - Or prefer safer path with guaranteed decent outcome?

---

## 🛠️ Technical Setup (We'll Do This Later)

When we start actual coding/experiments:

```bash
# Install FL frameworks
pip install torch torchvision tensorflow-federated

# Install PQC libraries
pip install pqcrypto  # For Kyber/Dilithium

# Install utilities
pip install matplotlib pandas numpy scipy

# Clone our repo
git clone https://github.com/asneem1234/SDP.git
cd SDP
```

But this is Week 3-4 stuff. First we need to decide direction!

---

## 📞 Next Steps

**Immediate (This Week):**
- [ ] Vaishu: Read 01.md and 05.md
- [ ] Yasaswini: Read 02.md and 05.md  
- [ ] Schedule team meeting (2-3 hours, can be online)
- [ ] Each person comes with: Preferred path (A/B/C), questions, concerns

**Team Meeting Agenda:**
1. Discuss honestly: What's our goal?
2. Evaluate: What's realistic in 4 months?
3. Decide: Path A or B (probably B)
4. If Path B: Choose which novel contribution (adaptive fingerprinting OR key amortization)
5. Divide work: Who does algorithm design, implementation, experiments, writing
6. Set weekly milestones

---

## 🎓 Final Thoughts

I know this is A LOT of information lol. Don't stress!

**The key takeaway:**
We're working on a cool problem (Byzantine-robust FL with PQC), we've done tons of research already, our current paper needs improvement, but with 4 focused months we can make it genuinely good.

**Not top-tier conference level** (that needs 6-12 months), but **solid conference level** (Path B) is totally achievable.

Let's read, discuss, and decide together!

Looking forward to our meeting! 🚀

---

**P.S.** Reading order (essential files only):
1. This README (you're reading it!) ✅
2. **01_what_is_federated_learning.md** (foundation - ML → FL → challenges) ✅
3. **02_post_quantum_cryptography_basics.md** (crypto basics + quantum threat) ✅
4. **03_choosing_our_research_direction.md** (DECISION TIME - pick our path) ✅

That's it! Those 4 files are all you need to get started.

**P.P.S.** Files 02a, 05, and 06 are **optional** and NOT required for initial understanding:
- **02a:** Quantum computing + PQC algorithms deep dive (good for technical depth, but 03 covers what you need)
- **05:** Previous paper discussion (outdated context - file 03 supersedes this)
- **06:** Compact PQC mathematics (PhD-level, only relevant if choosing Option 2)

**Focus on the 4 essentials first!** (README + 01 + 02 + 03) We can discuss advanced topics later if needed.

---

*Last Updated: December 13, 2025*  
*From: Asneem*  
*To: Vaishu & Yasaswini*  
*Timeline: 4 months (Dec 2025 - March 2026)*  
*Goal: Strong SDP publication* 🎯
