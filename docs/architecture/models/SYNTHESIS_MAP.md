---
title: "Architecture Synthesis Map"
type: meta-documentation
status: current
created: 2025-12-15
session_id: pulsing-horizon-1215
beth_topics:
  - sil-architecture
  - documentation-map
  - synthesis
  - meta-docs
  - progressive-disclosure
summary: Maps which source documents contribute which insights to architectural understanding, enabling future sessions to efficiently build context
---

# Architecture Synthesis Map

**Purpose:** Help future agents/humans efficiently build architectural context without reading everything.

**Philosophy:** Progressive disclosure for documentation. Start with this map, dive deeper only where needed.

---

## Quick Context (30 seconds)

**The architectural question:** How should SIL organize its semantic infrastructure?

**Three competing frames:**
1. **Layer models** (5 variations) - hierarchical organization
2. **Provenance-First** - layer model with provenance at L0
3. **Invariants Over Layers** - guarantees that must hold everywhere

**Current synthesis:** Use layers for organization, invariants for mission alignment.

**Key documents in this directory:**
- `README.md` - Index and decision status
- `LAYER_MODELS_COMPARISON.md` - 5 layer models compared
- `MODEL_EVALUATION.md` - Scoring and analysis
- `PROVENANCE_FIRST.md` - Winning layer model
- `INVARIANTS_OVER_LAYERS.md` - Mission-centric reframe
- `SYNTHESIS_MAP.md` - This file (meta-navigation)

---

## Source Documents → Insights

### Tier 1: Mission Grounding (Read First)

These establish WHY we're building anything. Read these before technical architecture.

| Document | Location | Key Insight | Read Time |
|----------|----------|-------------|-----------|
| **THE_FORK.md** | `foundation/pitch/` | Two futures: Grey Fog vs Glass Box. What SIL must fix vs cannot fix. | 8 min |
| **SCOPE_OF_HOPE.md** | `foundation/` | Complete positioning. Best/worst day. Bounded hope framework. | 15 min |
| **VISION_HOPE.md** | `foundation/pitch/` | What success looks like. Second Enlightenment vision. | 3 min |
| **VISION_REALITY.md** | `foundation/pitch/` | Honest limits. Structural failures we're obligated to fix. | 3 min |

**After reading these, you understand:**
- Best day: Shared reality, scientific renaissance, auditable governance
- Worst day: Epistemic collapse, black box dictatorship, "god off the mountain"
- What SIL can/cannot fix
- The "colleague not god" principle

### Tier 2: Technical Vision (Read Second)

These explain WHAT we're building at the technical level.

| Document | Location | Key Insight | Read Time |
|----------|----------|-------------|-----------|
| **SIL_VISION_COMPLETE.md** | `staging/vision/` | Semantic OS overview. Founder's role. Design principles. | 8 min |
| **SIL_MORPHOGEN_PROJECT.md** | `staging/canonical/` | Universal translator. Turing's morphogens. Deterministic computation. | 12 min |
| **SIL_CIVILIZATIONAL_SYSTEMS_ENGINEERING.md** | `staging/canonical/` | Scale of ambition. 50-year thinking. Software engineering for civilization. | 15 min |

**After reading these, you understand:**
- Semantic OS components (Memory, USIR, Domains, Agents, Engines, Interfaces)
- Morphogen as "universal translator" for scientific ideas
- Why SIL builds infrastructure, not apps
- The Turing lineage

### Tier 3: Architecture Models (Read Third)

These are the specific architectural proposals being evaluated.

| Document | Location | Key Insight | Read Time |
|----------|----------|-------------|-----------|
| **LAYER_MODELS_COMPARISON.md** | This directory | 5 layer models side-by-side. Historical evolution. | 10 min |
| **MODEL_EVALUATION.md** | This directory | Scoring criteria. Why Provenance-First won. | 8 min |
| **PROVENANCE_FIRST.md** | This directory | The winning layer model. L0=Provenance. Open questions answered. | 10 min |
| **INVARIANTS_OVER_LAYERS.md** | This directory | Mission-centric reframe. Guarantees over structure. | 12 min |

**After reading these, you understand:**
- Why 5 different layer models emerged
- How they were evaluated (criteria, weights, scores)
- Why Provenance-First scored highest
- The invariants alternative frame

### Tier 4: Session Context (Reference as Needed)

Session READMEs that contributed specific insights.

| Session | Key Contribution |
|---------|------------------|
| `enchanted-centaur-1214` | Discovered 4 competing models existed |
| `heating-snow-1214` | Proposed provenance-first model |
| `coral-shine-1212` | "3 critical missing subsystems" |
| `brewing-sleet-1212` | "Layer 1 is the glue" insight |
| `noble-kraken-1125` | COGNITIVE_OS_MASTER_MAP (696 lines) |
| `scorching-gust-1215` | Created comparison framework |
| `oracular-throne-1215` | Completed evaluation, scored models |
| `pulsing-horizon-1215` | Invariants over layers proposal |
| `turbulent-current-1215` | **Validated invariants frame**, identified Agent Ether gap |

---

## Reading Paths by Goal

### Path A: "Why does SIL exist?"
```
THE_FORK.md → VISION_HOPE.md → VISION_REALITY.md
(14 min total)
```

### Path B: "What is the technical architecture?"
```
SIL_VISION_COMPLETE.md → LAYER_MODELS_COMPARISON.md → PROVENANCE_FIRST.md
(28 min total)
```

### Path C: "How should I think about architecture decisions?"
```
THE_FORK.md → INVARIANTS_OVER_LAYERS.md
(20 min total)
```

### Path D: "Full context for architectural work"
```
THE_FORK.md → SIL_VISION_COMPLETE.md → MODEL_EVALUATION.md → INVARIANTS_OVER_LAYERS.md
(38 min total)
```

### Path E: "I need to understand Morphogen"
```
SIL_MORPHOGEN_PROJECT.md (12 min)
Optionally: SIL_CIVILIZATIONAL_SYSTEMS_ENGINEERING.md for scale context
```

---

## Key Concepts Quick Reference

### The Five Invariants

| Invariant | Enforced By | Prevents |
|-----------|-------------|----------|
| Everything has lineage | GenesisGraph | Epistemic collapse |
| Reasoning is inspectable | Glass Box (USIR/Reveal) | Black box dictatorship |
| Computation is grounded | Morphogen | Hallucinated science |
| Contracts are explicit | Agent Ether | Brittle complexity |
| Efficiency is sustainable | Reveal + Beth | Compute as privilege |

### The Provenance-First Stack

```
L6: Reflection       - Learning from execution
L5: Execution        - Agents working under constraints
L4: Composition      - Cross-domain integration (Pantheon IR)
L3: Intent           - What we're accomplishing (contracts)
L2: Trust            - Who can do what (TAP, Authorization)
L1: Meaning          - Embeddings, types, similarity (Beth)
L0: Provenance       - Everything has lineage (GenesisGraph)
─────────────────────────────────────────────────────────────
L-1: Substrate       - Physical/computational reality (Philbrick)
```

### The Chief Scientist Test

Before approving architecture, ask:
1. Does this maintain traceable lineage?
2. Is reasoning inspectable?
3. Is computation connected to reality?
4. Are assumptions explicit?
5. Is this sustainable at scale?
6. Does this keep humans as conductors?

---

## Document Health

| Document | Last Updated | Status | Needs Review If... |
|----------|--------------|--------|-------------------|
| THE_FORK.md | 2025-11-29 | Stable | Mission changes |
| SCOPE_OF_HOPE.md | 2025-12-13 | Current | Quarterly |
| SIL_VISION_COMPLETE.md | 2025-11-29 | Stable | Core vision changes |
| SIL_MORPHOGEN_PROJECT.md | 2025-11-29 | Stable | Morphogen evolves |
| LAYER_MODELS_COMPARISON.md | 2025-12-15 | Current | New model proposed |
| MODEL_EVALUATION.md | 2025-12-15 | Current | Criteria change |
| PROVENANCE_FIRST.md | 2025-12-15 | Current | Decision made |
| INVARIANTS_OVER_LAYERS.md | 2025-12-15 | **Validated** | Agent Ether implementation |
| VALIDATION_REPORT.md | 2025-12-15 | Current | Implementation status changes |

---

## For Future Sessions

### If you're continuing architecture work:
1. Read this map first
2. Use the reading path that matches your goal
3. Check session lineage for prior context
4. Reference INVARIANTS_OVER_LAYERS.md for decision framework

### If you're adding new documents:
1. Update this map with the new document
2. Add to appropriate tier
3. Note key insight and read time
4. Update document health table

### If architectural decisions change:
1. Update MODEL_EVALUATION.md with new scores
2. Update README.md with decision status
3. Update this map if reading paths change

---

**Document Status:** Current
**Maintainer:** Architecture documentation should be updated when new synthesis sessions occur
**Session:** pulsing-horizon-1215
