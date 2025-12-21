---
type: architecture-decision-record
decision_date: 2025-12-20
status: adopted
beth_topics:
  - architecture-decision
  - provenance-first
  - invariants
  - sil-architecture
---

# Architecture Decision Record: Provenance-First Model with Invariants Over Layers

**Decision Date:** December 20, 2025
**Status:** ✅ Adopted
**Supersedes:** Canonical 7-layer model (L0=Substrate)
**Authority:** Scott Senkeresty (Founder), TIA (Chief Semantic Agent)

---

## Decision

**ADOPTED:** The **Provenance-First layer model** with **Invariants Over Layers** framework as SIL's canonical architecture.

### Provenance-First Layer Model

```
L6: Reflection       Learning from execution (observability)
L5: Execution        Agents working under constraints
L4: Composition      Cross-domain integration (Pantheon IR)
L3: Intent           What we're accomplishing (contracts)
L2: Trust            Who can do what (TAP, Authorization)
L1: Meaning          Embeddings, types, similarity (Beth)
L0: Provenance       Everything has lineage (GenesisGraph)
─────────────────────────────────────────────────────────────
L-1: Substrate       Physical/computational reality (Philbrick, optional)
```

### Invariants Framework

| Invariant | Prevents | Enforcement |
|-----------|----------|-------------|
| Everything has lineage | Epistemic collapse | GenesisGraph |
| Reasoning is inspectable | Black box dictatorship | Reveal |
| Computation is grounded | Hallucinated science | Morphogen |
| Contracts are explicit | Brittle complexity | Agent Ether |
| Efficiency is sustainable | Compute as privilege | Beth + Reveal |

### Dual-Frame Synthesis

- **Use Layers For:** Organizing documentation, explaining tool relationships, onboarding, navigation
- **Use Invariants For:** Architectural decisions, design reviews, mission alignment, "should we build X?" questions

---

## Context

### The Problem

As of December 14, 2025, SIL documentation contained **4+ competing layer models**:

1. **Original Semantic OS** (6 layers, L0=Semantic Memory)
2. **Canonical Glossary** (7 layers, L0=Substrate/Philbrick)
3. **Feedback Loops** (6 layers, no L0)
4. **Observability** (8 layers with L4.5!)

This created:
- **P0 Blocker:** SEMANTIC_OS_ARCHITECTURE.md had TWO conflicting systems in one document
- **Confusion:** Website couldn't launch with contradictory architecture
- **Assignment Chaos:** "Where does tool X belong?" debates never resolved
- **Mission Drift:** Architecture serving project organization, not mission

### The Analysis Process (Dec 14-20, 2025)

**6-session rigorous evaluation arc:**

1. **enchanted-centaur-1214:** Discovered 4 competing models
2. **heating-snow-1214:** Proposed provenance-first alternative
3. **scorching-gust-1215:** Created evaluation framework
4. **oracular-throne-1215:** Scored all models (4.15 vs 3.05)
5. **pulsing-horizon-1215:** Proposed Invariants Over Layers
6. **turbulent-current-1215:** Validated framework (90% confidence)

**Deep research synthesis:**

7. **prairie-gust-1220:** Verified P0 blocker, documented coherence gaps
8. **enchanted-throne-1220:** Comprehensive landscape mapping
9. **stellar-supernova-1220:** Confidence assessment (85-90%)

---

## Alternatives Considered

### Alternative 1: Keep Canonical Model (L0=Substrate)

**Score:** 3.05 / 5.00

**Pros:**
- Most complete documentation
- Hardware grounding intuitive
- Philbrick placement clear

**Cons:**
- Product-centric ("where do projects fit?" not "how do we trust AI?")
- Lower score on problem fit (3/5 vs 5/5)
- Component assignment chaos unresolved
- Doesn't address LLM coexistence directly

**Rejected:** Lower score, doesn't serve mission as well

---

### Alternative 2: Create New Model From Scratch

**Outcome:** Unknown (not attempted)

**Pros:**
- Could address all known issues
- Fresh start

**Cons:**
- **Analysis paralysis** (never settle on a model)
- **Time cost** (another 6-session arc, 2+ weeks)
- **Unlikely to score higher** than already-validated 4.15
- **Delays website launch** and real work

**Rejected:** Diminishing returns, opportunity cost too high

---

### Alternative 3: Layers Only (No Invariants)

**Outcome:** Organization without mission enforcement

**Pros:**
- Simpler (one framework, not two)
- Familiar mental model

**Cons:**
- **No mission alignment check** ("should we build X?" unanswered)
- **Layers answer "where"** but not "why"
- **Misses core insight:** both frames needed for different purposes

**Rejected:** Incomplete solution

---

### Alternative 4: Invariants Only (No Layers)

**Outcome:** Mission without organization

**Pros:**
- Mission-aligned by default
- Clear decision framework

**Cons:**
- **No codebase organization** ("where does this code belong?" unanswered)
- **Developer confusion** (no navigation structure)
- **Documentation chaos** (no hierarchy)

**Rejected:** Developers need structure

---

## Evaluation Criteria & Scores

### Weighted Scoring Framework

| Criterion | Weight | Provenance-First | Canonical |
|-----------|--------|------------------|-----------|
| Problem Fit | 30% | 5 | 3 |
| Conceptual Clarity | 25% | 4 | 4 |
| Component Coherence | 20% | 4 | 2 |
| Extension Path | 15% | 4 | 4 |
| Implementation Guidance | 10% | 3 | 3 |
| **Weighted Total** | | **4.15** | **3.05** |

### Detailed Scoring

**Problem Fit (5/5 vs 3/5):**
- Provenance-First **directly addresses** LLM coexistence, trust, cross-domain work
- Canonical addresses these **implicitly**, not explicitly
- **Gap:** 2 points (66% improvement)

**Component Coherence (4/5 vs 2/5):**
- Provenance-First: "Tools span layers" resolves assignment debates
- Canonical: Component assignment chaos (Agent Ether at L3 vs L6, Beth at L1 vs L3)
- **Gap:** 2 points (100% improvement)

**Overall Gap:** 1.1 points (36% improvement)

---

## Evidence Supporting Decision

### Evidence 1: Perfect Triple Mapping (Mission Alignment)

| THE_FORK (Failures) | SCOPE_OF_HOPE (Pillars) | Invariants | Tool |
|---------------------|--------------------------|------------|------|
| Collapse of shared reality | Provenance Over Promises | Everything has lineage | GenesisGraph |
| Black box governance | Glass Box Over Black Box | Reasoning is inspectable | Reveal |
| Brittle complexity | Contracts Over Chaos | Contracts are explicit | Agent Ether |
| Trapped intelligence | Grounded Over Hallucinated | Computation is grounded | Morphogen |
| Unsustainable compute | Sustainable Over Wasteful | Efficiency is sustainable | Beth |

**Significance:** 1:1:1 mapping across three independently authored documents proves the invariants are a **distillation of existing mission commitments**, not retrofitting.

---

### Evidence 2: Validation Report Findings

From **turbulent-current-1215 VALIDATION_REPORT.md**:

> "The five invariants map 1:1 to the five structural failures SIL committed to fix in THE_FORK.md. This is not coincidence—it's architectural coherence."

**Confidence:** 90% on frame validity, 67% on implementation maturity (3.5/5 invariants production-ready)

---

### Evidence 3: Founder Alignment

From **heating-snow-1214** session:

> Scott's gut reaction: "Provenance when I hear SOS"

**Significance:** Founder intuition aligns with problem-centric model (L0=Provenance), not product-centric (L0=Substrate)

---

### Evidence 4: Tools Span Layers Insight

Historical chaos explained:

| Tool | Layers Touched | Why "Where does X go?" was intractable |
|------|----------------|----------------------------------------|
| Beth | L1 (Meaning) + L0 (Provenance) | Semantic search + knowledge lineage |
| Reveal | L6 (Reflection) + L4 (Composition) | Observability + structure navigation |
| TIA | L3 (Intent) + L5 (Execution) + L6 (Reflection) | Orchestration spans multiple concerns |

**Insight:** Tools are like Unix utilities (`grep`, `ls`, `ps`)—they span layers based on function. Trying to assign them to single layers was a category error.

---

### Evidence 5: Implementation Status (Honest Assessment)

| Invariant | Tool | Status | Confidence |
|-----------|------|--------|------------|
| Everything has lineage | GenesisGraph v0.3.0 | ✅ Production (666+ tests) | High (85%) |
| Reasoning is inspectable | Reveal v0.25.0 | ✅ Production (100x proven) | High (85%) |
| Efficiency is sustainable | Beth + Reveal | ✅ Production (25x proven) | High (85%) |
| Computation is grounded | Morphogen v0.12.0 | 🟡 Prototype (1,705 tests) | Medium (60%) |
| Contracts are explicit | Agent Ether 0.1.0-alpha | 🔴 Spec only (0 Python files) | Low (20%) |

**Overall Enforcement:** 67% (3.5/5 invariants production-ready)

**Known Gap:** Agent Ether is specification-only. This is documented honestly in the architecture.

---

## Decision Rationale

### Why Provenance-First Wins

1. **Mission Alignment** (36% score improvement)
   - Problem-centric: "How do we trust AI?"
   - Not product-centric: "Where do our 12 projects fit?"

2. **Resolves Component Chaos** (100% improvement on coherence)
   - "Tools span layers" explains historical confusion
   - No more intractable "where does X go?" debates

3. **Founder Intuition**
   - "Provenance when I hear SOS"
   - Gut reaction matches validated analysis

4. **Perfect Mission Mapping**
   - 1:1:1 across THE_FORK, SCOPE_OF_HOPE, Invariants
   - Not retrofitting—discovering implicit structure

5. **Practical Decision Framework**
   - Chief Scientist Test (6 questions)
   - Actionable, memorable, mission-aligned

6. **Dual-Frame Elegance**
   - Layers for organization
   - Invariants for mission
   - Both needed, neither sufficient alone

---

### Why Invariants Complement Layers

**The Synthesis:**

Layers and invariants serve **different purposes**:

| Question | Use Layers | Use Invariants |
|----------|-----------|---------------|
| Where does this code belong? | ✅ | |
| How do these systems communicate? | ✅ | |
| Does this serve the mission? | | ✅ |
| Does this prevent the worst day? | | ✅ |
| Would this create a god or colleague? | | ✅ |

**Not competing—complementary.**

---

## Implementation Status

### Completed (Dec 20, 2025)

✅ **SEMANTIC_OS_ARCHITECTURE.md** rewritten with Provenance-First model
✅ **Architecture Decision Record** (this document)
✅ **Confidence Assessment** (85-90% validation)
✅ **Documentation sync** to sil-website

### Known Gaps

🔴 **Agent Ether** (spec only, no implementation)
- **Gap Impact:** "Contracts are explicit" invariant not enforced
- **Priority:** CRITICAL (only invariant without tooling)
- **Timeline:** 16 weeks (Q1 2026) for Phases 1-3

🟡 **Morphogen** (prototype, not production-distributed)
- **Status:** v0.12.0 with 1,705 tests, 39 domains
- **Timeline:** v1.0 targeted Q2 2026

### Next Actions

**Immediate** (this week):
1. ✅ Fix P0 blocker (SEMANTIC_OS_ARCHITECTURE.md)
2. ✅ Create ADR (this document)
3. ⏳ Verify doc consistency (SIL_GLOSSARY, others)
4. ⏳ Agent Ether Roadmap
5. ⏳ Update project status

**Near-term** (30 days):
6. Clarify USIR status (is Reveal the implementation?)
7. Start Agent Ether Phase 1 (Registry + Metadata, 4 weeks)
8. Update remaining canonical docs

**Medium-term** (Q1 2026):
9. Morphogen v1.0 push
10. Agent Ether Phases 1-3 complete
11. Invariants Dashboard (track enforcement status)

---

## Risks & Mitigations

### Risk 1: Implementation Never Happens

**Risk:** Agent Ether stays spec-only indefinitely, enforcement remains 67%

**Mitigation:**
- Prioritize Agent Ether Phase 1 (Registry, 4 weeks)
- Roadmap with concrete milestones
- Track progress publicly

**Likelihood:** Low (roadmap exists, priority established)

---

### Risk 2: Too Complex for Adoption

**Risk:** Dual-frame (layers + invariants) confuses users, developers choose simpler alternatives

**Mitigation:**
- Make tools ridiculously useful (Reveal = 100x efficiency already proven)
- Progressive disclosure in documentation
- Clear decision framework (Chief Scientist Test)

**Likelihood:** Low (tools already proven valuable)

---

### Risk 3: Future Model Supersedes This

**Risk:** New architectural insight in 2026 invalidates this decision

**Mitigation:**
- This work is **validated** (90%), not speculative
- 6-session rigorous process, not gut decision
- Lock it in, prevent churn

**Likelihood:** Low (process quality high, confidence 85-90%)

---

### Risk 4: Mission Drift

**Risk:** Future decisions ignore invariants, framework becomes dead documentation

**Mitigation:**
- Chief Scientist Test as **blocking checklist** for design reviews
- Invariants Dashboard tracks enforcement status
- Architecture reviews reference this ADR

**Likelihood:** Medium (requires discipline)

---

## Success Criteria

### Immediate (This Week)

✅ P0 blocker resolved (SEMANTIC_OS_ARCHITECTURE.md internally consistent)
✅ ADR created and adopted
⏳ Website can launch with clear architecture

### Near-Term (30 Days)

- Related docs aligned (SIL_GLOSSARY, SEMANTIC_FEEDBACK_LOOPS, etc.)
- Agent Ether Phase 1 started
- Project status reflects decision

### Medium-Term (Q1 2026)

- Agent Ether Phases 1-2 complete (basic enforcement)
- Morphogen v1.0 production-distributed
- 80%+ invariant enforcement (4/5 production)

### Long-Term (1 Year)

- 100% invariant enforcement (5/5 production)
- External validation (users/partners adopt framework)
- Published architecture paper (validation beyond SIL)

---

## References

### Decision Process Documents

- `/sessions/enchanted-centaur-1214/` — 4 models discovered
- `/sessions/heating-snow-1214/` — Provenance-First proposed
- `/sessions/scorching-gust-1215/` — Evaluation framework
- `/sessions/oracular-throne-1215/` — Model scoring (4.15)
- `/sessions/pulsing-horizon-1215/` — Invariants Over Layers
- `/sessions/turbulent-current-1215/` — Validation (90%)
- `/sessions/stellar-supernova-1220/` — Confidence assessment (85-90%)

### Architecture Documents

- `/docs/architecture/models/INVARIANTS_OVER_LAYERS.md`
- `/docs/architecture/models/MODEL_EVALUATION.md`
- `/docs/architecture/models/PROVENANCE_FIRST.md`
- `/docs/architecture/models/VALIDATION_REPORT.md`

### Mission Grounding

- `/foundation/pitch/THE_FORK.md` — Five structural failures
- `/foundation/SCOPE_OF_HOPE.md` — Five pillars
- `/foundation/pitch/VISION_HOPE.md` — Glass Box future
- `/foundation/pitch/VISION_REALITY.md` — Grey Fog risks

### Canonical Documentation

- `/docs/foundations/SIL_SEMANTIC_OS_ARCHITECTURE.md` (v3.0, updated 2025-12-20)
- `/docs/foundations/SIL_GLOSSARY.md`

---

## Conclusion

After rigorous 6-session evaluation, cross-validation against mission documents, and confidence assessment scoring 85-90%, the **Provenance-First model with Invariants Over Layers** is adopted as SIL's canonical architecture.

**The decision is grounded in:**
- Quantitative scoring (4.15 vs 3.05)
- Qualitative mission alignment (perfect 1:1:1 mapping)
- Founder intuition ("provenance when I hear SOS")
- Implementation reality (67% enforcement today, clear path to 100%)
- Process quality (9 sessions, systematic analysis)

**The known gaps are documented:**
- Agent Ether is spec-only (16-week roadmap)
- Morphogen is prototype (v1.0 Q2 2026)

**The direction is right. The gaps are known. The path forward is clear.**

This architecture serves the mission: **building Timeline B (Glass Box future) instead of defaulting to Timeline A (Grey Fog)**.

---

**Adopted:** 2025-12-20
**Authority:** Scott Senkeresty (Founder), TIA (Chief Semantic Agent)
**Status:** ✅ **CANONICAL**
**Review Date:** 2026-Q1 (after Agent Ether Phase 1)
