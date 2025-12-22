# 3-Layer Meta-Framework Architecture

**Version:** 1.0
**Purpose:** Organize framework operations from execution to framework creation

---

## Overview

The 3-Layer Meta-Framework provides escalation paths when simpler approaches fail. Most problems are solved at Layer 1. Complex problems escalate to Layer 2. Novel problems that reveal framework gaps escalate to Layer 3.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         3-LAYER META-FRAMEWORK                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  LAYER 3: GENESIS (Framework Creation)                                      │
│  ─────────────────────────────────────                                      │
│  Create NEW frameworks when existing ones don't fit                         │
│  • Identify gaps in current framework coverage                              │
│  • Design new framework structure                                           │
│  • Validate with test problems                                              │
│  • Integrate into system                                                    │
│           ▲                                                                 │
│           │ Escalate when no framework fits                                 │
│                                                                             │
│  LAYER 2: ORCHESTRATION (Multi-Framework Coordination)                      │
│  ─────────────────────────────────────────────────────                      │
│  Coordinate MULTIPLE frameworks for complex tasks                           │
│  • Decompose problem into sub-problems                                      │
│  • Assign frameworks to each sub-problem                                    │
│  • Manage handoffs between frameworks                                       │
│  • Synthesize results                                                       │
│           ▲                                                                 │
│           │ Escalate when single framework insufficient                     │
│                                                                             │
│  LAYER 1: EXECUTION (Single Framework Application)                          │
│  ─────────────────────────────────────────────────                          │
│  Apply EXISTING frameworks to problems                                      │
│  • Classify problem                                                         │
│  • Select appropriate framework                                             │
│  • Execute framework phases                                                 │
│  • Verify results                                                           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Layer 1: EXECUTION

**Purpose:** Apply existing frameworks to single problems

### Process

```
1. CLASSIFY problem (category, domain, complexity)
2. SELECT framework (R-I-S-E, C-A-R-E, HARVEST)
3. LOAD domain module
4. EXECUTE framework phases
5. VERIFY results against quality gates
6. COMPLETE or iterate
```

### When to Stay at Layer 1

- Problem fits a single framework
- Domain module exists
- No cross-cutting concerns
- Complexity is manageable

### When to Escalate to Layer 2

- Problem requires multiple frameworks
- Cross-cutting concerns exist
- Dependencies between sub-problems
- Single framework isn't making progress

---

## Layer 2: ORCHESTRATION

**Purpose:** Coordinate multiple frameworks for complex tasks

### Process

```
1. DECOMPOSE problem into sub-problems
2. CLASSIFY each sub-problem independently
3. ASSIGN framework to each sub-problem
4. SEQUENCE execution (handle dependencies)
5. EXECUTE each sub-problem with appropriate framework
6. SYNTHESIZE results into unified solution
7. VERIFY integrated result
```

### Sub-Problem Decomposition

```yaml
decomposition:
  original_problem: "Build full-stack feature with documentation"
  
  sub_problems:
    - id: "SP-1"
      description: "Design backend API"
      category: "CREATION"
      framework: "R-I-S-E"
      dependencies: []
      
    - id: "SP-2"
      description: "Implement backend"
      category: "CREATION"
      framework: "C-A-R-E"
      dependencies: ["SP-1"]
      
    - id: "SP-3"
      description: "Design frontend components"
      category: "CREATION"
      framework: "R-I-S-E"
      dependencies: ["SP-1"]
      
    - id: "SP-4"
      description: "Implement frontend"
      category: "CREATION"
      framework: "C-A-R-E"
      dependencies: ["SP-2", "SP-3"]
      
    - id: "SP-5"
      description: "Write documentation"
      category: "UNDERSTANDING"
      framework: "HARVEST"
      dependencies: ["SP-2", "SP-4"]
  
  execution_order: ["SP-1", "SP-2", "SP-3", "SP-4", "SP-5"]
```

### Handoff Protocol

When transitioning between sub-problems:

```yaml
handoff:
  from: "SP-1"
  to: "SP-2"
  artifacts_passed:
    - api_specification.yaml
    - data_models.ts
  context_transferred:
    - design_decisions: "[Key choices made]"
    - constraints: "[Limitations discovered]"
    - open_questions: "[Unresolved issues]"
```

### When to Stay at Layer 2

- Decomposition is clear
- Existing frameworks cover all sub-problems
- No fundamental gaps in framework coverage

### When to Escalate to Layer 3

- No existing framework adequately addresses a sub-problem
- Pattern of failures indicates framework gap
- Novel problem type not covered

---

## Layer 3: GENESIS (Framework Creation)

**Purpose:** Create new frameworks when existing ones are insufficient

### The GENESIS Process

```
┌───────────────────────────────────────────────────────────────────────────┐
│                         GENESIS: Framework Creation                        │
├───────────────────────────────────────────────────────────────────────────┤
│                                                                           │
│  1. IDENTIFY GAP                                                          │
│     ├── What problem type isn't well-served?                             │
│     ├── Why do existing frameworks fail?                                 │
│     └── What's unique about this problem class?                          │
│                                                                           │
│  2. DESIGN FRAMEWORK                                                      │
│     ├── Define phases (typically 3-7)                                    │
│     ├── Define inputs and outputs for each phase                         │
│     ├── Define quality gates                                             │
│     └── Define iteration criteria                                        │
│                                                                           │
│  3. VALIDATE FRAMEWORK                                                    │
│     ├── Test on 3+ representative problems                               │
│     ├── Measure effectiveness vs. existing frameworks                    │
│     └── Gather feedback and refine                                       │
│                                                                           │
│  4. INTEGRATE FRAMEWORK                                                   │
│     ├── Add to problem classifier                                        │
│     ├── Create documentation                                             │
│     ├── Add to CLI commands                                              │
│     └── Train users                                                      │
│                                                                           │
│  5. MONITOR & IMPROVE                                                     │
│     ├── Track usage and success rates                                    │
│     ├── Collect feedback                                                 │
│     └── Iterate on framework design                                      │
│                                                                           │
└───────────────────────────────────────────────────────────────────────────┘
```

### New Framework Template

```yaml
framework:
  name: "[FRAMEWORK_NAME]"
  acronym: "[X-X-X-X]"
  version: "1.0"
  created: "2025-12-20"
  author: "CmL"
  
  purpose: "[What problem class does this solve?]"
  
  when_to_use:
    - "[Condition 1]"
    - "[Condition 2]"
  
  when_not_to_use:
    - "[Anti-condition 1]"
    - "[Anti-condition 2]"
  
  phases:
    - name: "[Phase 1 Name]"
      letter: "[X]"
      purpose: "[What this phase accomplishes]"
      inputs: 
        - "[input 1]"
        - "[input 2]"
      outputs: 
        - "[output 1]"
        - "[output 2]"
      quality_gate: "[How to know phase is complete]"
      
    - name: "[Phase 2 Name]"
      letter: "[Y]"
      purpose: "[What this phase accomplishes]"
      inputs: 
        - "[input from previous phase]"
      outputs: 
        - "[output for next phase]"
      quality_gate: "[Completion criteria]"
  
  iteration:
    continue_when: "[Condition to iterate]"
    stop_when: "[Condition to finish]"
    max_iterations: 5
  
  success_metrics:
    - name: "[Metric 1]"
      target: "[Target value]"
      measure: "[How to measure]"
    - name: "[Metric 2]"
      target: "[Target value]"
      measure: "[How to measure]"
  
  domain_integration:
    uses_domain_modules: true
    placeholder_locations:
      - phase: "[Phase Name]"
        placeholder: "[DOMAIN_STANDARDS]"
      - phase: "[Phase Name]"
        placeholder: "[QUALITY_GATES]"
```

### Framework Validation Criteria

Before a new framework is integrated:

| Criterion | Threshold | Measure |
|-----------|-----------|---------|
| **Effectiveness** | 80%+ | Success rate on test problems |
| **Efficiency** | Better than existing | Time/iterations vs. closest alternative |
| **Coverage** | New ground | Handles cases existing frameworks don't |
| **Clarity** | Understandable | Can be explained in <2 minutes |
| **Consistency** | Predictable | Similar inputs → similar outputs |

---

## Escalation Triggers

| From | To | Trigger |
|------|-----|---------|
| Layer 1 → Layer 2 | Problem requires multiple frameworks |
| Layer 1 → Layer 2 | Cross-cutting concerns detected |
| Layer 1 → Layer 2 | Single framework stuck after 3 iterations |
| Layer 2 → Layer 3 | No framework covers a sub-problem |
| Layer 2 → Layer 3 | Repeated failures indicate systemic gap |
| Layer 2 → Layer 3 | User explicitly requests new framework |

### Iteration Limit Clarification

Different frameworks have different iteration limits based on their purpose:

| Framework | Default Limit | Extended Limit | Purpose |
|-----------|--------------|----------------|---------|
| **C-A-R-E** | 3 iterations | 5 for complex | Quick fixes, familiar territory |
| **R-I-S-E** | No fixed limit | N/A | Thorough research, complex problems |
| **HARVEST** | 5 iterations | N/A | Documentation synthesis |

**Escalation Flow:**
- C-A-R-E stuck after 3 iterations → Escalate to Layer 2 (orchestration) or switch to R-I-S-E
- Layer 1 stuck → Escalate to Layer 2
- Layer 2 sub-problem stuck → Consider Layer 3 (GENESIS)

**Why Different Limits?**
- **C-A-R-E** is for familiar problems—if 3 iterations don't work, the problem may be misclassified
- **R-I-S-E** is for research—complex investigations may require many iterations naturally
- **HARVEST** is for documentation—synthesis converges within 5 iterations or needs human review

---

## Example: Layer 2 Orchestration

**Problem:** "Build a monitoring dashboard with real-time alerts"

```yaml
orchestration:
  problem: "Build monitoring dashboard with real-time alerts"
  
  decomposition:
    - sub_problem: "Design alert system architecture"
      framework: "R-I-S-E"
      category: "CREATION"
      estimated_complexity: "complex"
      
    - sub_problem: "Implement backend alert service"
      framework: "R-I-S-E"
      category: "CREATION"
      estimated_complexity: "moderate"
      
    - sub_problem: "Design dashboard UI"
      framework: "R-I-S-E"
      category: "CREATION"
      estimated_complexity: "moderate"
      
    - sub_problem: "Implement dashboard components"
      framework: "C-A-R-E"
      category: "CREATION"
      estimated_complexity: "moderate"
      
    - sub_problem: "Integrate real-time updates"
      framework: "C-A-R-E"
      category: "TRANSFORMATION"
      estimated_complexity: "moderate"
      
    - sub_problem: "Document system"
      framework: "HARVEST"
      category: "UNDERSTANDING"
      estimated_complexity: "simple"

  execution_sequence:
    phase_1: ["Design architecture", "Design UI"]  # Parallel
    phase_2: ["Implement backend", "Implement frontend"]  # Parallel after phase_1
    phase_3: ["Integrate real-time"]  # After phase_2
    phase_4: ["Document"]  # After phase_3

  synthesis:
    - Verify all components integrate correctly
    - Run end-to-end tests
    - Validate against original requirements
```

---

## Example: Layer 3 GENESIS

**Scenario:** Repeated failures debugging distributed systems suggest need for new framework.

```yaml
genesis:
  gap_identified:
    observation: "None of our frameworks handle distributed system debugging well"
    failures:
      - "R-I-S-E too slow for time-sensitive debugging"
      - "C-A-R-E doesn't handle multi-service coordination"
      - "No framework addresses log correlation across services"
    
  new_framework_design:
    name: "Distributed Debug Framework"
    acronym: "T-R-A-C-E"
    
    phases:
      - name: "Triage"
        purpose: "Quickly identify which service is the source"
        
      - name: "Reproduce"
        purpose: "Create minimal reproduction case"
        
      - name: "Analyze"
        purpose: "Deep dive into identified service"
        
      - name: "Correlate"
        purpose: "Connect logs/traces across services"
        
      - name: "Execute fix"
        purpose: "Implement and verify fix"
    
  validation_plan:
    - Test on 3 recent distributed system bugs
    - Measure time-to-resolution vs. ad-hoc debugging
    - Gather feedback from team

  integration:
    - Add "T-R-A-C-E" to problem classifier under REPAIR category
    - Create modules/distributed_systems.yaml
    - Add pliny trace CLI command
```

---

## Quick Reference

```
LAYER 1: EXECUTION
  └─ Apply single framework to single problem
  └─ Escalate when: multi-framework needed, stuck after 3 iterations

LAYER 2: ORCHESTRATION  
  └─ Decompose → Assign → Sequence → Execute → Synthesize
  └─ Escalate when: no framework fits, repeated failures

LAYER 3: GENESIS
  └─ IDENTIFY gap → DESIGN framework → VALIDATE → INTEGRATE → MONITOR
  └─ Only when existing frameworks fundamentally insufficient
```
