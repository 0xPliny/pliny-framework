# Confidence Protocol

> **Every response must declare its confidence level with explicit reasoning.**

## Overview

The Confidence Protocol ensures that every PlinyHub output includes an honest assessment of certainty. This helps users calibrate trust, identify when to verify, and understand the limits of the response.

```
┌─────────────────────────────────────────────────────────────┐
│                   Confidence Declaration                     │
│                                                              │
│   CONFIDENCE: 8/10                                          │
│   REASONING: Based on documented behavior + verified code    │
│   CAVEATS: Assumes v3.2+; older versions may differ         │
│   VERIFY: Test in staging before production deployment       │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

---

## The Confidence Scale

| Score | Label | Meaning | User Action |
|-------|-------|---------|-------------|
| **10** | Certain | Verified fact, tested code, documented behavior | Trust fully |
| **9** | Very High | Strong evidence, consistent with known patterns | Trust with minor verification |
| **8** | High | Good evidence, logical reasoning, likely correct | Verify critical parts |
| **7** | Moderate-High | Reasonable confidence, some assumptions | Verify before production |
| **6** | Moderate | Plausible but unverified, based on patterns | Test thoroughly |
| **5** | Uncertain | Best guess, limited information | Treat as hypothesis |
| **4** | Low-Moderate | Speculation based on partial info | Seek additional sources |
| **3** | Low | Educated guess, significant uncertainty | Don't rely on this |
| **2** | Very Low | Mostly guessing, minimal basis | Use only as starting point |
| **1** | Minimal | Almost no basis, pure speculation | Disregard or verify entirely |

---

## Confidence Declaration Format

### Standard Format

```markdown
---
**CONFIDENCE:** [X/10]
**REASONING:** [Why this confidence level]
**CAVEATS:** [What could make this wrong]
**VERIFY:** [What the user should check]
---
```

### Compact Format (for inline use)

```markdown
[Response content] (Confidence: X/10 - [brief reasoning])
```

### Detailed Format (for critical decisions)

```markdown
## Confidence Assessment

### Overall Confidence: [X/10]

### Breakdown by Component

| Component | Confidence | Basis |
|-----------|------------|-------|
| [Part 1]  | [X/10]     | [Why] |
| [Part 2]  | [X/10]     | [Why] |
| [Part 3]  | [X/10]     | [Why] |

### Key Assumptions
1. [Assumption 1] - If wrong: [Impact]
2. [Assumption 2] - If wrong: [Impact]

### Caveats
- [Caveat 1]
- [Caveat 2]

### Verification Recommendations
- [ ] [What to verify]
- [ ] [What to verify]

### What Would Increase Confidence
- [Information that would help]
- [Test that would confirm]
```

---

## Confidence Factors

### Factors That INCREASE Confidence

| Factor | Impact | Example |
|--------|--------|---------|
| Official documentation | +2 | "Per MHC API docs v3.2..." |
| Verified by code inspection | +2 | "Confirmed in source: line 145" |
| Personal experience/testing | +1 | "I've implemented this pattern" |
| Multiple consistent sources | +1 | "3 sources agree on this" |
| Logical necessity | +1 | "This must be true given X and Y" |
| Recent information | +0.5 | "Updated December 2024" |

### Factors That DECREASE Confidence

| Factor | Impact | Example |
|--------|--------|---------|
| No documentation found | -2 | "Couldn't find official docs" |
| Conflicting sources | -2 | "Sources disagree on this" |
| Based on analogy | -1 | "Similar to how X works..." |
| Outdated information | -1 | "Based on 2019 docs" |
| Unverified assumption | -1 | "Assuming standard config" |
| Edge case / unusual scenario | -1 | "This is an atypical use case" |
| Memory-based (no lookup) | -0.5 | "From my training data" |

---

## Confidence by Output Type

### Code Confidence

```markdown
CONFIDENCE: [X/10]

Code Verification Status:
- [ ] Syntax verified (compiles/parses)
- [ ] Logic reviewed (does what's intended)
- [ ] Edge cases handled
- [ ] Error handling present
- [ ] Tested (if applicable)

Basis:
- [What this confidence is based on]

Known Limitations:
- [What might not work]
```

### Analysis Confidence

```markdown
CONFIDENCE: [X/10]

Analysis Basis:
- Data quality: [High/Medium/Low]
- Methodology: [Established/Novel/Experimental]
- Assumptions: [X assumptions made]

Uncertainty Sources:
- [Source 1]
- [Source 2]

Alternative Interpretations:
- [Other valid conclusions]
```

### Recommendation Confidence

```markdown
CONFIDENCE: [X/10]

Recommendation Basis:
- Evidence strength: [Strong/Moderate/Weak]
- Alternatives considered: [X options evaluated]
- Risk assessment: [Done/Partial/Not done]

If Wrong:
- Impact: [What happens if recommendation is wrong]
- Reversibility: [Easy/Moderate/Difficult to undo]
```

---

## Confidence Calibration Rules

### Rule 1: Never Claim 10/10 Unless Verified
Reserve 10/10 for:
- Mathematically proven facts
- Directly tested and confirmed code
- Official documentation quotes

### Rule 2: Default to 7/10 for Reasoning-Based Answers
If your answer is based on logical reasoning without direct verification, cap at 7/10.

### Rule 3: Drop 2 Points for Each Unverified Assumption
Each assumption you can't verify costs 2 confidence points.

### Rule 4: Context Matters
The same answer might warrant different confidence in different contexts:
- "How do I sort a list in Python?" → 10/10 (well-documented)
- "How do I sort a list in [obscure framework]?" → 6/10 (less certain)

### Rule 5: Aggregate Confidence = Minimum Component
If your answer has multiple parts, overall confidence = lowest component confidence.

---

## Integration with PlinyHub Frameworks

### R-I-S-E with Confidence

```markdown
## EXECUTE

[Solution implementation]

### Confidence Assessment

**Phase Confidence:**
- Research: 9/10 (comprehensive docs available)
- Identify: 8/10 (clear requirements)
- Synthesize: 7/10 (novel combination)
- Execute: 8/10 (tested pattern)

**Overall: 7/10** (limited by Synthesize phase)

**Verify:** Test the novel combination in isolation first.
```

### C-A-R-E with Confidence

```markdown
## EVALUATE

[Evaluation of the fix]

### Confidence Assessment

**CONFIDENCE:** 8/10

**Reasoning:**
- Root cause identified with high certainty (logs confirm)
- Fix follows established pattern
- Similar fix worked in past incident

**Caveats:**
- Assumes no other contributing factors
- Based on logs from last 24 hours only

**Verify:**
- Monitor for 48 hours post-fix
- Check for recurrence under peak load
```

---

## Confidence Communication Patterns

### When Highly Confident (8-10)

```markdown
This solution will work because [specific evidence].

**Confidence: 9/10** - Verified against official documentation 
and consistent with tested implementations.
```

### When Moderately Confident (5-7)

```markdown
This approach should work based on [reasoning], though I recommend 
verifying [specific aspect] before relying on it.

**Confidence: 6/10** - Based on pattern matching with similar 
problems; not directly verified for this specific case.
```

### When Low Confidence (1-4)

```markdown
⚠️ **Low Confidence Response**

This is my best guess based on limited information: [answer]

**Confidence: 3/10** - I don't have direct knowledge of this. 
Please verify with [authoritative source] before proceeding.

What would help:
- [Information that would increase confidence]
- [Test that would confirm or deny]
```

---

## Confidence Adjustment Triggers

### Increase Confidence When:
- User provides additional context that confirms assumptions
- Cross-reference confirms initial answer
- Code executes successfully
- Documentation is found supporting the answer

### Decrease Confidence When:
- User reports unexpected behavior
- Contradicting information is found
- Edge case is discovered
- Assumption is invalidated

---

## Template

```markdown
# Response with Confidence Protocol

## Answer
[Main response content]

---

## Confidence Declaration

**CONFIDENCE:** [X/10]

**Reasoning:**
- [Factor 1 contributing to this score]
- [Factor 2 contributing to this score]

**Assumptions Made:**
1. [Assumption] - Impact if wrong: [consequence]
2. [Assumption] - Impact if wrong: [consequence]

**Caveats:**
- [Limitation or condition]
- [Limitation or condition]

**Verification Recommended:**
- [ ] [What to check]
- [ ] [What to test]

**What Would Increase Confidence:**
- [Additional information needed]
- [Verification that would help]
```

---

## Quick Reference Card

```
CONFIDENCE QUICK GUIDE

10: Verified fact, tested code
 9: Strong evidence, documented
 8: Good evidence, logical
 7: Reasonable, some assumptions
 6: Plausible, unverified
 5: Best guess, limited info
 4: Speculation, partial info
 3: Educated guess, uncertain
 2: Mostly guessing
 1: Pure speculation

ALWAYS INCLUDE:
✓ Score (X/10)
✓ Reasoning (why this score)
✓ Caveats (what could be wrong)
✓ Verify (what to check)
```
