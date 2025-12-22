# PlinyHub Edge Case Examples

**Version:** 1.0  
**Created:** December 22, 2025  
**Purpose:** Demonstrate framework application in non-obvious scenarios

---

## Overview

These examples demonstrate framework application in non-obvious scenarios where classification or framework selection isn't straightforward.

---

## Edge Case 1: Ambiguous Category (Creation vs Transformation)

**User Request:** "Add TypeScript types to our existing JavaScript React components"

**Why It's Tricky:**
- Could be CREATION (creating new type definitions)
- Could be TRANSFORMATION (converting JS to TS)

**Correct Classification:**
```yaml
category: "TRANSFORMATION"
rationale: "We're converting existing code to a new form, not creating from scratch"
framework: "R-I-S-E"
rationale: "Migration requires research into existing patterns and planning"
```

**Key Insight:** If the core logic already exists and you're changing its form/format, it's TRANSFORMATION.

---

## Edge Case 2: Repair That Requires Research

**User Request:** "Fix the intermittent connection failures to the PLC - we've tried everything"

**Why It's Tricky:**
- Signal word "fix" suggests REPAIR → C-A-R-E
- But "tried everything" suggests root cause is unknown

**Correct Classification:**
```yaml
category: "REPAIR"
framework: "R-I-S-E"  # NOT C-A-R-E
rationale: "Root cause unclear, need research phase before attempting fixes"
```

**Key Insight:** When C-A-R-E would exceed 5 iterations or root cause is unknown, escalate to R-I-S-E.

---

## Edge Case 3: Understanding That Leads to Creation

**User Request:** "Document the move dispatcher, then add a new move type"

**Why It's Tricky:**
- Two tasks in one request
- First is UNDERSTANDING, second is CREATION

**Correct Approach:**
```yaml
task_1:
  category: "UNDERSTANDING"
  framework: "HARVEST"
  deliverable: "Move dispatcher documentation"
  
task_2:
  category: "CREATION"
  framework: "R-I-S-E"
  dependency: "task_1 must complete first"
  deliverable: "New move type implementation"
```

**Key Insight:** Split compound requests into sequential tasks. Use output of first as input to second.

---

## Edge Case 4: No Clear Domain

**User Request:** "Help me decide whether to use microservices or monolith for our new system"

**Why It's Tricky:**
- No code files to analyze
- No specific technology mentioned
- Strategic/architectural decision

**Correct Classification:**
```yaml
category: "UNDERSTANDING"  # Need to understand requirements first
domain: "general_reasoning"
framework: "R-I-S-E"
rationale: "High-stakes decision requiring multiple options evaluation"
```

**Key Insight:** Strategic decisions without clear technical domain use `general_reasoning` with R-I-S-E.

---

## Edge Case 5: Optimization That's Actually Repair

**User Request:** "Make the database queries faster - they're timing out"

**Why It's Tricky:**
- "faster" suggests OPTIMIZATION
- "timing out" suggests something is broken (REPAIR)

**Correct Classification:**
```yaml
category: "REPAIR"  # NOT OPTIMIZATION
rationale: "Timeouts indicate broken functionality, not just suboptimal performance"
framework: "C-A-R-E"
```

**Key Insight:** If the system is failing (errors, timeouts, crashes), it's REPAIR even if the user says "optimize."

---

## Edge Case 6: Multi-Step Workflow

**User Request:** "Set up CI/CD pipeline for our MHC project"

**Why It's Tricky:**
- CREATION (new pipeline)
- But involves multiple domains (DevOps, MHC, possibly web)
- Multiple sub-tasks

**Correct Approach:**
```yaml
category: "CREATION"
framework: "R-I-S-E"
primary_domain: "general_reasoning"  # DevOps isn't a defined domain
secondary_domain: "murata_mhc"  # For MHC-specific build steps

sub_tasks:
  1: "Research CI/CD options for Windows/.NET projects"
  2: "Design pipeline stages (build, test, deploy)"
  3: "Implement pipeline configuration"
  4: "Add MHC-specific build steps (z_* generation, etc.)"
  5: "Test and verify"
```

**Key Insight:** When no specific domain fits, use `general_reasoning` as primary and apply relevant domain standards where applicable.

---

## Edge Case 7: Vague Request

**User Request:** "Make this better"

**Why It's Tricky:**
- No specific category signal
- No clear domain
- Ambiguous goal

**Correct Approach:**
```yaml
category: "UNKNOWN"
confidence: 0.3  # Below threshold
action: "ASK_CLARIFYING_QUESTION"

clarifying_question: |
  "I'd be happy to help improve this. Could you clarify:
  1. What specifically isn't working well? (REPAIR)
  2. What would 'better' look like? (OPTIMIZATION)
  3. Are there new features you need? (CREATION)
  4. Do you need documentation or explanation? (UNDERSTANDING)"
```

**Key Insight:** When confidence is below 0.7, ask clarifying questions rather than guessing.

---

## Edge Case 8: Conflicting Signals

**User Request:** "Create a bug fix for the login issue"

**Why It's Tricky:**
- "Create" suggests CREATION
- "bug fix" suggests REPAIR

**Correct Classification:**
```yaml
category: "REPAIR"
rationale: "'bug fix' is the noun, 'create' is just describing the action"
framework: "C-A-R-E"
```

**Key Insight:** Focus on what the DELIVERABLE is, not the verb describing the action.

---

## Edge Case 9: Documentation vs Implementation

**User Request:** "Add error handling to the API"

**Why It's Tricky:**
- Could be CREATION (new error handling code)
- Could be UNDERSTANDING (documenting existing error handling)

**Correct Classification:**
```yaml
category: "CREATION"
rationale: "'Add' implies creating new functionality, not documenting existing"
framework: "C-A-R-E"  # If familiar with the API
# OR
framework: "R-I-S-E"  # If unfamiliar with the API
```

**Key Insight:** "Add" almost always means CREATION. For documentation, users typically say "document," "explain," or "describe."

---

## Edge Case 10: Multi-Domain with Unclear Primary

**User Request:** "Build a REST API in C++ that serves crane status data to a React dashboard"

**Why It's Tricky:**
- C++ is unusual for REST APIs
- MHC domain (crane data)
- Web domain (REST API, React)

**Correct Classification:**
```yaml
category: "CREATION"
primary_domain: "murata_mhc"  # Crane data is core logic
secondary_domain: "web_development"  # REST/React is consumption layer
framework: "R-I-S-E"  # Complex creation, needs research
orchestration_mode: "multi-domain"

rationale: |
  Primary is murata_mhc because:
  - Crane status data comes from MHC system
  - C++ is typical for MHC backend
  - MHC standards apply to data access
  
  Secondary is web_development because:
  - REST API patterns apply
  - React consumption defines response format
```

**Key Insight:** The domain that OWNS the data is usually primary. The domain that CONSUMES is usually secondary.

---

## Quick Reference: Edge Case Decision Tree

```
Is the user asking to FIX something that's BROKEN?
├── YES → REPAIR (even if they say "optimize" or "improve")
└── NO → Continue

Does the core logic/content ALREADY EXIST?
├── YES → Is it being CONVERTED to a new form?
│         ├── YES → TRANSFORMATION
│         └── NO → Is it being DOCUMENTED/EXPLAINED?
│                   ├── YES → UNDERSTANDING
│                   └── NO → OPTIMIZATION
└── NO → CREATION

Is the root cause KNOWN?
├── YES → C-A-R-E (iterate to fix)
└── NO → R-I-S-E (research first)

Are there MULTIPLE TASKS in one request?
├── YES → Split into sequential tasks with dependencies
└── NO → Single classification

Is there a CLEAR TECHNICAL DOMAIN?
├── YES → Use that domain
└── NO → Use general_reasoning

Is confidence below 0.7?
├── YES → Ask clarifying question
└── NO → Proceed with classification
```

---

## Signal Word Priority

When multiple signals conflict, use this priority order:

1. **Broken/Error signals trump all** → REPAIR
   - "error", "bug", "broken", "not working", "fails", "timeout"

2. **Conversion signals indicate transformation** → TRANSFORMATION
   - "migrate", "convert", "port", "refactor", "upgrade"

3. **Explanation signals indicate understanding** → UNDERSTANDING
   - "explain", "document", "analyze", "research", "how does"

4. **New/Build signals indicate creation** → CREATION
   - "create", "build", "implement", "design", "add new"

5. **Default for working systems** → OPTIMIZATION
   - "improve", "faster", "better", "enhance", "optimize"

---

## Related Documentation

- [Problem Classifier](../../frameworks/problem_classifier.md) - Core classification logic
- [Multi-Domain Orchestration](../../core/multi_domain_orchestration.md) - Cross-domain handling
- [C-A-R-E Framework](../../frameworks/universal_care.md) - Iterative refinement
- [R-I-S-E Framework](../../frameworks/universal_rise.md) - Research-first approach

---

**Document Version:** 1.0  
**Author:** CmL  
**Framework:** PlinyHub

