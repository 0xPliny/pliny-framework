# ReAct Integration Framework

> **ReAct = Reasoning + Acting**
> Interleave thinking with actions to dynamically gather information and solve problems.

## Overview

ReAct combines Chain-of-Thought reasoning with the ability to take **external actions** (search, execute code, query APIs, verify facts). Instead of reasoning in isolation, the AI actively gathers information during problem-solving.

```
┌─────────────────────────────────────────────────────────────┐
│                     ReAct Loop                               │
│                                                              │
│   THOUGHT → ACTION → OBSERVATION → THOUGHT → ... → ANSWER   │
│                                                              │
│   "I need to    "Search for    "Found that     "Now I can   │
│    know X"       X docs"        X does Y"       conclude Z" │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

---

## The ReAct Pattern

### Core Loop

```markdown
THOUGHT 1: [What I'm trying to figure out]
ACTION 1: [Action type]: [Action details]
OBSERVATION 1: [What the action revealed]

THOUGHT 2: [Updated reasoning based on observation]
ACTION 2: [Action type]: [Action details]
OBSERVATION 2: [What the action revealed]

... (repeat as needed)

THOUGHT N: [Final reasoning with all gathered information]
ANSWER: [Complete response]
```

---

## Action Types

### 1. SEARCH
Query external knowledge sources.

```markdown
ACTION: SEARCH["MHC crane error code E-1234"]
OBSERVATION: Error E-1234 indicates servo communication timeout. 
             Common causes: cable damage, encoder failure, parameter mismatch.
```

### 2. EXECUTE
Run code to verify or compute.

```markdown
ACTION: EXECUTE[python: calculate_checksum("0x4A2B")]
OBSERVATION: Checksum result: 0x75
```

### 3. VERIFY
Check a fact or assumption.

```markdown
ACTION: VERIFY[Does cc_str support Unicode in MHC systems?]
OBSERVATION: No, cc_str is ASCII-only. Use wide string alternatives for Unicode.
```

### 4. READ
Access specific documentation or code.

```markdown
ACTION: READ[file: src/CraneController.cpp, lines 145-160]
OBSERVATION: [Code content showing the relevant function]
```

### 5. QUERY
Ask for clarification or additional context.

```markdown
ACTION: QUERY[What version of the MHC runtime is being used?]
OBSERVATION: User confirms: MHC Runtime v3.2.1
```

### 6. TEST
Validate a hypothesis.

```markdown
ACTION: TEST[hypothesis: The null pointer occurs when queue is empty]
OBSERVATION: Confirmed - added empty check, error no longer reproduces.
```

---

## ReAct Decision Points

At each THOUGHT, decide:

```
Do I have enough information to proceed?
├── YES → Continue reasoning or provide ANSWER
└── NO → What information do I need?
    │
    ├── Factual knowledge → ACTION: SEARCH
    ├── Code behavior → ACTION: EXECUTE
    ├── Assumption validation → ACTION: VERIFY
    ├── Specific content → ACTION: READ
    ├── User context → ACTION: QUERY
    └── Hypothesis testing → ACTION: TEST
```

---

## Integration with PlinyHub Frameworks

### ReAct + R-I-S-E

```markdown
## RESEARCH (with ReAct)

THOUGHT: I need to understand the current system architecture.
ACTION: READ[architecture_docs/system_overview.md]
OBSERVATION: [Document content]

THOUGHT: The docs mention a "legacy adapter" - I need more details.
ACTION: SEARCH["MHC legacy adapter implementation"]
OBSERVATION: [Search results]

THOUGHT: Now I have enough context to proceed.
[Continue to IDENTIFY phase]

## IDENTIFY (with ReAct)

THOUGHT: I need to verify my assumption about the data flow.
ACTION: VERIFY[Data flows from PLC → Adapter → Database]
OBSERVATION: Partially correct - there's a queue between Adapter and Database.

THOUGHT: I should check the queue implementation.
ACTION: READ[src/DataQueue.cpp]
OBSERVATION: [Code showing queue is bounded, 1000 items max]

[Continue with updated understanding]
```

### ReAct + C-A-R-E

```markdown
## CONTEXT (with ReAct)

THOUGHT: User reports "intermittent timeout errors" - I need specifics.
ACTION: QUERY[When do timeouts occur? Under what load? Which operations?]
OBSERVATION: User says: "During batch imports, after ~500 records"

THOUGHT: This suggests a resource exhaustion issue. Let me check the logs.
ACTION: READ[logs/batch_import_2024-12-20.log]
OBSERVATION: [Log shows connection pool exhausted at record 487]

## ANALYZE (with ReAct)

THOUGHT: Connection pool size might be the issue. What's the current config?
ACTION: READ[config/database.yaml]
OBSERVATION: pool_size: 10, max_overflow: 5

THOUGHT: 15 connections for 500 concurrent operations is insufficient.
[Continue to RESPOND with specific fix]
```

---

## ReAct Execution Rules

### Rule 1: Think Before Acting
Always state THOUGHT before ACTION. Never act blindly.

### Rule 2: One Action at a Time
Execute one action, observe result, then decide next step.

### Rule 3: Limit Action Chains
Maximum 5 actions before synthesizing. If more needed, reassess approach.

### Rule 4: Validate Observations
Don't blindly trust observations. Cross-reference when critical.

### Rule 5: Know When to Stop
If 3 consecutive actions don't advance understanding, step back and reassess.

---

## ReAct Quality Checklist

Before providing final ANSWER:

- [ ] All critical assumptions have been verified (not assumed)
- [ ] Relevant documentation/code has been consulted
- [ ] User context has been clarified where ambiguous
- [ ] Solution has been tested or validated where possible
- [ ] Confidence level reflects the quality of observations

---

## Example: Debugging MHC Communication Error

### Problem
"Crane stops responding after 2 hours of operation"

### ReAct Solution

```markdown
THOUGHT 1: This sounds like a resource leak or timeout issue. 
           I need to understand what "stops responding" means.
ACTION 1: QUERY[Does the crane freeze, throw an error, or disconnect?]
OBSERVATION 1: User says: "No error, just stops accepting commands. 
               Restart fixes it."

THOUGHT 2: No error suggests silent failure. Could be memory leak, 
           connection pool exhaustion, or watchdog timeout. 
           Let me check if there are any logs around the 2-hour mark.
ACTION 2: SEARCH[MHC crane communication timeout after extended operation]
OBSERVATION 2: Known issue in MHC v3.1: Socket connections not properly 
               released in KeepAlive handler. Fixed in v3.2.

THOUGHT 3: Need to verify which version is running.
ACTION 3: QUERY[What MHC runtime version is installed?]
OBSERVATION 3: User confirms: v3.1.4

THOUGHT 4: This matches the known bug. Let me verify the fix exists.
ACTION 4: SEARCH[MHC v3.2 release notes socket fix]
OBSERVATION 4: v3.2.0 release notes: "Fixed socket leak in KeepAlive 
               handler that caused communication failures after 
               prolonged operation."

THOUGHT 5: Root cause identified. Solution is version upgrade.
           Let me check if there are workarounds for v3.1.
ACTION 5: SEARCH[MHC v3.1 socket leak workaround]
OBSERVATION 5: Workaround: Add manual socket cleanup call every 
               30 minutes using SocketManager.ForceCleanup()

ANSWER:
## Root Cause
Known socket leak in MHC v3.1.x KeepAlive handler. Connections 
accumulate until system becomes unresponsive (~2 hours at normal load).

## Solution (Recommended)
Upgrade to MHC Runtime v3.2.0 or later.

## Workaround (If upgrade not immediately possible)
Add periodic cleanup to your main loop:

```cpp
// Add to main operation loop
static int cleanupCounter = 0;
if (++cleanupCounter >= 1800) { // Every 30 minutes at 1 Hz
    SocketManager::ForceCleanup();
    cleanupCounter = 0;
    cs_log_printf("Socket cleanup performed");
}
```

## Confidence: 9/10
High confidence - matches known documented issue with confirmed fix.
```

---

## Template

```markdown
# ReAct Analysis: [Problem Name]

## Initial Problem
[Problem statement]

---

THOUGHT 1: [Initial reasoning]
ACTION 1: [TYPE][Details]
OBSERVATION 1: [Result]

THOUGHT 2: [Updated reasoning]
ACTION 2: [TYPE][Details]
OBSERVATION 2: [Result]

[Continue as needed...]

---

## ANSWER

### Summary
[Brief answer]

### Details
[Full explanation]

### Evidence
[Key observations that support the answer]

### Confidence
Score: [1-10]
Rationale: [Based on quality/quantity of observations]
```

---

## When NOT to Use ReAct

| Situation | Better Approach |
|-----------|-----------------|
| Simple, well-defined tasks | Direct response or C-A-R-E |
| Pure reasoning (no external data needed) | Chain-of-Thought |
| Creative/generative tasks | R-I-S-E without actions |
| User has provided all context | Standard framework |

Use ReAct when you **need information you don't have** to solve the problem correctly.
