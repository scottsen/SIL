# Layer 3 Sub-Layer Architecture (Agent Ether)

**Created:** 2025-12-12
**Session:** peaceful-rainbow-1212 (extracted from nasezivu-1211 synthesis)
**Status:** Architectural Proposal
**Context:** NATS implementation revealing need for Layer 3 structure

---

## Executive Summary

**Problem**: Layer 3 (Agent Ether) in the SIL Semantic OS conflates three distinct concerns:
1. How agents physically communicate (infrastructure)
2. How agents invoke tools (contracts)
3. How agents coordinate with each other (protocols)

**Solution**: Structure Layer 3 as **three sub-layers** (3a, 3b, 3c), each with clear responsibilities.

**Status**:
- **Layer 3a**: 70% implemented (TIA local), NATS adds distributed tier
- **Layer 3b**: Specified, not implemented
- **Layer 3c**: Principles documented, implementation pending

---

## The Three Sub-Layers

### Layer 3c: Protocol Layer (Agent ↔ Agent)

**Purpose**: Enable safe, predictable agent-to-agent coordination

**Core Components**:

#### 1. Multi-Agent Protocol Principles (7 Principles)
1. **Communicate intent, not instructions** - Purpose, constraints, success criteria
2. **All communication must be typed** - Input/output schemas, error schemas, provenance metadata
3. **Roles must be explicit** - RACI framework (Responsible, Accountable, Consulted, Informed)
4. **Autonomy must be bounded** - Decision limits, escalation conditions, resource budgets
5. **Uncertainty does not permit creativity** - Stop → Escalate → Ask (don't improvise)
6. **Provenance is the substrate of trust** - Track what was seen, believed, relied upon, generated
7. **Parallelism requires synthesis** - Deterministic merge of multi-agent outputs

**Reference**: SIL Canonical - `MULTI_AGENT_PROTOCOL_PRINCIPLES.md`

#### 2. Message Schemas
- **Intent envelopes** - What the agent wants to achieve
- **Context propagation** - Preserve purpose across delegation chain
- **Result schemas** - Typed outputs with confidence/provenance
- **Error schemas** - Structured failure reporting

#### 3. Coordination Primitives
- **Delegation** - Agent A asks Agent B to perform task
- **Negotiation** - Agents agree on terms before execution
- **Composition** - Agent orchestrates multiple sub-agents
- **Escalation** - Agent requests human/superior intervention
- **Synthesis** - Merge results from parallel agents

#### 4. RACI Role System
- **Responsible** - Which agent does the work
- **Accountable** - Which agent is ultimately answerable
- **Consulted** - Which agents provide input
- **Informed** - Which agents receive results

**Implementation Status**: ❌ Principles documented (2025-12-03), implementation pending (Q1 2026)

**TIA Mapping**: Would use NATS messagebus (Layer 3a) as transport

---

### Layer 3b: Tool Behavior Contracts (Agent ↔ Tool)

**Purpose**: Enable predictable, observable tool invocation

**Core Innovation**: Every tool answers 5 questions via structured metadata

#### The 5 Questions

1. **How does it execute?**
   - `mode: sync | async | job | session`
   - Sync: Request → immediate response
   - Async: Fire & monitor
   - Job: Long-running with progress
   - Session: Interactive/stateful (REPL, browser, debugger)

2. **What channels does it use?**
   - `stdin`, `stdout`, `stderr` (standard I/O)
   - `events` (structured notifications)
   - `logs` (observability)
   - `progress` (completion percentage)

3. **How do you track progress?**
   - `percent` (0-100%)
   - `steps` (n of m)
   - `indeterminate` (spinner)

4. **What permissions does it need?**
   - `filesystem-read`, `filesystem-write`
   - `network-access`
   - `secrets-access`
   - `execution-privileged`

5. **How do I invoke and monitor you?**
   - Device paths: `/dev/agent-ether/tools/{name}/...`
   - Control: `stdin`, `control`
   - Output: `stdout`, `stderr`, `events`, `logs`
   - Status: `status`, `progress`, `result`

**Reference**: `/home/scottsen/src/projects/agent-ether/README.md`

**Implementation Status**: ❌ Specification exists, not implemented in TIA

**TIA Mapping**: Would wrap TIA commands (`tia semantic search`, `tia ast scan`) with TBC metadata

---

### Layer 3a: Orchestration Substrate (Infrastructure)

**Purpose**: Physical medium through which agents discover and coordinate

**Two Tiers**:

#### Local Ether (Single-Host)
**Medium**: Named pipes, Unix IPC, virtual filesystem

**TIA Implementation** (✅ Production-Ready, 2,834 LOC):
- `/agent/` virtual filesystem
- `lib/agent/coordination.py` (631 LOC) - Task sequencing, dependencies
- `lib/agent/routing.py` (770 LOC) - Capability-based tool selection
- `lib/agent/messaging.py` (558 LOC) - Inter-agent communication
- `lib/agent/patterns.py` (875 LOC) - Workflow templates
- `lib/agents/registry.py` (~300 LOC) - Agent discovery
- `lib/agents/orchestrator.py` (~400 LOC) - Multi-agent orchestration

**Capabilities**:
- ✅ Agent registry & discovery
- ✅ Intelligent routing (capability-based)
- ✅ Orchestration patterns (sequential, parallel, hierarchical, collaborative)
- ✅ Message passing
- ✅ Execution modes (sync, async, job)
- ✅ Provenance (Sessions, Beth, Tasks, Processes)

**Limitations**:
- ❌ Single-host only (no distributed coordination)

---

#### Distributed Ether (Cross-Host)
**Medium**: NATS messagebus

**TIA Implementation** (🚧 In Progress - NATS Phase):
- **Location**: tia-proxy:4222
- **Technology**: NATS (cloud-native messaging)
- **Patterns**: Pub/sub, request/reply, work queues, streaming

**Subject Taxonomy**:
```
{agent}.{category}.{topic}.{detail}

Examples:
tia.events.session.started         # TIA publishes session lifecycle
tia.tasks.analysis.python          # TIA work queue (distribute tasks)
tia.rpc.git.status                 # TIA synchronous RPC
frono.rpc.catalog.search           # Frono catalog search
agent.presence.announce            # Agent discovery protocol
```

**Capabilities**:
- 🚧 Agent discovery across hosts
- 🚧 Cross-instance session awareness
- 🚧 Task delegation to remote agents
- 🚧 Load balancing (multiple instances)
- 🚧 Event-driven workflows
- 🚧 Horizontal scaling

**Status**: Planning complete (149 pages documentation), implementation starting

**Reference**:
- Architecture: `tia/docs/infrastructure/NATS_MESSAGEBUS_ARCHITECTURE.md`
- Deployment: `tia/docs/infrastructure/NATS_DEPLOYMENT_PLAN.md`
- Integration: `tia/docs/integrations/slack/SLACK_NATS_AGENT_INTEGRATION.md`

---

## Complete Layer 3 Architecture

```
┌──────────────────────────────────────────────────────────────┐
│ Layer 3: Agent Ether (Multi-Agent Coordination)              │
├──────────────────────────────────────────────────────────────┤
│                                                                │
│  Layer 3c: Protocol Layer (Agent ↔ Agent Communication)      │
│  ┌────────────────────────────────────────────────────────┐  │
│  │ • 7 Multi-Agent Protocol Principles                     │  │
│  │ • Typed message schemas (intent, context, results)      │  │
│  │ • RACI role definitions                                 │  │
│  │ • Escalation primitives (stop → escalate → ask)        │  │
│  │ • Synthesis patterns (merge parallel results)          │  │
│  │ • Provenance tracking (semantic trace)                 │  │
│  └────────────────────────────────────────────────────────┘  │
│                            ↕                                   │
│  Layer 3b: Tool Behavior Contracts (Agent ↔ Tool)            │
│  ┌────────────────────────────────────────────────────────┐  │
│  │ • TBC specification (5 questions every tool answers)    │  │
│  │ • Execution modes (sync, async, job, session)           │  │
│  │ • Channel contracts (stdin, stdout, events, logs)       │  │
│  │ • Progress models (percent, steps, indeterminate)       │  │
│  │ • Security declarations (permissions, audit, limits)    │  │
│  │ • Device filesystem (/dev/agent-ether/tools/...)       │  │
│  └────────────────────────────────────────────────────────┘  │
│                            ↕                                   │
│  Layer 3a: Orchestration Substrate (Infrastructure)          │
│  ┌────────────────────────────────────────────────────────┐  │
│  │ LOCAL (single-host):                                    │  │
│  │ • /agent/ filesystem, pipes, Unix IPC                   │  │
│  │ • lib/agent/* (coordination, routing, messaging)        │  │
│  │ • lib/agents/* (registry, orchestrator)                 │  │
│  │ • Status: ✅ Production (TIA has this)                  │  │
│  │                                                          │  │
│  │ DISTRIBUTED (cross-host):                               │  │
│  │ • NATS messagebus (pub/sub, req/reply, work queues)     │  │
│  │ • Subject taxonomy (tia.*, frono.*, agent.*)            │  │
│  │ • Agent discovery & presence                            │  │
│  │ • Load balancing & failover                             │  │
│  │ • Status: 🚧 In Progress (NATS phase)                   │  │
│  └────────────────────────────────────────────────────────┘  │
│                                                                │
└──────────────────────────────────────────────────────────────┘
```

---

## Why Three Sub-Layers?

### Separation of Concerns

**Different Responsibilities**:
- **3a**: "How do messages physically travel?"
- **3b**: "How do agents invoke tools safely?"
- **3c**: "How do agents coordinate with each other?"

**Different Stakeholders**:
- **3a**: Infrastructure engineers, DevOps
- **3b**: Tool developers, security architects
- **3c**: Multi-agent system designers, AI researchers

**Different Evolution Rates**:
- **3a**: Infrastructure changes (local → distributed, NATS → alternatives)
- **3b**: Tool contract evolution (add new execution modes, channels)
- **3c**: Protocol refinement (new coordination patterns, safety properties)

---

### Analogy: OSI Network Model

| OSI Model | Agent Ether | Purpose |
|-----------|-------------|---------|
| Physical | Layer 3a (substrate) | How bits move (NATS, pipes) |
| Data Link | Layer 3a (substrate) | Reliable delivery |
| Network | Layer 3a (substrate) | Routing (subject taxonomy) |
| Transport | Layer 3b (TBC) | Tool invocation contracts |
| Session | Layer 3b (TBC) | Execution modes, channels |
| Presentation | Layer 3c (protocol) | Message schemas, typing |
| Application | Layer 3c (protocol) | Coordination semantics (delegation, synthesis) |

**Key Insight**: Just as OSI separates physical transport from application semantics, Layer 3 separates orchestration substrate from coordination protocols.

---

## Implementation Roadmap

### Phase 1: Layer 3a (Distributed Substrate) — Q4 2025 / Q1 2026
**Goal**: NATS messagebus operational

**Milestones**:
1. ✅ NATS deployed on tia-proxy
2. 🚧 Python client library (`lib/messagebus.py`)
3. 🚧 Session coordination (cross-instance awareness)
4. 🚧 Slack integration (universal-bot ↔ NATS)
5. 🚧 TIA responder service
6. 🚧 Frono integration

**Reference**: `tia/docs/infrastructure/NATS_DEPLOYMENT_PLAN.md`

---

### Phase 2: Layer 3c (Protocol Layer) — Q1-Q2 2026
**Goal**: Implement 7 multi-agent principles

**Milestones**:
1. Typed message schemas (intent, context, result, error)
2. RACI role system
3. Escalation primitives (`agent.escalation.*` subjects)
4. Synthesis patterns (merge parallel agent outputs)
5. Provenance integration (emit coordination events to Layer 0)
6. Human-in-the-loop workflows (via Slack)

**Reference**: SIL Canonical - `MULTI_AGENT_PROTOCOL_PRINCIPLES.md`

---

### Phase 3: Layer 3b (Tool Behavior Contracts) — Q2-Q3 2026
**Goal**: Implement TBC specification

**Milestones**:
1. TBC metadata schema (RFC-style spec)
2. Wrap TIA commands with TBC metadata
3. TBC registry (publish tool capabilities to NATS)
4. `/dev/agent-ether/` virtual filesystem
5. Session execution mode (for REPLs, browsers)
6. Security declaration enforcement

**Reference**: `/home/scottsen/src/projects/agent-ether/README.md`

---

## Benefits of Sub-Layer Structure

### 1. **Clarity**
Each layer has clear, distinct responsibilities. No confusion about whether something is "infrastructure" or "protocol."

### 2. **Modularity**
Can replace Layer 3a substrate (NATS → alternative) without changing Layer 3c protocols.

### 3. **Progressive Implementation**
Can deploy Layer 3a (NATS) first, then Layer 3c (protocols), then Layer 3b (TBC). Each layer delivers value independently.

### 4. **Testing & Validation**
Each layer can be tested in isolation. Easier to verify correctness.

### 5. **Documentation**
Each layer gets its own specification, making architecture clearer.

---

## Relationship to Other Layers

### Layer 2 (Domain Modules)
- **Layer 2 provides**: Domain-specific capabilities (semantic search, AST analysis, Git operations)
- **Layer 3b wraps**: Domain modules with TBC metadata
- **Layer 3a routes**: Requests to appropriate domain modules
- **Layer 3c coordinates**: Multi-domain workflows

### Layer 1 (Pantheon IR)
- **Current**: Layer 3 uses JSON for messages
- **Future**: Migrate to Pantheon IR when Layer 1 matures
- **Design**: Message schemas should be Pantheon IR-compatible

### Layer 0 (Semantic Memory)
- **Layer 0 stores**: Coordination provenance (who delegated what to whom, when, why)
- **Layer 3c emits**: Coordination events to Layer 0
- **Layer 0 enables**: Audit trail, learning from coordination patterns

---

## Open Questions

### 1. Should sub-layer split be formalized in SIL architecture?
**Current**: Layer 3 is monolithic in official docs
**Proposed**: Add 3a/3b/3c to canonical architecture
**Decision**: Needs SIL architecture team review

### 2. Naming Conventions
**Current**: "Agent Ether" means everything
**Proposed**:
- **Formal**: Layer 3 (with sub-layers 3a/3b/3c)
- **Infrastructure**: "Distributed Agent Ether" or "NATS messagebus" (Layer 3a)
- **Casual**: "The Ether" when context is clear

### 3. Cross-Layer Dependencies
**Issue**: Layer 3c should use Pantheon IR (Layer 1), but Layer 1 only 30% complete
**Workaround**: Use JSON now, design for IR compatibility
**Migration**: When Layer 1 matures, migrate message schemas

### 4. Security Model
**Question**: Should each sub-layer have separate security concerns?
- **3a**: Network-level (NATS auth, TLS)
- **3b**: Tool permissions (filesystem, network, secrets)
- **3c**: Protocol-level (agent authentication, authorization)

---

## Related Documentation

### SIL Architecture
- Canonical architecture: `SIL_SEMANTIC_OS_ARCHITECTURE.md`
- Multi-agent principles: `MULTI_AGENT_PROTOCOL_PRINCIPLES.md`
- Specification gaps: `LAYER3_AGENT_ETHER_SPECIFICATION_GAPS.md`

### TIA Implementation
- Agent Ether status: `tia/projects/SIL/docs/TIA_AGENT_ETHER_IMPLEMENTATION_STATUS.md`
- NATS architecture: `tia/docs/infrastructure/NATS_MESSAGEBUS_ARCHITECTURE.md`
- NATS deployment: `tia/docs/infrastructure/NATS_DEPLOYMENT_PLAN.md`
- Agent Ether guide: `tia/docs/infrastructure/AGENT_ETHER_GUIDE.md`

### Specifications
- Tool Behavior Contracts: `/home/scottsen/src/projects/agent-ether/README.md`
- Multi-agent coordination: `/home/scottsen/src/projects/agent-ether/docs/architecture/MULTI_AGENT_COORDINATION.md`

---

## Summary

**Core Thesis**: Layer 3 (Agent Ether) should be structured as three sub-layers, each with distinct concerns.

**Layer 3a (Orchestration Substrate)**: The physical "ether" — pipes, NATS, messagebus
**Layer 3b (Tool Behavior Contracts)**: Agent → Tool predictability
**Layer 3c (Protocol Layer)**: Agent ↔ Agent coordination safety

**Current Status**:
- **3a**: 70% done (TIA local), NATS adds distributed tier (in progress)
- **3b**: Specified, not implemented
- **3c**: Principles documented, implementation pending

**Rationale**: Separation enables clarity, modularity, progressive implementation, independent evolution.

**Next Step**: Deploy Layer 3a (NATS), then implement 3c (protocols), then 3b (TBC).

---

**Document**: peaceful-rainbow-1212 (extracted from nasezivu-1211 synthesis)
**Status**: Architectural Proposal
**Last Updated**: 2025-12-12
