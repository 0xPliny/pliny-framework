# Edge Case Handling Guide

**Version:** 1.0  
**Purpose:** Comprehensive guide for handling edge cases and ambiguous scenarios in the Pliny Framework

---

## Overview

This document provides explicit decision trees and protocols for handling edge cases, ambiguous scenarios, and situations where standard framework flows don't apply cleanly.

---

## Layer Escalation Decision Trees

### When to Escalate from Layer 1 to Layer 2

**Decision Tree:**

```
Layer 1 (Single Framework) Execution
    │
    ├─→ Problem solved successfully?
    │   └─→ YES: Complete at Layer 1
    │
    ├─→ Single framework insufficient after 3+ iterations?
    │   └─→ YES: Escalate to Layer 2
    │
    ├─→ Problem requires multiple distinct frameworks?
    │   └─→ YES: Escalate to Layer 2
    │       Examples:
    │       - Creation + Documentation (R-I-S-E + HARVEST)
    │       - Repair + Optimization (C-A-R-E + C-A-R-E)
    │       - Multiple sub-problems with different categories
    │
    ├─→ Cross-cutting concerns detected?
    │   └─→ YES: Escalate to Layer 2
    │       Examples:
    │       - Frontend + Backend changes needed
    │       - Code + Documentation + Tests required
    │       - Multiple domains involved
    │
    └─→ Dependencies between sub-problems?
        └─→ YES: Escalate to Layer 2
            Examples:
            - Backend API must be created before frontend
            - Data migration before code migration
            - Architecture design before implementation
```

**Explicit Triggers for Layer 1 → Layer 2:**

1. **Multiple Frameworks Needed**
   - Problem decomposition reveals sub-problems requiring different frameworks
   - Example: "Build dashboard with documentation" → R-I-S-E (creation) + HARVEST (documentation)

2. **3+ Iterations Without Progress**
   - Single framework stuck after 3 iterations
   - Quality not improving
   - No clear path forward

3. **Cross-Cutting Concerns**
   - Problem spans multiple domains
   - Requires coordination across systems
   - Multiple artifact types needed

4. **Complex Dependencies**
   - Sub-problems have clear dependencies
   - Sequential execution needed
   - Handoff artifacts required

### When to Escalate from Layer 2 to Layer 3

**Decision Tree:**

```
Layer 2 (Orchestration) Execution
    │
    ├─→ All sub-problems have matching frameworks?
    │   └─→ YES: Continue at Layer 2
    │
    ├─→ No framework fits a sub-problem?
    │   └─→ YES: Escalate to Layer 3
    │       Examples:
    │       - Novel problem type not in taxonomy
    │       - Existing frameworks fundamentally insufficient
    │       - Pattern of failures indicates framework gap
    │
    ├─→ Repeated failures across multiple sub-problems?
    │   └─→ YES: Escalate to Layer 3
    │       - Indicates systemic framework gap
    │       - May need new framework category
    │
    ├─→ User explicitly requests new framework?
    │   └─→ YES: Escalate to Layer 3
    │
    └─→ Framework validation criteria met but still failing?
        └─→ YES: Escalate to Layer 3
            - Existing frameworks validated but insufficient
            - Need framework creation (GENESIS)
```

**Explicit Triggers for Layer 2 → Layer 3:**

1. **No Framework Fits Sub-Problem**
   - Sub-problem doesn't match any framework's purpose
   - Existing frameworks fail validation criteria
   - Novel problem type identified

2. **Pattern of Failures**
   - Multiple similar sub-problems fail with existing frameworks
   - Systematic gap identified
   - Framework library incomplete

3. **User Request**
   - User explicitly requests framework creation
   - User identifies framework gap
   - User has novel problem pattern

---

## Iteration Limit Handling

### C-A-R-E Iteration Limits

**Default Limit:** 3 iterations

**When Limit Reached:**

```
C-A-R-E Iteration 3 Complete
    │
    ├─→ Quality >= threshold?
    │   └─→ YES: Complete successfully
    │
    ├─→ Quality improving each iteration?
    │   └─→ YES: Extend limit to 5 iterations
    │       Conditions:
    │       - Quality improved: iteration_1 < iteration_2 < iteration_3
    │       - Gap to threshold closing
    │       - No fundamental approach flaws
    │
    ├─→ Quality plateaued (not improving)?
    │   └─→ Escalate to R-I-S-E
    │       - Problem complexity underestimated
    │       - Need RESEARCH phase
    │       - Re-assess classification
    │
    ├─→ Quality declining?
    │   └─→ Return to ANALYZE phase
    │       - Approach may be flawed
    │       - Try alternative approach
    │       - Consider escalation if persists
    │
    └─→ Multiple blocking issues?
        └─→ Escalate to R-I-S-E
            - Problem misclassified
            - Need thorough analysis
            - Re-classify problem
```

**Extension Criteria:**
- Quality improved in iterations 1, 2, 3
- Gap to threshold is < 20%
- No approach flaws detected
- Estimated 1-2 more iterations sufficient

**Escalation Criteria:**
- Quality plateaued after 3 iterations
- Multiple blocking issues identified
- Requirements unclear or incomplete
- Problem complexity misassessed

### HARVEST Iteration Limits

**Default Limit:** 5 iterations

**When Limit Reached:**

```
HARVEST Iteration 5 Complete
    │
    ├─→ Quality >= 95%?
    │   └─→ YES: Complete successfully
    │
    ├─→ Quality > 85%?
    │   └─→ YES: Accept with documented gaps
    │       - Document all gaps explicitly
    │       - Mark incomplete sections
    │       - Note source material limitations
    │       - Allow user review/editing
    │
    ├─→ Quality 75-85%?
    │   └─→ Accept with strong warnings
    │       - Document gaps extensively
    │       - Request user intervention
    │       - Schedule follow-up improvement
    │       - Provide gap analysis
    │
    └─→ Quality < 75%?
        └─→ Request user intervention
            - Source material may be insufficient
            - Manual documentation may be needed
            - Consider alternative documentation approach
            - Provide detailed gap analysis
```

### R-I-S-E Iteration Handling

**No Hard Limit:** R-I-S-E has no fixed iteration limit

**When to Escalate:**

```
R-I-S-E Execution
    │
    ├─→ Making progress?
    │   └─→ YES: Continue R-I-S-E
    │
    ├─→ 3+ iterations without progress?
    │   └─→ YES: Escalate to Layer 2
    │       - May need decomposition
    │       - Multiple frameworks may be needed
    │
    ├─→ 5+ iterations without progress?
    │   └─→ YES: Strongly consider Layer 3
    │       - Problem may be fundamentally novel
    │       - Framework gap may exist
    │       - Need GENESIS layer
    │
    └─→ Problem simpler than expected?
        └─→ Switch to C-A-R-E
            - R-I-S-E may be overkill
            - Quick iteration may be sufficient
            - Re-assess complexity
```

---

## Confidence Threshold Handling

### Persistent Low Confidence (< 0.7)

**After 2 Clarification Attempts:**

```
Confidence < 0.7 After 2 Clarifications
    │
    ├─→ Category confidence < 0.7?
    │   └─→ Default to CREATION + R-I-S-E
    │       - Safest default (most thorough)
    │       - Allows user override
    │       - Document uncertainty explicitly
    │
    ├─→ Domain confidence < 0.7?
    │   └─→ Default to general_reasoning
    │       - Universal patterns only
    │       - No domain-specific assumptions
    │       - Ask user to specify domain
    │
    ├─→ Framework confidence < 0.7?
    │   └─→ Default to R-I-S-E
    │       - Most thorough framework
    │       - Handles complexity best
    │       - Can switch to C-A-R-E if simpler
    │
    └─→ Overall confidence < 0.5?
        └─→ Explicit user intervention required
            - Present classification options
            - Ask user to choose
            - Proceed with user selection
            - Still document confidence
```

### Handling Persistent Uncertainty

**Protocol:**

1. **Acknowledge Uncertainty Explicitly**
   ```
   "Classification confidence is low (X%) after clarification attempts.
   Proceeding with default: [CATEGORY] + [FRAMEWORK] + [DOMAIN].
   
   If this is incorrect, please specify: [DOMAIN: X] [FRAMEWORK: Y]"
   ```

2. **Provide Override Mechanism**
   - Always allow user to explicitly override
   - Accept manual classification
   - Proceed with user-specified path

3. **Document for Learning**
   - Log ambiguous classifications
   - Record user corrections
   - Update classifier patterns
   - Improve future accuracy

### Confidence Calibration

**Low Confidence Indicators:**
- < 0.5: Very uncertain, require user input
- 0.5-0.7: Uncertain, use defaults with override option
- 0.7-0.85: Moderate confidence, proceed with monitoring
- 0.85+: High confidence, proceed normally

---

## Multi-Domain Conflict Resolution

### Detecting Conflicts

**When Multiple Domains Detected:**

```
Multiple Domain Signals Detected
    │
    ├─→ Single primary domain identifiable?
    │   └─→ YES: Use primary, ignore secondary
    │       - Apply primary domain standards
    │       - Use secondary only where non-conflicting
    │
    ├─→ Clear primary/secondary relationship?
    │   └─→ YES: Use multi-domain orchestration
    │       - Apply primary standards first
    │       - Apply secondary where non-conflicting
    │       - Document conflicts explicitly
    │
    └─→ Conflicting standards?
        └─→ YES: Use conflict resolution protocol
```

### Conflict Resolution Protocol

**Priority Rules:**

1. **Primary Domain Takes Precedence**
   - Primary domain standards applied first
   - Secondary domain standards where non-conflicting
   - Document all conflicts

2. **Explicit Conflict Resolution**
   ```yaml
   conflict_resolution:
     conflict: "String handling: cc_str vs TypeScript string methods"
     primary_domain: "murata_mhc"
     secondary_domain: "web_development"
     resolution: "Use cc_str (primary domain standard)"
     rationale: "Backend logic requires MHC standards"
     documented: true
   ```

3. **Boundary Mapping**
   - At domain boundaries, create explicit mappings
   - Example: GP.BAD (MHC) → HTTP 500 (Web)
   - Document all boundary conversions

4. **User Override**
   - Allow user to specify resolution
   - Accept manual conflict resolution
   - Document user decisions

### Three or More Domains

**Handling Multiple Domains:**

1. **Identify Primary Domain**
   - Where does core logic/data live?
   - Which domain is most critical?
   - User-specified primary takes precedence

2. **Order Secondary Domains**
   - By importance/criticality
   - By dependency order
   - Apply in sequence

3. **Resolve Conflicts Sequentially**
   - Primary vs Secondary 1
   - Result vs Secondary 2
   - Continue for all domains

4. **Document All Resolutions**
   - List all conflicts
   - Document resolution rationale
   - Note any compromises

---

## User Override Mechanisms

### Classification Override

**When User Wants to Override Classification:**

```yaml
user_override:
  original_classification:
    category: "CREATION"
    confidence: 0.45
  user_override:
    category: "TRANSFORMATION"
    domain: "web_development"
    framework: "R-I-S-E"
  accepted: true
  rationale: "User specified explicit classification"
  confidence_adjusted: "User override, proceeding with user selection"
```

**Override Process:**
1. User specifies: `[DOMAIN: X] [FRAMEWORK: Y]` or explicit classification
2. Accept user override
3. Proceed with user-specified classification
4. Still apply confidence protocol (may note override)
5. Log override for learning

### Framework Override

**When User Wants Different Framework:**

**Process:**
1. User requests specific framework
2. Validate framework is appropriate for category
3. Warn if framework seems mismatched
4. Proceed with user selection
5. Document override

**Validation:**
- CREATION/TRANSFORMATION: R-I-S-E or C-A-R-E (if simple)
- REPAIR/OPTIMIZATION: C-A-R-E or R-I-S-E (if complex)
- UNDERSTANDING: HARVEST

### Complexity Override

**When User Wants to Adjust Complexity:**

**Process:**
1. User specifies complexity level
2. Adjust framework selection if needed
3. Adjust verification intensity
4. Proceed with user-specified complexity
5. Document any adjustments

---

## Edge Case Scenarios

### Scenario: "Make This Better" (Vague Request)

**Handling:**
1. Ask clarifying questions:
   - "Do you want to fix something broken?"
   - "Improve performance?"
   - "Add new features?"
   - "Refactor code structure?"

2. Based on answer, classify:
   - Fix broken → REPAIR
   - Improve performance → OPTIMIZATION
   - Add features → CREATION
   - Refactor → TRANSFORMATION

3. Proceed with classification

### Scenario: "Create a Bug Fix"

**Classification:** REPAIR (focus on deliverable, not verb)

**Rationale:**
- Deliverable is fixing a bug
- "Create" is implementation verb, not category
- Focus on what user wants (fixed bug)

### Scenario: "Optimize the Timeouts" (But They're Failing)

**Classification:** REPAIR (broken trumps optimize)

**Rationale:**
- If something is broken, it must be fixed first
- REPAIR takes priority over OPTIMIZATION
- Fix broken, then optimize if needed

### Scenario: Root Cause Unknown for REPAIR

**Handling:**
1. Classify as REPAIR (correct category)
2. If root cause unknown: Switch to R-I-S-E framework
3. Use RESEARCH phase to find root cause
4. Then proceed with repair

**Decision:**
```
REPAIR Problem
    │
    ├─→ Root cause known?
    │   └─→ YES: Use C-A-R-E (quick fix)
    │
    └─→ Root cause unknown?
        └─→ Use R-I-S-E (research first)
            - RESEARCH: Find root cause
            - IDENTIFY: Understand problem
            - SYNTHESIZE: Design fix
            - EXECUTE: Implement fix
```

### Scenario: C-A-R-E Exceeds 3 Iterations

**See:** Iteration Limit Handling section above

### Scenario: Multiple Tasks in One Request

**Handling:**
1. Identify distinct tasks
2. Split into sequential tasks with dependencies
3. Handle each task separately
4. Use Layer 2 (Orchestration) if needed
5. Execute in dependency order

**Example:**
```
Request: "Create API endpoint and write tests and document it"

Tasks:
1. Create API endpoint (CREATION → R-I-S-E)
2. Write tests (CREATION → C-A-R-E, depends on #1)
3. Document it (UNDERSTANDING → HARVEST, depends on #1, #2)

Use Layer 2 Orchestration to coordinate.
```

---

## OMEGA Loop Edge Cases

### When Does OMEGA.LEARN Execute?

**Execution Triggers:**
- After successful framework completion
- After framework failure (learn from mistakes)
- After verification completion
- At end of problem-solving session

**Not Executed:**
- During framework execution (too frequent)
- After every phase (too granular)
- On user interruption (incomplete context)

### How Are Learnings Retrieved in OMEGA.OBSERVE?

**Retrieval Process:**

1. **Problem Signature Matching**
   - Extract keywords, domain, category
   - Match against stored learnings
   - Rank by relevance

2. **Semantic Similarity**
   - Compare problem descriptions
   - Match patterns and contexts
   - Surface relevant learnings

3. **Top-N Retrieval**
   - Retrieve top 5-10 most relevant learnings
   - Present during OBSERVE phase
   - Use to inform framework selection

**If Knowledge Base Empty:**
- Proceed without prior learnings
- Build knowledge base from scratch
- No degradation in functionality

### What If Knowledge Base Is Empty?

**Handling:**
1. Proceed normally (framework works without learnings)
2. Start building knowledge base
3. First problems have no prior knowledge
4. Learnings accumulate over time
5. Framework improves with use

**No Special Handling Required:**
- Framework is functional without learnings
- Learnings are enhancement, not requirement
- Empty knowledge base is valid starting state

---

## Quick Reference Decision Trees

### Classification Uncertainty

```
Confidence < 0.7?
    ├─→ After 2 clarifications? → Default to safest + allow override
    └─→ Still < 0.5? → Require user input
```

### Framework Selection Uncertainty

```
Framework unclear?
    ├─→ Category known? → Use category default
    ├─→ Complexity simple? → C-A-R-E
    └─→ Otherwise? → R-I-S-E (safest)
```

### Iteration Limit Reached

```
C-A-R-E: 3 iterations
    ├─→ Quality improving? → Extend to 5
    └─→ Quality plateaued? → Escalate to R-I-S-E

HARVEST: 5 iterations
    ├─→ Quality > 85%? → Accept with gaps
    └─→ Quality < 75%? → Request user intervention
```

### Layer Escalation

```
Layer 1 stuck?
    ├─→ 3+ iterations? → Escalate to Layer 2
    └─→ Multiple frameworks needed? → Escalate to Layer 2

Layer 2 stuck?
    ├─→ No framework fits? → Escalate to Layer 3
    └─→ Pattern of failures? → Escalate to Layer 3
```

---

## See Also

- [Error Handling Protocol](../frameworks/error_handling_protocol.md) - Comprehensive error handling
- [Meta-Framework](../frameworks/meta_framework.md) - Layer escalation details
- [Problem Classifier](../frameworks/problem_classifier.md) - Classification procedures
- [Multi-Domain Orchestration](../core/multi_domain_orchestration.md) - Conflict resolution
- [Troubleshooting Guide](TROUBLESHOOTING.md) - Common edge case solutions

---

**Version:** 1.0  
**Last Updated:** December 2024

