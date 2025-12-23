# Troubleshooting Guide

**Version:** 1.0  
**Purpose:** Common issues and solutions for Pliny Framework usage

---

## Quick Problem Resolution

| Problem | Quick Solution | Detailed Guide |
|---------|---------------|----------------|
| Classification keeps failing | See [Classification Issues](#classification-issues) | Section below |
| Framework stuck in loop | See [Framework Execution Issues](#framework-execution-issues) | Section below |
| Verification keeps failing | See [Verification Failures](#verification-failures) | Section below |
| Domain module not loading | See [Domain Module Issues](#domain-module-issues) | Section below |
| Low confidence warnings | See [Confidence Issues](#confidence-issues) | Section below |

---

## Classification Issues

### Problem: Classification Confidence Always Low

**Symptoms:**
- Classification confidence consistently < 0.7
- Framework asks for clarification repeatedly
- Default classifications being used

**Possible Causes:**
1. Problem statement is vague or ambiguous
2. Domain signals are weak or conflicting
3. Problem spans multiple categories

**Solutions:**

1. **Provide More Context**
   - Include relevant file paths
   - Mention specific technologies or domains
   - Describe the actual goal, not just the action

   **Bad:** "Fix this"  
   **Good:** "Fix the GP.BAD error in SR01 store command when processing crane requests"

2. **Use Explicit Domain Hints**
   - Add `[DOMAIN: murata_mhc]` to your request
   - Or include domain-specific keywords (cc_str, React, pandas, etc.)

3. **Specify Framework Explicitly**
   - Add `[FRAMEWORK: RISE]` or `[FRAMEWORK: CARE]` or `[FRAMEWORK: HARVEST]`
   - Override automatic selection if you know what you need

4. **Break Down Complex Problems**
   - Split multi-part requests into separate problems
   - Handle dependencies explicitly

### Problem: Wrong Classification Selected

**Symptoms:**
- Framework selected doesn't match problem
- Execution feels wrong (too thorough or not thorough enough)

**Solutions:**

1. **Override Classification**
   - Explicitly specify: `[DOMAIN: X] [FRAMEWORK: Y]`
   - Framework will use your specification

2. **Provide Correction Feedback**
   - Tell framework the correct classification
   - Framework will learn from correction (if learning enabled)

3. **Re-state Problem More Clearly**
   - Use category signal words:
     - CREATION: create, build, implement, design
     - TRANSFORMATION: convert, migrate, refactor, port
     - UNDERSTANDING: explain, analyze, document
     - REPAIR: fix, debug, error, broken
     - OPTIMIZATION: optimize, improve, enhance

### Problem: Multiple Domains Detected

**Symptoms:**
- Framework asks which domain is primary
- Conflicts between domain standards

**Solutions:**

1. **Specify Primary Domain**
   - Use `[DOMAIN: primary_domain]` syntax
   - Framework will use your specification

2. **Let Framework Choose**
   - Framework uses "where core logic lives" heuristic
   - Usually correct, but you can override

3. **Use Multi-Domain Orchestration**
   - For complex multi-domain tasks
   - See [Multi-Domain Orchestration](../core/multi_domain_orchestration.md)

---

## Framework Execution Issues

### Problem: R-I-S-E Stuck in RESEARCH Phase

**Symptoms:**
- Research phase takes too long
- Keeps asking for more information
- Never progresses to IDENTIFY

**Solutions:**

1. **Provide Missing Information**
   - Answer framework's questions directly
   - Provide context files if available

2. **Allow Framework to Proceed with Assumptions**
   - Framework can document assumptions
   - Continue with documented gaps
   - Flag for verification later

3. **Simplify Problem**
   - Break into smaller problems
   - Focus on one aspect at a time

### Problem: C-A-R-E Exceeding Iteration Limit

**Symptoms:**
- C-A-R-E completes 3 iterations but quality still low
- Framework escalates to R-I-S-E
- Feels like over-engineering

**Solutions:**

1. **Check if Problem Was Misclassified**
   - If problem is actually complex, R-I-S-E escalation is correct
   - Accept escalation to more thorough framework

2. **Provide Better Initial Context**
   - C-A-R-E needs good initial state
   - Provide clear current state and goal
   - Reduce ambiguity

3. **Simplify Requirements**
   - Complex requirements may need R-I-S-E
   - Break into smaller C-A-R-E problems if possible

### Problem: HARVEST Quality Below Threshold

**Symptoms:**
- HARVEST completes 5 iterations but quality < 95%
- Documentation has gaps
- Source material seems insufficient

**Solutions:**

1. **Provide More Source Material**
   - Include all relevant files
   - Add existing documentation (even if outdated)
   - Include configuration files, schemas, etc.

2. **Accept Partial Quality**
   - Quality > 85% is acceptable with documented gaps
   - Review and edit documentation manually
   - Fill gaps in follow-up iteration

3. **Check Source Material Quality**
   - If source code is poorly documented, documentation will reflect that
   - Improve source code documentation first
   - Then re-run HARVEST

### Problem: Framework Phase Keeps Failing

**Symptoms:**
- Same phase fails repeatedly
- Error messages don't help
- No progress made

**Solutions:**

1. **Check Error Messages Carefully**
   - Error messages usually indicate root cause
   - Look for specific failure points
   - Address root cause, not symptoms

2. **Return to Previous Phase**
   - Phase failures often indicate previous phase issues
   - Go back and fix root cause
   - Then retry failing phase

3. **Switch Framework or Escalate**
   - If framework fundamentally wrong: Switch to different framework
   - If problem too complex: Escalate to Layer 2 (Orchestration)
   - See [Error Handling Protocol](../frameworks/error_handling_protocol.md)

---

## Verification Failures

### Problem: Layer 1 (Formal) Keeps Failing

**Symptoms:**
- Type errors, syntax errors, linting violations
- Fix one error, another appears
- Compilation/parsing fails

**Solutions:**

1. **Fix Errors Sequentially**
   - Fix first error, re-run
   - Don't try to fix all at once
   - Errors may cascade

2. **Check Domain Standards**
   - Verify domain module is loaded correctly
   - Check if standards are being applied
   - Review domain module requirements

3. **Verify File Context**
   - Ensure all referenced files are available
   - Check import paths are correct
   - Verify dependencies are installed

### Problem: Layer 2 (Testing) Failures

**Symptoms:**
- Tests failing
- Coverage below threshold
- Can't write tests for code

**Solutions:**

1. **Fix Implementation Based on Test Failures**
   - Tests reveal what's wrong with implementation
   - Fix implementation, don't just fix tests
   - Re-run tests after fixes

2. **Add Missing Tests**
   - Identify untested code paths
   - Add tests for critical functionality
   - Focus on edge cases and error paths

3. **Review Test Quality**
   - Ensure tests are actually testing functionality
   - Check test assertions are correct
   - Verify test data is appropriate

### Problem: Layer 3 (Statistical) Failures

**Symptoms:**
- Performance regressions
- Memory issues
- Coverage dropped

**Solutions:**

1. **Profile and Optimize**
   - Use profiling tools to identify bottlenecks
   - Optimize hot paths
   - Verify improvements with benchmarks

2. **Fix Resource Management**
   - Identify memory leaks
   - Fix resource cleanup
   - Verify with memory profiling

3. **Maintain Test Coverage**
   - Add tests for new code
   - Don't remove existing tests
   - Monitor coverage trends

### Problem: Layer 4 (Ensemble) Failures

**Symptoms:**
- Multiple methods disagree
- Independent review finds issues
- Invariants violated

**Solutions:**

1. **Investigate Disagreement**
   - Understand why methods disagree
   - Determine which is correct
   - Fix underlying issue

2. **Address Review Concerns**
   - Take review feedback seriously
   - Fix identified issues
   - Get re-approval

3. **Verify Invariants**
   - Understand what invariants should hold
   - Fix violations
   - Add invariant checks if missing

### Problem: Layer 5 (Human) Rejection

**Symptoms:**
- Expert review rejects solution
- Design concerns raised
- UX or business logic issues

**Solutions:**

1. **Address Concerns Directly**
   - Don't dismiss expert feedback
   - Understand the concern
   - Fix the root issue

2. **Return to Design Phase**
   - May need to return to SYNTHESIZE phase
   - Consider alternative designs
   - Get design approval before re-implementing

3. **Clarify Requirements**
   - May need to return to RESEARCH or IDENTIFY
   - Verify understanding of requirements
   - Get domain expert confirmation

---

## Domain Module Issues

### Problem: Domain Module Not Loading

**Symptoms:**
- Framework uses general_reasoning domain
- Domain-specific standards not applied
- Warning about domain detection

**Solutions:**

1. **Check Domain Signals**
   - Include file extensions (.vb, .tsx, .py, etc.)
   - Use domain keywords (cc_str, React, pandas, etc.)
   - Provide context paths if available

2. **Explicitly Specify Domain**
   - Use `[DOMAIN: murata_mhc]` syntax
   - Framework will use your specification
   - Overrides auto-detection

3. **Verify Module Exists**
   - Check modules/ directory for available modules
   - Module name must match exactly
   - Create custom module if needed (use template)

### Problem: Domain Standards Not Applied

**Symptoms:**
- Code doesn't follow domain standards
- Quality gates not checking domain rules
- Framework seems to ignore domain module

**Solutions:**

1. **Verify Module Loaded**
   - Check framework output for domain confirmation
   - Should see domain name in classification output
   - If not, explicitly specify domain

2. **Check Module Format**
   - Verify module YAML is valid
   - Check standards section exists
   - Ensure quality_gates are defined

3. **Review Standards Application**
   - Framework applies standards during EXECUTE phase
   - Check if you're at correct phase
   - Standards may be in verification phase

### Problem: Standards Conflict Between Domains

**Symptoms:**
- Multiple domains detected
- Conflicting standards
- Framework asks for resolution

**Solutions:**

1. **Specify Primary Domain**
   - Use `[DOMAIN: primary_domain]` to set primary
   - Framework will prioritize primary domain standards
   - See [Multi-Domain Orchestration](../core/multi_domain_orchestration.md)

2. **Review Conflict Resolution Rules**
   - Data format: Primary domain wins
   - Code style: Primary domain wins
   - Naming: Primary internally, secondary at boundaries
   - Errors: Map at boundaries

3. **Create Boundary Mappings**
   - Document how standards map at boundaries
   - Use explicit conversion functions
   - See conflict resolution protocol

---

## Learning and Knowledge Base Issues

### Problem: Learnings Not Being Retrieved

**Symptoms:**
- Framework doesn't seem to learn from past problems
- Similar problems handled differently each time
- No prior knowledge applied

**Solutions:**

1. **Check Knowledge Base Status**
   - Verify knowledge base is accessible
   - Check if learnings are being persisted
   - Ensure OMEGA Loop learning is enabled

2. **Verify Learning Retrieval**
   - Learnings retrieved during OMEGA.OBSERVE phase
   - Check if problem signature matches stored learnings
   - Similar problems should surface relevant learnings

3. **Manual Learning Import**
   - If using manual learning files, ensure they're loaded
   - Check learning file format is correct
   - Verify learning records are valid YAML

### Problem: Wrong Learnings Applied

**Symptoms:**
- Framework applies irrelevant learnings
- Past solutions don't fit current problem
- Learnings seem outdated

**Solutions:**

1. **Review Learning Relevance**
   - Check if learning actually applies to current problem
   - Problem signatures should match closely
   - Domain and category should align

2. **Update or Remove Learnings**
   - Remove outdated or incorrect learnings
   - Update learnings if patterns changed
   - Curate learning base regularly

3. **Provide Correction**
   - Correct framework when wrong learning applied
   - Framework will learn from correction
   - Update learning base accordingly

---

## Confidence Issues

### Problem: Confidence Always Low

**Symptoms:**
- Confidence scores consistently < 0.7
- Framework keeps asking for clarification
- Uncertainty warnings frequent

**Solutions:**

1. **Provide More Information**
   - Include context files
   - Specify domain explicitly
   - Use clear, specific problem statements

2. **Accept Low Confidence if Appropriate**
   - Some problems are genuinely uncertain
   - Framework will proceed with defaults
   - You can override if needed

3. **Check if Problem is Well-Defined**
   - Vague problems lead to low confidence
   - Define problem more precisely
   - Break into smaller, clearer problems

### Problem: Confidence Seems Incorrect

**Symptoms:**
- High confidence but solution is wrong
- Low confidence but solution is correct
- Confidence doesn't match actual certainty

**Solutions:**

1. **Calibration Takes Time**
   - Confidence calibration improves with feedback
   - Provide corrections when confidence is wrong
   - Framework will learn to calibrate better

2. **Review Confidence Factors**
   - Confidence based on: documentation, code inspection, testing, etc.
   - If factors are weak, confidence should be lower
   - Verify confidence factors are appropriate

3. **Provide Feedback**
   - Tell framework when confidence assessment is wrong
   - Framework will adjust calibration
   - Helps improve future confidence scoring

---

## Performance Issues

### Problem: Framework Execution Takes Too Long

**Symptoms:**
- Framework phases take excessive time
- Research phase never completes
   - Verification runs slowly

**Solutions:**

1. **Check Problem Complexity**
   - Complex problems take longer
   - Consider breaking into smaller problems
   - Use appropriate framework (C-A-R-E for simple, R-I-S-E for complex)

2. **Provide Better Initial Context**
   - More context = less research needed
   - Include relevant files upfront
   - Reduce ambiguity in problem statement

3. **Use Appropriate Verification Intensity**
   - Trivial changes: Layer 1 only
   - Simple changes: Layers 1-2
   - Don't use full 5-layer verification for simple fixes

### Problem: Resource Exhaustion

**Symptoms:**
- Timeout errors
- Memory issues
- Framework stops responding

**Solutions:**

1. **Simplify Problem**
   - Break into smaller sub-problems
   - Handle dependencies explicitly
   - Use Layer 2 orchestration for complex problems

2. **Check Resource Limits**
   - Verify timeout settings are appropriate
   - Check memory limits
   - Adjust limits if needed

3. **Use Checkpoint/Resume**
   - Save state periodically
   - Resume from checkpoint if timeout
   - Divide work into smaller sessions

---

## Getting Help

### When to Escalate

Escalate to framework maintainers when:

1. **Framework Bug**
   - Framework produces incorrect output
   - Error handling doesn't work
   - Framework gets stuck in loop

2. **Documentation Issues**
   - Documentation is unclear or incorrect
   - Missing information
   - Examples don't work

3. **Feature Requests**
   - Need new domain module
   - Want new framework feature
   - Request framework enhancement

### Reporting Issues

When reporting issues, include:

1. **Problem Description**
   - What you were trying to do
   - What went wrong
   - Expected vs actual behavior

2. **Context**
   - Problem statement you used
   - Domain and framework selected
   - Classification results

3. **Error Information**
   - Error messages
   - Framework output
   - Verification results (if applicable)

4. **Environment**
   - Framework version
   - Domain modules in use
   - Any custom configurations

---

## See Also

- [Error Handling Protocol](../frameworks/error_handling_protocol.md) - Comprehensive error handling
- [Error Recovery Guide](ERROR_RECOVERY.md) - Step-by-step recovery procedures
- [Edge Case Handling Guide](edge_case_handling.md) - Edge case protocols
- [Problem Classifier](../frameworks/problem_classifier.md) - Classification troubleshooting
- [Verification Framework](../frameworks/verification_framework.md) - Verification troubleshooting

---

**Version:** 1.0  
**Last Updated:** December 2024

