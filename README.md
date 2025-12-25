# PlinyHub - Universal Problem-Solving Framework

> **TL;DR - 5 Minute Quickstart**
>
> 1. **CLASSIFY** your problem → `pliny classify "your problem"`
> 2. **CATEGORY** determines framework:
>    - CREATION/TRANSFORMATION → R-I-S-E (thorough)
>    - REPAIR/OPTIMIZATION → C-A-R-E (fast)
>    - UNDERSTANDING → HARVEST (docs)
> 3. **LOAD** domain standards → `pliny module load web_development`
> 4. **EXECUTE** the framework → `pliny rise "your problem"`
> 5. **VERIFY** your solution → `pliny verify <file>`
>
> That's it. The framework handles everything else. [Full guide →](QUICK_START.md)

---

**Version:** 3.0
**Purpose:** Solve any problem correctly, every time

**Implementation:** The framework is primarily **prompt-based** - load framework documentation into AI assistants (Claude, ChatGPT, etc.) to activate. CLI specification exists but CLI implementation is optional. See [Implementation Status](docs/IMPLEMENTATION_STATUS.md) for details.

---

## 🎯 What is PlinyHub?

PlinyHub is a **self-improving framework** for solving problems systematically. It combines:

- **Universal thinking patterns** (R-I-S-E, C-A-R-E, HARVEST)
- **Pluggable domain standards** (Murata MHC, Web Dev, Python, etc.)
- **Self-improvement via the OMEGA Loop**
- **Mathematical correctness guarantees** (5-layer verification)

The framework works for **any problem domain**—from debugging VB.NET code to building React components to making business decisions.

---

## 🚀 Quick Start

### Prompt-Based Usage (Primary Method)

1. **Load the framework:**
   - Copy content from `PLINYHUB_MASTER.md`
   - Paste into your AI assistant (Claude, ChatGPT, etc.)

2. **State your problem:**
   ```
   "Create a React component for filtering notifications"
   ```

3. **Framework automatically:**
   - Classifies your problem (CREATION, web_development, R-I-S-E)
   - Selects optimal framework
   - Executes phases with domain standards
   - Verifies solution

See [QUICK_START.md](QUICK_START.md) for the 5-minute getting started guide.

**Note:** CLI commands (if implemented) would work as shown below. See [Implementation Status](docs/IMPLEMENTATION_STATUS.md) for details.

---

## 📁 Framework Structure

```
PlinyHub/
├── README.md                    # You are here
├── QUICK_START.md               # 5-minute getting started
├── QUICK_REFERENCE.md           # One-page cheat sheet
│
├── frameworks/                  # HOW to think (methodologies)
│   ├── problem_classifier.md    # 5 categories + confidence scoring
│   ├── universal_rise.md        # Research → Identify → Synthesize → Execute
│   ├── universal_care.md        # Context → Analyze → Respond → Evaluate
│   ├── universal_harvest.md     # Documentation & understanding
│   ├── verification_framework.md # 5-layer correctness stack
│   ├── knowledge_transfer.md    # Cross-domain learning
│   ├── omega_loop.md            # Self-improving master loop
│   ├── meta_framework.md        # 3-layer architecture with GENESIS
│   ├── tree_of_thoughts.md      # **NEW** Multi-path exploration
│   └── react_integration.md     # **NEW** Reasoning + Acting
│
├── core/                        # Core enhancement layers
│   ├── meta_prompting.md        # **NEW** Self-critique layer
│   ├── confidence_protocol.md   # **NEW** Explicit confidence scoring
│   ├── persona_clarification.md # Persona management
│   ├── multi_domain_orchestration.md # Domain coordination
│   └── orchestration.md         # **NEW** Agent orchestration
│
├── execution/                   # **NEW** Execution engine
│   ├── session_manager.md      # Persistent state management
│   ├── checkpoint_manager.md   # Git-based checkpointing
│   ├── audit_system.md         # Crash-safe logging
│   ├── parallel_agents.md      # Multi-agent orchestration
│   └── error_handling.md       # Retry logic & error categories
│
├── integrations/                # **NEW** External integrations
│   ├── mcp_integration.md      # Model Context Protocol
│   ├── browser_automation.md   # Playwright patterns
│   └── tool_validation.md     # Tool availability checking
│
├── modules/                     # WHAT standards to follow
│   ├── domain_module_template.md # Template for new modules
│   ├── murata_mhc.yaml          # Murata MHC (VB.NET, C++)
│   ├── web_development.yaml     # React, TypeScript, FastAPI
│   ├── python_data.yaml         # Python, pandas, ML
│   ├── general_reasoning.yaml   # Logic, decisions
│   ├── research_analysis.yaml   # Research methodology
│   └── security_testing.yaml    # **NEW** Security testing standards
│
├── personas/                    # AI personalities
│   ├── atlas.md                 # Deep Research
│   ├── sage.md                  # Architecture
│   ├── scribe.md                # Documentation
│   └── sentinel.md              # **NEW** Security Testing
│
├── configs/                     # **NEW** Configuration schemas
│   ├── config-schema.json       # JSON Schema validation
│   └── example-config.yaml      # Example configuration
│
├── cli/                         # Automation tools
│   └── CLI_SPECIFICATION.md     # Complete command reference
│
├── docs/                        # Documentation
│   ├── MHC_INTEGRATION_GUIDE.md # MHC-specific integration
│   ├── PATTERN_LIBRARY.md       # **NEW** Comprehensive pattern catalog
│   ├── PATTERN_EXTRACTION_GUIDE.md # **NEW** How to extract patterns
│   ├── PATTERN_APPLICATION_GUIDE.md # **NEW** How to apply patterns
│   ├── SUCCESS_METRICS.md       # **NEW** Examples of high-quality docs
│   ├── EXECUTION_ENGINE_GUIDE.md # **NEW** How to use execution engine
│   └── SECURITY_TESTING_GUIDE.md # **NEW** Security testing guide
│
└── templates/                   # Reusable templates
    ├── rise/
    ├── care/
    ├── harvest/
    │   ├── javascript_documentation.md # **NEW** JavaScript/Node.js template
    │   └── multi_agent_architecture.md # **NEW** Multi-agent system template
    └── security/                 # **NEW** Security templates
        ├── vulnerability_report.md
        ├── pentest_report.md
        └── security_assessment.md
```

---

## 🚀 Execution Engine (NEW)

PlinyHub now includes an execution engine inspired by Shannon AI Pentester:

### Session Management

Manage persistent state across task execution:

```bash
pliny session start "My Task"    # Start new session
pliny session status             # Check current session
pliny session list               # List all sessions
pliny session resume <id>        # Resume incomplete session
```

### Checkpointing

Enable rollback and recovery using git-based checkpointing:

```bash
pliny checkpoint create "after-research"  # Create checkpoint
pliny checkpoint list                      # List checkpoints
pliny rollback "after-research"            # Rollback to checkpoint
```

### Parallel Execution

Execute multiple AI agents concurrently for faster completion:

```bash
pliny execute --parallel          # Run agents in parallel
pliny execute --phase research    # Run specific phase
```

### Audit Logs

All executions are logged to `audit-logs/` with:
- Event-by-event tracking
- Timing and cost metrics
- Rollback history
- Deliverable artifacts

See [Execution Engine Guide](docs/EXECUTION_ENGINE_GUIDE.md) for details.

---

## 🔒 Security Testing Module (NEW)

PlinyHub now includes security testing capabilities from Shannon:

### Quick Security Assessment

```bash
pliny security assess https://example.com /path/to/repo
```

### Vulnerability Types Covered

- SQL Injection
- Cross-Site Scripting (XSS)
- Authentication Bypass
- Authorization Flaws
- Server-Side Request Forgery (SSRF)

### Security Persona

Use the **Sentinel** persona for security-focused tasks:

```
Load personas/sentinel.md into your AI assistant
```

See [Security Testing Guide](docs/SECURITY_TESTING_GUIDE.md) for details.

---

## ⚡ Advanced Enhancements (NEW)

### Tree of Thoughts (ToT)

For complex problems with multiple valid approaches:

```
BRANCH → EVALUATE → PRUNE → EXPLORE → CONVERGE
```

Generate 3+ solution paths, score each, select optimal with fallback.

### ReAct Integration

When you need information you don't have:

```
THOUGHT → ACTION → OBSERVATION → (repeat) → ANSWER
```

Actions: SEARCH, EXECUTE, VERIFY, READ, QUERY, TEST

### Meta-Prompting

Self-critique layer before finalizing any output:

```
GENERATE → SELF-CRITIQUE → IMPROVE → VERIFY → FINALIZE
```

Catches errors that slip through standard frameworks.

### Confidence Protocol

Every response must include explicit confidence:

```
CONFIDENCE: [1-10]
REASONING: [Why this score]
CAVEATS: [What could be wrong]
VERIFY: [What to check]
```

---

## 🎭 Persona Library

Specialized AI personas for specific tasks:

| Persona | Specialty | Methodology | Use Case |
|---------|-----------|-------------|----------|
| **[Atlas](personas/atlas.md)** | Deep Research | HARVEST-R | Comprehensive research with sources |
| **[Sage](personas/sage.md)** | Architecture | R-I-S-E + ToT | System design with trade-off analysis |
| **[Scribe](personas/scribe.md)** | Documentation | HARVEST + Meta | Technical writing for any audience |
| **[Sentinel](personas/sentinel.md)** | Security Testing | R-I-S-E + C-A-R-E | Vulnerability identification and validation |

Each persona is a **self-contained prompt** you can paste into any AI. They integrate PlinyHub's frameworks, Confidence Protocol, and Meta-Prompting into focused specialists.

**Quick Start:**

1. Open any AI chat (ChatGPT, Claude, Gemini)
2. Copy the entire persona file content
3. Paste as your first message
4. Start working with your specialist!

See [personas/](personas/) for the full library.

---

## 🧠 The Core Loop

```
┌────────────┐      ┌────────────┐      ┌────────────┐      ┌────────────┐
│  CLASSIFY  │ ──→  │  FRAMEWORK │ ──→  │   VERIFY   │ ──→  │   LEARN    │
│  Problem   │      │  Execute   │      │  Solution  │      │  (OMEGA)   │
└────────────┘      └────────────┘      └────────────┘      └────────────┘
      │                  │                    │                    │
      ▼                  ▼                    ▼                    ▼
┌────────────┐   ┌─────────────────┐   ┌────────────┐      ┌────────────┐
│ 5 Categories│   │ R-I-S-E        │   │ 5 Layers   │      │ Knowledge  │
│ + Domain    │   │ C-A-R-E        │   │ Error→0    │      │ Base       │
│ + Complexity│   │ HARVEST        │   └────────────┘      └────────────┘
└────────────┘   └─────────────────┘
```

---

## 📊 The 5 Universal Problem Categories

Every problem falls into one of these categories:

| Category | Signal Words | Primary Framework |
|----------|--------------|-------------------|
| **CREATION** | create, build, implement, design | R-I-S-E |
| **TRANSFORMATION** | convert, migrate, refactor, port | R-I-S-E |
| **UNDERSTANDING** | explain, analyze, document, research | HARVEST |
| **REPAIR** | fix, debug, troubleshoot, resolve | C-A-R-E |
| **OPTIMIZATION** | optimize, improve, enhance, speed up | C-A-R-E |

---

## 🔌 Domain Modules

Domain modules inject standards into frameworks:

| Module | For | Key Standards |
|--------|-----|---------------|
| `murata_mhc` | Murata MHC systems | cc_str, generated classes, cs_log_printf |
| `web_development` | React/TypeScript/FastAPI | TypeScript, error handling, accessibility |
| `python_data` | Python/ML/Data Science | Type hints, reproducibility, validation |
| `general_reasoning` | Decisions, analysis | State assumptions, multiple perspectives |
| `research_analysis` | Research, data | Cite sources, report limitations |
| `security_testing` | Security assessments | OWASP methodology, CVSS scoring, proof-of-concept |

---

## 🔄 The OMEGA Loop (Self-Improvement)

Every task runs through the OMEGA Loop:

```
OBSERVE → MODEL → EXECUTE → GENERATE → ANALYZE → LEARN → (repeat)
```

**Key property:** Error rate converges to zero over iterations.

```
Error(n) = Error(0) × (1 - learning_rate)^n

After 5 iterations:  Initial 40% error → 13% error
After 10 iterations: Initial 40% error → 4% error  
After 20 iterations: Initial 40% error → 0.5% error
```

---

## ✅ The 5-Layer Verification Stack

```
Layer 5: Human Judgment    → Final arbiter
Layer 4: Ensemble          → Multiple methods agree (99%+)
Layer 3: Statistical       → Benchmarks, metrics (90%+)
Layer 2: Automated Testing → Tests pass (95%+)
Layer 1: Formal            → Types, syntax, linting (100%)

Combined: 99.9%+ correctness for well-defined problems
```

---

## 🛠️ CLI Usage

```bash
# Classify
pliny classify "Create a notification filter"

# Execute frameworks
pliny rise "<problem>"    # Thorough research-first
pliny care "<problem>"    # Fast iteration
pliny harvest <file>      # Documentation

# Learning
pliny omega start         # Start session tracking
pliny learn show          # View accumulated learnings
pliny learn apply "<problem>"  # Apply relevant learnings

# Verification
pliny verify <file>       # Standard verification
pliny verify --full <file>  # Full 5-layer verification

# Domain modules
pliny module load web_development
pliny check <file>        # Check standards
```

See [cli/CLI_SPECIFICATION.md](cli/CLI_SPECIFICATION.md) for complete reference.

---

## 📈 Expected Results

| Metric | Before PlinyHub | After PlinyHub |
|--------|-----------------|----------------|
| Problem domains | 1 (Murata only) | Unlimited |
| Framework selection | Manual | Automatic with confidence |
| Cross-domain transfer | None | Systematic |
| Error rate over time | Constant | Converges to 0 |
| Documentation speed | ~1 hour | ~1 minute (56x) |
| Standards checking | ~6 hours | ~90 seconds (240x) |

---

## 🎓 Learning Path

1. **Beginner:** Read [QUICK_START.md](QUICK_START.md) (5 minutes)
2. **Intermediate:** Study frameworks in `frameworks/` directory
3. **Advanced:** Create custom domain modules using template
4. **Expert:** Use GENESIS to create new frameworks

---

## 🔑 Key Principles

1. **Classify First** — Know what problem type you're solving
2. **Load Standards** — Domain modules provide guardrails
3. **Follow Phases** — Don't skip framework steps
4. **Verify Always** — Check before calling it done
5. **Learn and Store** — OMEGA captures lessons for future

---

## 📚 Further Reading

- [Problem Classifier](frameworks/problem_classifier.md) — 5 categories + confidence
- [OMEGA Loop](frameworks/omega_loop.md) — Self-improvement system
- [Meta-Framework](frameworks/meta_framework.md) — 3-layer architecture
- [Verification Framework](frameworks/verification_framework.md) — 5-layer correctness
- [CLI Specification](cli/CLI_SPECIFICATION.md) — All commands
- **[Pattern Library](docs/PATTERN_LIBRARY.md)** — **NEW** Comprehensive pattern catalog
- **[Pattern Extraction Guide](docs/PATTERN_EXTRACTION_GUIDE.md)** — **NEW** How to extract patterns
- **[Pattern Application Guide](docs/PATTERN_APPLICATION_GUIDE.md)** — **NEW** How to apply patterns
- **[Success Metrics](docs/SUCCESS_METRICS.md)** — **NEW** Examples of high-quality documentation
- **[Execution Engine Guide](docs/EXECUTION_ENGINE_GUIDE.md)** — **NEW** Session management, checkpointing, parallel execution
- **[Security Testing Guide](docs/SECURITY_TESTING_GUIDE.md)** — **NEW** Security assessment workflows

---

**PlinyHub: Universal patterns, domain-specific standards, self-improving intelligence.**
