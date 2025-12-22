# Universal R-I-S-E Framework

**Version:** 2.0 (Universal)
**Purpose:** Domain-agnostic systematic problem-solving methodology

---

## Overview

R-I-S-E is a 4-phase approach that works for **any problem domain**. The phases are universal; domain-specific standards are injected via modules.

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│   RESEARCH   │ → │   IDENTIFY   │ → │  SYNTHESIZE  │ → │   EXECUTE    │
│   Gather     │    │   Pattern    │    │   Design     │    │  Implement   │
│   Context    │    │   Match      │    │   Solution   │    │  + Verify    │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
      ↑                                                            │
      └────────────────── Iterate if needed ──────────────────────┘
```

---

## Phase 1: RESEARCH

**Goal:** Build complete understanding of the problem space

### Universal Steps

1. **Gather Available Information**
   - Read all provided context (documents, code, data)
   - Identify information sources
   - Note what is explicitly stated vs implied

2. **Identify Missing Information**
   - What facts are needed but not provided?
   - What assumptions are being made?
   - What clarifications would help?

3. **Understand Constraints**
   - Time constraints
   - Resource constraints
   - Technical constraints
   - Quality requirements

4. **Create Context Document**
   - Summarize the problem
   - List all known facts
   - Flag uncertainties

### Research Checklist

- [ ] I understand what success looks like
- [ ] I know all explicit requirements
- [ ] I've identified implicit requirements
- [ ] I understand the constraints
- [ ] I've flagged areas of uncertainty

---

## Phase 2: IDENTIFY

**Goal:** Find patterns, requirements, and potential approaches

### Universal Steps

1. **Extract Key Requirements**
   - Functional: What must it do?
   - Non-functional: How well must it do it?
   - Constraints: What can't it do?

2. **Recognize Patterns**
   - Does this match a known problem type?
   - What similar problems have I solved?
   - What approaches work for this category?

3. **Identify Risks**
   - What could go wrong?
   - What edge cases exist?
   - What dependencies are fragile?

4. **Map the Solution Space**
   - What are the possible approaches?
   - What are the trade-offs?
   - Which approach fits the constraints?

### Identify Checklist

- [ ] All requirements extracted and prioritized
- [ ] Problem type classified
- [ ] Similar problems identified
- [ ] Risks catalogued
- [ ] At least 2 potential approaches identified

---

## Phase 3: SYNTHESIZE

**Goal:** Design the solution

### Universal Steps

1. **Generate Solution Options**
   - Create at least 2-3 approaches
   - Don't dismiss ideas prematurely
   - Include conventional and creative options

2. **Evaluate Options**

   ```
   For each option:
   ├── Does it meet all requirements?
   ├── Does it respect all constraints?
   ├── What are the trade-offs?
   ├── What is the implementation complexity?
   └── What is the verification difficulty?
   ```

3. **Select Optimal Approach**
   - Choose approach with best fit
   - Document rationale for selection
   - Document why alternatives were rejected

4. **Create Implementation Plan**
   - Break into discrete steps
   - Identify dependencies between steps
   - Define success criteria for each step

### Synthesize Checklist

- [ ] Multiple options generated
- [ ] Options evaluated against requirements
- [ ] Optimal approach selected with rationale
- [ ] Implementation plan created
- [ ] Success criteria defined

---

## Phase 4: EXECUTE

**Goal:** Implement and verify the solution

### Universal Steps

1. **Implement Solution**
   - Follow implementation plan
   - Apply `[DOMAIN_STANDARDS]` (from domain module)
   - Document decisions and trade-offs

2. **Verify Incrementally**
   - Check each step against success criteria
   - Apply `[QUALITY_GATES]` (from domain module)
   - Don't proceed if verification fails

3. **Handle Failures**
   - If step fails, analyze why
   - Determine if approach is still viable
   - If not, return to SYNTHESIZE with new information

4. **Complete and Document**
   - Verify final output meets all requirements
   - Document what was done and why
   - Capture lessons learned

### Execute Checklist

- [ ] Solution implemented per plan
- [ ] Domain standards applied
- [ ] Each step verified before proceeding
- [ ] Final output meets requirements
- [ ] Solution documented

---

## Domain Module Integration

The `[PLACEHOLDERS]` in Execute phase are filled by domain modules:

```yaml
# Example: How domain module integrates
domain: web_development
standards:
  - Use TypeScript for type safety
  - Follow React hooks patterns
  - Apply proper error handling
quality_gates:
  - All components render without errors
  - No TypeScript compilation errors
  - Accessibility checks pass
```

**To apply a domain module:**

1. Load module: `pliny module load [domain_name]`
2. Standards automatically inject into Execute phase
3. Quality gates apply during verification

---

## When to Use R-I-S-E

| Situation | Use R-I-S-E? | Why |
|-----------|--------------|-----|
| New complex problem | ✅ Yes | Need thorough research first |
| Unfamiliar domain | ✅ Yes | Pattern matching helps |
| High-stakes decision | ✅ Yes | Multiple options important |
| Quick familiar fix | ❌ No | Use C-A-R-E instead |
| Iterating on existing | ❌ No | Use C-A-R-E instead |

---

## R-I-S-E Quick Reference

```
RESEARCH → What do I know? What don't I know?
IDENTIFY → What patterns apply? What could go wrong?
SYNTHESIZE → What are my options? Which is best?
EXECUTE → Implement, verify, document
```

**Remember:** If execution reveals missing information, return to Research.
