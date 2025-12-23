# Error Recovery Guide

**Version:** 1.0  
**Purpose:** Step-by-step recovery procedures for framework errors and failures

---

## Recovery Decision Framework

When an error occurs, follow this decision process:

```
Error Detected
    │
    ├─→ Can fix immediately?
    │   └─→ YES: Fix and continue
    │
    ├─→ Need to return to previous phase?
    │   └─→ YES: Go back, fix root cause, retry
    │
    ├─→ Need to switch framework?
    │   └─→ YES: Re-classify, switch framework, restart
    │
    ├─→ Need to escalate layer?
    │   └─→ YES: Escalate to Layer 2 or Layer 3
    │
    └─→ Fundamental problem?
        └─→ YES: Restart from beginning with better context
```

---

## Classification Error Recovery

### Low Confidence After Clarification

**Step-by-Step Recovery:**

1. **Acknowledge Uncertainty**
   - Framework will state: "Confidence is low (X%)"
   - Framework will provide default classification
   - Review default classification

2. **Evaluate Default**
   - Is default reasonable?
   - If yes: Proceed with default
   - If no: Override with explicit specification

3. **Override if Needed**
   ```
   User specifies: [DOMAIN: murata_mhc] [FRAMEWORK: RISE]
   Framework accepts override
   Proceeds with user-specified classification
   ```

4. **Proceed with Caution**
   - Monitor execution closely
   - Verify framework is using correct approach
   - Adjust if needed during execution

### Wrong Classification Selected

**Step-by-Step Recovery:**

1. **Stop Current Execution**
   - Don't continue with wrong classification
   - Correction is more efficient than wrong path

2. **Provide Correct Classification**
   ```
   User: "This should be REPAIR, not CREATION"
   Framework: Re-classifies as REPAIR
   ```

3. **Restart with Correct Classification**
   - Framework selects appropriate framework
   - Proceeds with correct approach

4. **Provide Learning Feedback**
   - Framework records correction
   - Improves future classification accuracy
   - Helps avoid similar mistakes

---

## Framework Execution Error Recovery

### Phase Failure Recovery

**General Procedure:**

1. **Identify Failed Phase**
   - Which phase failed? (RESEARCH, IDENTIFY, SYNTHESIZE, EXECUTE)
   - What was the failure? (error message, invalid output, timeout)

2. **Analyze Root Cause**
   ```
   IF syntax/type error:
       → Fix immediately, re-run phase
   
   ELSE IF missing information:
       → Return to RESEARCH phase
       → Gather missing information
       → Retry from RESEARCH
   
   ELSE IF logic/design error:
       → Return to SYNTHESIZE phase
       → Try alternative approach
       → Retry from SYNTHESIZE
   
   ELSE IF requirements misunderstood:
       → Return to IDENTIFY phase
       → Re-analyze requirements
       → Retry from IDENTIFY
   ```

3. **Fix and Retry**
   - Fix root cause
   - Return to appropriate phase
   - Retry from that phase (don't skip phases)

4. **Monitor Progress**
   - Verify fix resolves issue
   - Check if new issues arise
   - Continue or escalate as needed

### R-I-S-E Phase Failures

#### RESEARCH Phase Failure

**Recovery Steps:**

1. **Identify Missing Information**
   - What information is needed?
   - What sources are missing?

2. **Gather Information**
   - Ask user for specific information
   - Request additional files/context
   - Use alternative information sources

3. **Document Assumptions**
   - If information unavailable, document assumptions
   - Flag assumptions for verification
   - Proceed with reduced confidence

4. **Continue to IDENTIFY**
   - Use available information
   - Note gaps and assumptions
   - Proceed with caution

#### IDENTIFY Phase Failure

**Recovery Steps:**

1. **Return to RESEARCH**
   - May need more information
   - Gather additional context
   - Better understanding needed

2. **Try Alternative Analysis**
   - Break problem into smaller parts
   - Analyze by functional area
   - Look for partial pattern matches

3. **Consider Complexity Re-assessment**
   - Problem may be simpler: Try C-A-R-E
   - Problem may be more complex: Escalate to Layer 2

#### SYNTHESIZE Phase Failure

**Recovery Steps:**

1. **Return to IDENTIFY**
   - Better pattern recognition needed
   - Re-analyze requirements
   - Identify alternative patterns

2. **Try Alternative Approaches**
   - Simplify requirements if possible
   - Relax constraints if acceptable
   - Look for partial solutions

3. **Consider Escalation**
   - May need Layer 2 (Orchestration) for decomposition
   - May need Layer 3 (GENESIS) if truly novel

#### EXECUTE Phase Failure

**Recovery Steps:**

1. **Fix Immediate Issues**
   - Syntax/type errors: Fix and re-verify Layer 1
   - Domain standards violations: Fix and re-verify

2. **Return to Appropriate Phase**
   - Logic errors: Return to SYNTHESIZE
   - Requirements misunderstood: Return to IDENTIFY
   - Missing information: Return to RESEARCH

3. **Re-implement After Fix**
   - Fix root cause first
   - Then re-implement
   - Verify fix resolves issue

### C-A-R-E Iteration Limit Recovery

**When 3 Iterations Completed But Quality Low:**

1. **Analyze Quality Trend**
   ```
   Quality scores: [0.65, 0.68, 0.67]
   Trend: Plateaued (not improving)
   ```

2. **Identify Blocking Issues**
   - What prevents quality improvement?
   - Are issues fixable within C-A-R-E?
   - Is problem more complex than assessed?

3. **Make Recovery Decision**

   ```
   IF quality improving:
       → Extend limit to 5 iterations
       → Continue C-A-R-E
   
   ELSE IF quality plateaued:
       → Escalate to R-I-S-E
       → Re-classify complexity
       → Start at RESEARCH phase
   
   ELSE IF quality declining:
       → Return to ANALYZE phase
       → Try alternative approach
       → Consider escalation if persists
   ```

4. **Execute Recovery**
   - Extend, escalate, or return to ANALYZE
   - Document decision rationale
   - Proceed with chosen path

### HARVEST Quality Threshold Recovery

**When Quality < 95% After 5 Iterations:**

1. **Assess Quality Score**
   ```
   Overall: 87%
   Completeness: 92%
   Accuracy: 95%
   Structure: 83%
   ```

2. **Identify Root Cause**
   - Source material insufficient?
   - Structural issues?
   - Accuracy problems?

3. **Choose Recovery Strategy**

   ```
   IF source material insufficient:
       → Document gaps explicitly
       → Mark incomplete sections
       → Accept partial quality (if > 85%)
       → Note: "Documentation incomplete due to missing sources"
   
   ELSE IF structural issues:
       → Try alternative template
       → Simplify structure
       → Focus on critical sections
   
   ELSE IF accuracy issues:
       → Request user verification
       → Mark uncertain sections
       → Provide source references
   ```

4. **Complete with Documented Gaps**
   - Document all gaps
   - Mark incomplete sections
   - Provide gap analysis
   - Allow user review/editing

---

## Verification Failure Recovery

### Layer-Specific Recovery

#### Layer 1 (Formal) Failure

**Recovery Steps:**

1. **Fix Error Immediately**
   - Syntax errors: Fix syntax
   - Type errors: Fix types
   - Linting violations: Fix violations

2. **Re-run Layer 1**
   - Verify fix resolves error
   - Check for new errors
   - Continue only after Layer 1 passes

3. **If Fix Not Obvious**
   - Review error message carefully
   - Check domain module standards
   - Return to EXECUTE phase if needed

#### Layer 2 (Testing) Failure

**Recovery Steps:**

1. **Identify Failing Tests**
   - List all failing tests
   - Categorize by type

2. **Fix Implementation**
   - Don't just fix tests
   - Fix implementation issues
   - Tests reveal what's wrong

3. **Re-run All Tests**
   - Fix may affect other tests
   - Verify all tests pass
   - Check coverage maintained

#### Layer 3 (Statistical) Failure

**Recovery Steps:**

1. **Measure Regression**
   - Quantify performance/memory issue
   - Compare to baseline

2. **Profile and Optimize**
   - Identify bottlenecks
   - Fix performance issues
   - Fix memory leaks

3. **Verify Fix**
   - Re-run Layer 3 verification
   - Compare to baseline
   - Ensure improvement

#### Layer 4 (Ensemble) Failure

**Recovery Steps:**

1. **Investigate Disagreement**
   - Why do methods disagree?
   - Which is correct?

2. **Fix Underlying Issue**
   - Address root cause
   - Fix implementation

3. **Get Consensus**
   - Re-run ensemble verification
   - Ensure methods agree
   - Get independent re-approval if needed

#### Layer 5 (Human) Failure

**Recovery Steps:**

1. **Document Concerns**
   - List all expert concerns
   - Categorize by severity

2. **Address Concerns**
   - Return to appropriate phase
   - Fix identified issues
   - Get re-approval

3. **Re-verify All Layers**
   - If implementation changed
   - Re-run all verification layers
   - Ensure all layers pass

### Multi-Layer Failure Recovery

**When Multiple Layers Fail:**

1. **Fix Layer 1 First**
   - Foundation must be solid
   - Fix structural issues first
   - Then address other layers

2. **Identify Common Root Cause**
   - Multiple failures may share cause
   - Fix root cause once
   - Re-verify all layers

3. **Escalate if Needed**
   - If fundamental issues: Consider framework switch
   - If requirements wrong: Return to RESEARCH
   - If approach flawed: Return to SYNTHESIZE

---

## When to Restart vs Continue

### Restart from Beginning

**When to Restart:**

1. **Fundamental Misunderstanding**
   - Requirements completely wrong
   - Problem misclassified
   - Wrong framework selected

2. **Context Completely Changed**
   - New information changes everything
   - Problem scope significantly different
   - User pivots to different approach

3. **Multiple Critical Failures**
   - Too many things wrong
   - Easier to start fresh
   - Clean slate needed

**Restart Procedure:**
1. Clear current state
2. Re-classify problem
3. Start framework from beginning
4. Use lessons learned from previous attempt

### Continue from Checkpoint

**When to Continue:**

1. **Partial Progress Made**
   - Some phases completed successfully
   - Can build on completed work
   - Context preserved

2. **Minor Issues**
   - Fixable errors
   - Can resume from previous phase
   - Don't lose completed work

3. **Iterative Improvement**
   - Quality improving
   - On right track
   - Just needs refinement

**Continue Procedure:**
1. Identify last successful phase
2. Fix issues blocking progress
3. Resume from that phase
4. Continue execution

---

## Checkpoint and Resume Procedures

### Creating Checkpoints

**When to Create Checkpoints:**

- Before major phase transitions
- After successful phase completion
- Before risky operations
- Periodically for long-running tasks

**Checkpoint Contents:**
```yaml
checkpoint:
  timestamp: "2025-12-20T14:30:00Z"
  problem_statement: "[Original problem]"
  classification:
    category: "CREATION"
    domain: "web_development"
    framework: "R-I-S-E"
  current_phase: "SYNTHESIZE"
  completed_phases:
    - RESEARCH: "Completed, findings documented"
    - IDENTIFY: "Completed, patterns identified"
  artifacts:
    - research_findings.md
    - requirement_analysis.md
  context: "[Current state]"
```

### Resuming from Checkpoint

**Resume Procedure:**

1. **Load Checkpoint**
   - Restore problem context
   - Load completed artifacts
   - Restore classification

2. **Verify State**
   - Check artifacts are still valid
   - Verify context hasn't changed
   - Confirm resume point is correct

3. **Resume Execution**
   - Continue from checkpoint phase
   - Use preserved context
   - Build on completed work

---

## Escalation Procedures

### When to Escalate Layer

**Layer 1 → Layer 2:**
- Multiple frameworks needed
- Problem decomposition required
- Cross-cutting concerns

**Layer 2 → Layer 3:**
- No framework fits sub-problem
- Framework gap identified
- Novel problem type

**Escalation Steps:**
1. Document why escalation needed
2. Preserve current context
3. Transition to higher layer
4. Continue with appropriate approach

### When to Switch Framework

**R-I-S-E → C-A-R-E:**
- Problem simpler than expected
- Quick iteration sufficient
- Familiar territory

**C-A-R-E → R-I-S-E:**
- Problem more complex than expected
- Research needed
- Root cause unknown

**Framework Switch Steps:**
1. Re-assess problem complexity
2. Select appropriate framework
3. Transfer relevant context
4. Start with appropriate phase

---

## Recovery Checklist

Use this checklist when recovering from errors:

- [ ] Error identified and categorized
- [ ] Root cause analyzed
- [ ] Recovery strategy selected
- [ ] Fix applied (if immediate fix possible)
- [ ] Appropriate phase identified for return
- [ ] Context preserved
- [ ] Recovery action executed
- [ ] Progress verified
- [ ] Error logged for learning

---

## Learning from Errors

### Error Logging

All errors should be logged:

```yaml
error_log:
  timestamp: "2025-12-20T14:30:00Z"
  error_type: "[Classification|Framework|Verification|Domain|System]"
  error_details: "[What went wrong]"
  recovery_action: "[What was done]"
  outcome: "[Success/Failure]"
  lesson: "[What to do differently next time]"
```

### Error Pattern Analysis

**Common Patterns:**
- Classification errors → Improve problem statements
- Framework phase failures → Better context needed
- Verification failures → Implementation quality issues
- Domain conflicts → Explicit domain specification needed

**Prevention:**
- Learn from error patterns
- Improve processes
- Update frameworks
- Enhance documentation

---

## See Also

- [Error Handling Protocol](../frameworks/error_handling_protocol.md) - Comprehensive error handling
- [Troubleshooting Guide](TROUBLESHOOTING.md) - Common issues and solutions
- [Edge Case Handling Guide](edge_case_handling.md) - Edge case protocols

---

**Version:** 1.0  
**Last Updated:** December 2024

