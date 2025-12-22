# Universal C-A-R-E Framework

**Version:** 2.0 (Universal)
**Purpose:** Fast iteration and quality assurance for any domain

---

## Overview

C-A-R-E is an **iterative refinement loop** designed for speed when the problem is understood. Use when you need rapid execution with quality control.

```
    ┌────────────────────────────────────────┐
    │                                        │
    ▼                                        │
┌─────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐
│ CONTEXT │ → │ ANALYZE  │ → │ RESPOND  │ → │ EVALUATE │
│ Load    │   │ Break    │   │ Generate │   │ Check    │
│ State   │   │ Down     │   │ Solution │   │ Quality  │
└─────────┘   └──────────┘   └──────────┘   └─────┬────┘
                                                  │
                                           ┌──────▼──────┐
                                           │ Quality OK? │
                                           └──────┬──────┘
                                            No    │   Yes
                                      ┌───────────┴───────────┐
                                      ▼                       ▼
                              [Iterate from              [Complete]
                               Context]
```

---

## Phase 1: CONTEXT

**Goal:** Rapidly load all relevant state

### Universal Steps

1. **Load Current State**
   - What exists now?
   - What are we working with?
   - What was done previously?

2. **Understand Goal**
   - What specific change is needed?
   - What defines success?
   - What are the boundaries?

3. **Identify Constraints**
   - Time available
   - Quality requirements
   - Domain-specific constraints

### Context Checklist

- [ ] Current state understood
- [ ] Goal is specific and clear
- [ ] Constraints identified

**Time Target:** 1-2 minutes for familiar problems

---

## Phase 2: ANALYZE

**Goal:** Decompose the problem into actionable parts

### Universal Steps

1. **Break Down Task**
   - Split into discrete sub-tasks
   - Identify dependencies
   - Estimate effort for each

2. **Identify Approach**
   - What method will work?
   - What patterns apply?
   - What pitfalls to avoid?

3. **Plan Execution Order**
   - Sequence sub-tasks correctly
   - Identify parallelizable parts
   - Note verification points

### Analyze Checklist

- [ ] Task decomposed into sub-tasks
- [ ] Approach selected
- [ ] Execution order planned

**Time Target:** 2-3 minutes

---

## Phase 3: RESPOND

**Goal:** Generate the solution

### Universal Steps

1. **Execute Sub-Tasks**
   - Follow planned order
   - Apply `[DOMAIN_STANDARDS]`
   - Check each step briefly

2. **Maintain Quality**
   - Don't skip steps for speed
   - Apply standards consistently
   - Document as you go

3. **Handle Blockers**
   - If stuck, note what's blocking
   - If approach fails, analyze why
   - Adjust or escalate as needed

### Respond Checklist

- [ ] All sub-tasks completed
- [ ] Domain standards applied
- [ ] Solution is complete

**Time Target:** Variable (depends on complexity)

---

## Phase 4: EVALUATE

**Goal:** Verify quality and determine if iteration needed

### Universal Steps

1. **Apply Quality Gates**
   - Run `[QUALITY_CHECKS]` from domain module
   - Score against threshold
   - Identify gaps

2. **Check Acceptance Criteria**
   - Does output meet goal?
   - Are all requirements satisfied?
   - Are there any obvious issues?

3. **Decide: Complete or Iterate**

   ```
   IF quality_score >= threshold AND requirements_met:
       → Mark complete
   ELSE IF minor_issues:
       → Quick fix and re-evaluate
   ELSE IF approach_flawed:
       → Return to CONTEXT with lessons learned
   ```

### Evaluate Checklist

- [ ] Quality gates applied
- [ ] Acceptance criteria checked
- [ ] Decision made: complete/iterate

---

## Iteration Strategy

### When to Iterate

| Signal | Action |
|--------|--------|
| Minor quality issues | Fix in place, re-evaluate |
| Missing requirement | Return to Context, add to scope |
| Approach not working | Return to Analyze, try alternative |
| Fundamental misunderstanding | Stop C-A-R-E, switch to R-I-S-E |

### Maximum Iterations

- **Default:** 3 iterations
- **Complex problems:** 5 iterations
- **If exceeding max:** Problem may need R-I-S-E treatment

---

## Domain Module Integration

```yaml
# Example: C-A-R-E with web_development module
domain: web_development
standards:  # Applied in RESPOND
  - Components must be properly typed
  - State management follows patterns
  - Error boundaries present
quality_gates:  # Applied in EVALUATE
  completeness: 0.95
  tests_pass: true
  no_console_errors: true
```

---

## C-A-R-E vs R-I-S-E

| Use C-A-R-E When | Use R-I-S-E When |
|------------------|------------------|
| Problem is understood | Problem needs research |
| Familiar territory | New domain |
| Iteration welcome | Need to get it right first time |
| Speed matters | Thoroughness matters |
| Improving existing | Creating from scratch |

---

## C-A-R-E Quick Reference

```
CONTEXT  → Load state, understand goal, know constraints
ANALYZE  → Decompose, plan approach, order execution
RESPOND  → Execute with standards, maintain quality
EVALUATE → Check quality, decide if done or iterate
```

**Remember:** C-A-R-E is a loop. Budget for 2-3 iterations.
