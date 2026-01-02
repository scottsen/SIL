---
beth_topics:
  - configuration
  - semantic-contracts
  - progressive-disclosure
  - reveal
  - tool-behavior-contracts
  - architecture-validation
related_docs:
  - PROGRESSIVE_DISCLOSURE_GUIDE.md
  - ../AGENT_HELP_STANDARD.md
  - ../../foundations/architectural-principles.md
  - ../../LAYER3_SUBLAYER_ARCHITECTURE.md
status: published
date: 2025-12-22
---

# Configuration as Semantic Contract

**Abstract:** Configuration files traditionally serve as "settings" or "tuning knobs" for software tools. This document argues for a more fundamental role: **configuration as executable documentation of project semantics**. We examine how Reveal's `.reveal.yaml` specification demonstrates this pattern, connecting to SIL's principles of explicit meaning, progressive disclosure, and tool behavior contracts.

---

## 1. The Problem with Traditional Configuration

### 1.1 Configuration Drift

Teams often declare architectural intentions ("we follow clean architecture") without enforcement mechanisms. Over time:

- **Intent lives in documentation** (e.g., "routes shouldn't call repositories directly")
- **Reality lives in code** (but a developer adds `from repositories import UserRepo` to save time)
- **No automated check** catches the violation
- **Drift accumulates** until architecture is unrecognizable

**Result:** Architecture documentation becomes archaeological artifact rather than living contract.

### 1.2 Binary Configuration Choices

Most tools force binary decisions:

**Option A: Zero Configuration** ("Convention over configuration")
- ✅ Simple to start
- ❌ No project-specific customization
- ❌ Generic rules don't match team reality
- Example: ESLint's default rules may not match your architecture

**Option B: Configuration Everything** ("Explicit over implicit")
- ✅ Full control
- ❌ Configuration complexity rivals codebase
- ❌ Barrier to entry (new devs overwhelmed)
- Example: Webpack configs that need configs

**The gap:** No middle path that **scales complexity with project needs**.

### 1.3 Configuration as Settings (Not Semantics)

Traditional configuration treats settings as **opaque values**:

```yaml
# Traditional approach
max_line_length: 120
complexity_threshold: 10
```

These are **tuning parameters**, not **semantic declarations**. They answer "how much?" but not "what does this mean for our system?"

---

## 2. Configuration as Semantic Contract

### 2.1 Core Insight

**Configuration should declare project semantics, not just tune behavior.**

Instead of:
```yaml
ignore_patterns: ["**/tests/**"]  # What does this mean?
```

We declare:
```yaml
ast:
  entry_points:
    - pattern: "def test_"
      description: "Pytest test functions"
      languages: [python]
```

**Difference:**
- Traditional: "Ignore this path" (mechanism)
- Semantic: "These functions are entry points invoked by pytest" (meaning)

### 2.2 Executable Documentation

Configuration becomes **executable documentation** when:

1. **It declares intent** (not just parameters)
2. **Tools enforce it** (violations detected automatically)
3. **It's version-controlled** (evolves with codebase)
4. **It's team-shared** (everyone sees same rules)

**Example from Reveal:**
```yaml
architecture:
  layers:
    - name: routes
      path: app/routes/**
      description: "HTTP route handlers"
      cannot_import:
        - repositories/**      # Routes must go through services

    - name: services
      path: app/services/**
      description: "Business logic layer"
      cannot_import:
        - routes/**
```

This configuration **IS the architecture**. The tool enforces what the team means by "layered architecture."

### 2.3 Connection to SIL Principle #2: Meaning Must Be Explicit

From [architectural-principles.md](/foundations/architectural-principles):

> **Principle #2: Meaning Must Be Explicit**
> Semantic infrastructure makes meaning first-class. All meaningful objects are typed, inspectable semantic structures—not implicit conventions or documentation promises.

**How configuration embodies this:**
- **Layer boundaries** are explicit typed structures (not implicit conventions)
- **Entry points** are declared patterns (not "developers should know")
- **Custom semantics** are named patterns (not "search the code for Stripe calls")

Traditional configuration: "Here are some settings"
Semantic configuration: "Here is what these structures mean in our system"

---

## 3. Reveal's YAML Specification: Case Study

### 3.1 Progressive Configuration Pattern

Reveal demonstrates **progressive configuration** matching the three-level progressive disclosure pattern:

**Level 1: Zero Config (Intelligent Defaults)**
```bash
reveal app.py                    # Works immediately
reveal app.py --check            # Quality checks with sensible rules
```

**Level 2: Project Overrides (`.reveal.yaml`)**
```yaml
# .reveal.yaml - Project-specific semantics
imports:
  ignore_unused:
    - "**/tests/fixtures/**"     # Fixtures import without direct usage

architecture:
  layers:
    - name: routes
      cannot_import: [repositories/**]
```

**Level 3: Custom Extensions (`~/.reveal/rules/`)**
```python
# ~/.reveal/rules/stripe_usage.py
# Team-specific custom rule for tracking payment code
```

**Key insight:** Complexity cost is opt-in. Teams **pay for what they need**.

### 3.2 URI Schemes + Custom Patterns = Composable Semantics

Reveal's URI adapter system (`reveal python://`, `reveal ast://`) combines with configuration to enable **queryable domain knowledge**:

```yaml
semantic:
  custom_patterns:
    - name: uses_stripe_api
      description: "Functions that call Stripe API"
      patterns:
        - "stripe\\..*\\("
```

**Now queryable:**
```bash
reveal 'semantic://app?uses_stripe_api'
```

**Result:** Domain-specific knowledge (e.g., "what code touches our payment provider?") becomes **first-class queryable semantic**—not tribal knowledge or manual grep.

**Connection to SIL:** This mirrors how USIR (Universal Semantic IR) enables cross-domain queries. Configuration extends the semantic vocabulary for project-specific domains.

### 3.3 Entry Points as First-Class Concept

Modern frameworks use **implicit invocation** (decorators, dependency injection, event handlers). Dead code detection fails because tools don't understand "framework magic."

**Reveal's solution:**
```yaml
ast:
  entry_points:
    - pattern: "@app\\.(route|get|post)"
      description: "FastHTML route handlers"
      languages: [python]

    - pattern: "@click\\.command"
      description: "Click CLI commands"
      languages: [python]
```

**Benefit:** Teaches tools about framework invocation patterns. What was "magic" becomes **declared semantic contract**.

**Generalization:** Any implicit invocation pattern can be declared:
- Event handlers (`addEventListener`, React hooks)
- Dependency injection (`@Injectable`, Spring beans)
- Plugin systems (Jupyter kernels, VSCode extensions)

### 3.4 Team-Shareable Architectural Rules

```yaml
architecture:
  rules:
    - name: no-god-functions
      check: function_lines <= 100
      severity: error
      message: "Functions should be under 100 lines for maintainability"

    - name: models-import-restrictions
      pattern: "app/models/**/*.py"
      check: "only imports from [typing, pydantic, datetime, enum]"
      severity: error
      message: "Models should have no business logic dependencies"
```

**Distinction from ESLint/Pylint:**
- **Global rules:** Apply same rules everywhere
- **Semantic rules:** Different rules for different architectural layers

**Example:** Services can import repositories, but routes cannot. This is **architecture-aware**.

---

## 4. Theoretical Foundations

### 4.1 Configuration as Tool Behavior Contract (TBC)

From [LAYER3_SUBLAYER_ARCHITECTURE.md](/docs/LAYER3_SUBLAYER_ARCHITECTURE.md), every tool should answer:

1. **How does it execute?** (mode: sync/async/job/session)
2. **What channels does it use?** (stdin, stdout, stderr, events)
3. **How do you track progress?**
4. **What permissions does it need?**
5. **How do I invoke and monitor you?**

**Configuration extends this:**

The `.reveal.yaml` file documents how Reveal should **behave for this project**:

```yaml
# Execution mode: How should unused imports be detected?
imports:
  ignore_unused: [...]           # Context-specific execution rules

# Permissions: What can different layers access?
architecture:
  layers:
    - name: routes
      cannot_import: [...]       # Permission boundaries
```

**Key insight:** Configuration is **metadata about tool behavior** in project context.

### 4.2 Invariants Over Layers

From [architectural-principles.md](/foundations/architectural-principles):

> **Principle #4: Invariants Define Correctness**
> Correctness in semantic infrastructure comes from preserved invariants, not intuition or guidelines.

**How configuration encodes invariants:**

```yaml
architecture:
  layers:
    - name: models
      path: app/models/**
      can_import: [typing, pydantic, datetime, enum]
      cannot_import: ["**/!(typing|pydantic|datetime|enum)"]
```

**This declares an invariant:** "Models have no business logic dependencies"

**Verification:** Tool checks imports → violations break the build → invariant enforced

**Traditional approach:** Write this in documentation, hope developers remember, catch in code review (maybe).

**Semantic approach:** Declare the invariant, automate verification, make violation impossible to merge.

### 4.3 Multi-Agent Protocol Principles

From [MULTI_AGENT_PROTOCOL_PRINCIPLES.md](/research/agent-infrastructure/MULTI_AGENT_PROTOCOL_PRINCIPLES.md):

> **Principle 2: All communication must be typed**
> Input/output schemas prevent silent failures

**How configuration supports this:**

```yaml
semantic:
  custom_patterns:
    - name: uses_email
      description: "Functions that send email"
      languages: [python]
      patterns: ["send.*email", "EmailMessage"]
```

**Result:** Agents can query "what functions send email?" with typed responses. The configuration **types the project's semantic domain**.

---

## 5. Broader Implications

### 5.1 Pattern Applies Beyond Code Analysis

The "configuration as semantic contract" pattern generalizes:

**Documentation Structure:**
```yaml
# docs.yaml
structure:
  - section: foundations
    audience: [newcomers, researchers]
    reading_time: 30min
    dependencies: []

  - section: systems
    audience: [developers]
    reading_time: 2hr
    dependencies: [foundations]
```

**API Contracts:**
```yaml
# api.yaml
endpoints:
  - path: /api/users
    rate_limit: 1000/hour
    auth_required: true
    data_sensitivity: PII
    cannot_call: [/api/admin/**]    # Security boundary
```

**Deployment Rules:**
```yaml
# deployment.yaml
environments:
  - name: production
    branch: main
    auto_deploy: false              # Invariant: prod requires approval
    required_checks: [tests, security_scan, architecture_validation]
```

**Common pattern:** Declare semantic constraints, enforce automatically, version-control the contract.

### 5.2 Configuration as Team Alignment Mechanism

Traditional alignment:
- Write architecture docs
- Explain in meetings
- Hope everyone remembers
- Catch drift in code reviews

**Semantic configuration alignment:**
- Declare architecture in `.reveal.yaml`
- Commit to version control
- Tool enforces on every commit
- Violations fail CI immediately

**Result:** Architecture **cannot drift silently**. The configuration is **living documentation**.

### 5.3 Enabling Progressive Complexity

**The problem with "zero config" tools:**
- Great for simple projects
- Break down as complexity scales
- Force users to eject entirely (React's `eject` pattern)

**The problem with "configure everything" tools:**
- Overwhelming for simple projects
- Barrier to entry too high
- Configuration becomes second codebase

**Progressive configuration solves this:**
- Start with intelligent defaults
- Add project overrides as needed
- Extend with custom rules when domain-specific
- **Complexity scales with actual project needs**

---

## 6. Connection to SIL Research Themes

### 6.1 Progressive Disclosure (Theme: Information Architecture)

Configuration follows three-level progressive disclosure:

**Level 1:** Tool works with zero config (intelligent defaults)
**Level 2:** Project declares overrides (`.reveal.yaml`)
**Level 3:** Team extends with custom semantics (`~/.reveal/rules/`)

See: [PROGRESSIVE_DISCLOSURE_GUIDE.md](PROGRESSIVE_DISCLOSURE_GUIDE.md)

### 6.2 Agent-Help Standard (Theme: Agent Infrastructure)

Configuration becomes **machine-readable tool contract**:

```bash
reveal --agent-help                    # General usage
reveal help://architecture             # How to use architecture validation
```

The configuration **documents project-specific semantics** that agents can query.

See: [AGENT_HELP_STANDARD.md](../AGENT_HELP_STANDARD.md)

### 6.3 Tool Behavior Contracts (Theme: Agent Infrastructure)

Configuration answers the TBC questions for project context:

- How does this tool behave **for this project**?
- What are the **project-specific rules**?
- What **semantic patterns** exist in this codebase?

See: [LAYER3_SUBLAYER_ARCHITECTURE.md](../../LAYER3_SUBLAYER_ARCHITECTURE.md)

### 6.4 Structure Before Heuristics (Theme: Architectural Principles)

**Traditional linters:** Heuristics for "code smells"
**Semantic configuration:** Explicit structural rules

```yaml
# Not: "Complexity seems high" (heuristic)
# Instead: "Functions in services/ must be under 100 lines" (structure)
architecture:
  rules:
    - pattern: "app/services/**"
      check: function_lines <= 100
```

See: [architectural-principles.md](../../foundations/architectural-principles.md)

---

## 7. Future Research Directions

### 7.1 Configuration as Trust Assertion

Could configuration declare **capability requirements**?

```yaml
# Hypothetical: Trust Assertion Protocol integration
trust:
  capabilities:
    - name: network_access
      required_for: [semantic://app?makes_http_call]
      justification: "External API calls for data enrichment"
```

**Vision:** Configuration declares what capabilities code needs, TAP verifies at runtime.

See: [TRUST_ASSERTION_PROTOCOL.md](../standards/TRUST_ASSERTION_PROTOCOL.md)

### 7.2 Multi-Agent Configuration Contracts

Could teams declare **agent behavior contracts** in configuration?

```yaml
# Hypothetical: Agent Ether integration
agents:
  code_reviewer:
    can_read: [src/**, tests/**]
    can_write: [tests/**]
    cannot_write: [src/**]              # Read-only for source
    required_approval: [human]          # Must get human approval

  test_generator:
    can_read: [src/**]
    can_write: [tests/**]
    auto_commit: true                   # Can commit directly
```

**Vision:** Configuration as **multi-agent protocol contract** (not just single-tool settings).

### 7.3 Cross-Project Semantic Standards

Could projects declare **semantic compatibility**?

```yaml
# Hypothetical: USIR compatibility declaration
semantics:
  compatible_with:
    - usir: v1.0
    - domain: code-understanding
  exports:
    - type: ArchitectureGraph
      version: 1.0
      schema: ./schemas/architecture.yaml
```

**Vision:** Projects declare semantic exports, other tools can depend on them.

---

## 8. Practical Guidelines

### 8.1 When to Use Semantic Configuration

**Use semantic configuration when:**

✅ **Team alignment matters** (architecture rules, conventions)
✅ **Domain knowledge is valuable** (custom patterns, project-specific semantics)
✅ **Enforcement prevents drift** (layer boundaries, invariants)
✅ **Configuration is shared** (version-controlled, team-wide)

**Don't use semantic configuration for:**

❌ **Personal preferences** (tabs vs spaces, editor settings)
❌ **Purely aesthetic rules** (no semantic meaning)
❌ **Rules that can't be verified** (vague guidelines)

### 8.2 Design Principles for Semantic Config

**1. Declare meaning, not mechanism**
```yaml
# ❌ Mechanism-focused
ignore_paths: ["tests/"]

# ✅ Meaning-focused
ast:
  entry_points:
    - pattern: "def test_"
      description: "Test functions invoked by pytest"
```

**2. Make contracts explicit**
```yaml
# ❌ Implicit
max_imports: 10

# ✅ Explicit contract
architecture:
  rules:
    - name: minimize-coupling
      check: import_count <= 10
      message: "High import count suggests tight coupling"
```

**3. Enable progressive adoption**
- Level 1: Zero config (intelligent defaults)
- Level 2: Project overrides (common needs)
- Level 3: Custom extensions (domain-specific)

**4. Version control and share**
- Commit `.reveal.yaml` to repository
- Document why rules exist (not just what they check)
- Review config changes like code changes

---

## 9. Conclusion

**Configuration as semantic contract** transforms configuration from "settings file" to "executable documentation of project semantics."

**Key insights:**

1. **Configuration should declare meaning** (not just tune parameters)
2. **Tools should enforce contracts** (violations detected automatically)
3. **Progressive complexity** (opt-in, scales with project needs)
4. **Team alignment** (shared, version-controlled, living documentation)

**Reveal's `.reveal.yaml` specification demonstrates:**
- Progressive disclosure applied to configuration
- URI schemes + custom patterns = composable semantics
- Entry points as first-class framework integration concept
- Architecture-aware rules (not just global linting)

**Connection to SIL:**
- Embodies Principle #2 (Meaning Must Be Explicit)
- Extends Tool Behavior Contracts to project context
- Demonstrates Structure Before Heuristics
- Supports Agent-Help Standard with machine-readable contracts

**Future potential:**
- Integration with Trust Assertion Protocol (capability declarations)
- Multi-agent configuration contracts (Agent Ether)
- Cross-project semantic compatibility (USIR exports)

**Bottom line:** When configuration declares project semantics rather than just tuning behavior, it becomes **infrastructure for maintaining architectural integrity**—exactly the kind of semantic infrastructure SIL builds.

---

## 10. References

**SIL Documents:**
- [Architectural Principles](/foundations/architectural-principles.md) - Structure Before Heuristics, Meaning Must Be Explicit
- [Progressive Disclosure Guide](PROGRESSIVE_DISCLOSURE_GUIDE.md) - Three-level pattern
- [Agent-Help Standard](../AGENT_HELP_STANDARD.md) - Machine-readable tool contracts
- [Layer 3 Architecture](../../LAYER3_SUBLAYER_ARCHITECTURE.md) - Tool Behavior Contracts
- [Multi-Agent Protocol Principles](../agent-infrastructure/MULTI_AGENT_PROTOCOL_PRINCIPLES.md) - Typed communication

**External References:**
- Reveal YAML Config Spec: `/home/scottsen/src/projects/reveal/internal-docs/planning/REVEAL_YAML_CONFIG_SPEC.md`
- Reveal v0.24.0+: Production implementation of pattern detection system
- Reveal v0.17.0+: URI adapter registry and progressive discovery

**Related Research:**
- Configuration as code (infrastructure as code patterns)
- Design by contract (Bertrand Meyer)
- Type-driven development (dependent types, refinement types)
- Architecture decision records (ADRs)

---

**Status:** Published
**Date:** 2025-12-22
**Version:** 1.0
**Author:** Semantic Infrastructure Lab
**Maintainer:** SIL Research Team
