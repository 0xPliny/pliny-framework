# Knowledge Transfer Patterns

**Version:** 1.0
**Purpose:** Apply learnings from solved problems to new problems

---

## Overview

Knowledge Transfer enables **cross-domain learning**—applying what works in one context to different contexts. This prevents reinventing solutions and accelerates problem-solving.

```
┌─────────────────┐       ┌─────────────────┐
│  Past Problem   │       │  New Problem    │
│  (Solved)       │       │  (Unsolved)     │
└────────┬────────┘       └────────┬────────┘
         │                         │
         ▼                         ▼
┌─────────────────────────────────────────────┐
│         KNOWLEDGE TRANSFER ENGINE           │
├─────────────────────────────────────────────┤
│                                             │
│  1. ABSTRACTION    Extract general pattern  │
│  2. MAPPING        Map concepts across      │
│  3. ADAPTATION     Adjust for new context   │
│  4. VERIFICATION   Confirm transfer valid   │
│                                             │
└─────────────────────────────────────────────┘
         │
         ▼
┌─────────────────┐
│  Solution for   │
│  New Problem    │
└─────────────────┘
```

---

## Pattern 1: Analogical Reasoning

**Use when:** Facing a new problem that reminds you of something you've solved before

### Process

1. **Identify Structural Similarity**

   ```
   Past Problem: "Optimize database queries for faster page load"
   New Problem: "Optimize API calls for faster mobile response"
   
   Similarity: Both are "reduce latency by minimizing external calls"
   ```

2. **Map Concepts**

   ```
   Past → New:
   ├── database queries → API calls
   ├── query batching → request batching  
   ├── caching results → caching responses
   └── indexing → endpoint optimization
   ```

3. **Apply Mapped Solution**

   ```
   Past Solution: "Batch queries, add caching, create indexes"
   
   Transferred: "Batch API calls, add response caching, optimize endpoints"
   ```

4. **Verify Mapping Validity**
   - Does the mapping preserve essential relationships?
   - Are there important differences that invalidate transfer?
   - Does the transferred solution actually work?

### When It Works

- Problems share underlying structure
- Solutions are not deeply domain-specific
- Key abstractions transfer cleanly

### When It Fails

- Surface similarity hides deep differences
- Critical constraints don't map
- Domain-specific factors are central

---

## Pattern 2: Abstraction Ladder

**Use when:** A solution seems domain-specific but might generalize

### Process

1. **Climb the Ladder (Specific → Abstract)**

   ```
   Level 0 (Specific): "Add cc_str.copy() for Murata string handling"
   Level 1 (More Abstract): "Use domain-specific safe string operations"
   Level 2 (Abstract): "Use safe type operations instead of raw operations"
   Level 3 (Universal): "Prefer safe, encapsulated operations over raw primitives"
   ```

2. **Find the Universal Principle**

   ```
   Principle: "Encapsulated operations are safer and more maintainable 
              than raw primitive operations"
   ```

3. **Descend to New Domain**

   ```
   Domain: Web Development (TypeScript)
   
   Level 3: "Prefer safe, encapsulated operations"
   Level 2: "Use type-safe operations"
   Level 1: "Use domain-specific type patterns"
   Level 0: "Use branded types for IDs, use Result types for errors"
   ```

4. **Apply Instantiated Principle**

   ```
   Web Solution: "Instead of raw strings for userIds, use branded types:
                  type UserId = string & { readonly _brand: 'UserId' }"
   ```

### The Ladder

```
        ABSTRACT
           △
           │  "Always encapsulate for safety"
           │
           │  "Use domain-safe types"
           │
           │  "Use cc_str library functions"
           ▼
        CONCRETE
```

---

## Pattern 3: Failure Analysis Transfer

**Use when:** Previous attempts failed and you want to avoid the same mistakes

### Process

1. **Document What Didn't Work**

   ```yaml
   failed_approach:
     problem: "Speed up report generation"
     attempted: "Parallelize database queries"
     result: "Deadlocks and worse performance"
     root_cause: "Database locking on writes during reads"
   ```

2. **Extract Anti-Pattern**

   ```yaml
   anti_pattern:
     name: "Naive Parallelization"
     description: "Parallelizing operations without checking for shared state"
     applies_when: "Operations share mutable resources"
     better_approach: "Serialize, queue, or partition shared resources"
   ```

3. **Check New Problem for Anti-Pattern**

   ```
   New Problem: "Speed up image processing pipeline"
   
   Check: Does naive parallelization apply?
   ├── Shared resources? → File system, memory
   ├── Mutable state? → Output files, counters
   └── Risk of conflict? → Yes
   
   → Don't naively parallelize, use proper queue/partition
   ```

4. **Apply Lesson Learned**

   ```
   Solution: "Use work queue with dedicated workers, 
             partition output to separate directories"
   ```

---

## Pattern 4: Solution Templates

**Use when:** You recognize a well-known problem category

### Process

1. **Classify Problem Category**

   ```
   Known Categories:
   ├── Caching (key-value with expiration)
   ├── Rate Limiting (token bucket, sliding window)
   ├── Pagination (offset, cursor, keyset)
   ├── Error Handling (retry, circuit breaker, fallback)
   ├── State Machine (transitions, guards, actions)
   └── Producer-Consumer (queue, workers)
   ```

2. **Retrieve Template Solution**

   ```yaml
   category: rate_limiting
   template: token_bucket
   components:
     - bucket_capacity: "[configurable max tokens]"
     - refill_rate: "[tokens per second]"
     - consume_tokens: "[function to deduct tokens]"
     - check_available: "[function to verify quota]"
   ```

3. **Instantiate for Context**

   ```
   Problem: "Limit API requests per user"
   
   Instantiated:
   ├── bucket_capacity: 100 requests
   ├── refill_rate: 10 per minute
   ├── consume_tokens: Called on each request
   └── check_available: Returns 429 if depleted
   ```

---

## Pattern 5: Cross-Domain Concept Mapping

**Use when:** Domains seem unrelated but share deep structure

### Examples

| Source Domain | Target Domain | Shared Concept |
|---------------|---------------|----------------|
| Version Control (Git) | Document Editing | Branching, merging, conflict resolution |
| Manufacturing (Kanban) | Software Development | Work-in-progress limits, flow optimization |
| Electrical Circuits | Software Systems | Load balancing, circuit breakers, backpressure |
| Biological Systems | Distributed Systems | Redundancy, self-healing, evolution |

### Process

1. Model source domain solution
2. Identify abstract structure
3. Find corresponding structures in target domain
4. Map and adapt

---

## Knowledge Base Structure

Store solved problems for future reference:

```yaml
# knowledge_base/rate_limiting_api.yaml
problem:
  category: rate_limiting
  context: API gateway
  constraints: [high traffic, per-user limits]

solution:
  approach: sliding_window_log
  implementation: Redis sorted sets for request timestamps
  trade_offs: Memory for precision

learnings:
  - "Fixed window causes boundary bursts"
  - "Token bucket simpler but less fair"
  - "Sliding log most accurate but memory-heavy"

transferable_to:
  - "Any per-entity limiting scenario"
  - "Quota enforcement systems"
  - "Traffic shaping"
```

---

## When Transfer Fails

### Signs of Invalid Transfer

- Mapped solution doesn't fit constraints
- Essential elements have no analog
- Transferred solution feels forced
- Domain experts say "that's not how it works here"

### Recovery

1. Return to R-I-S-E Research phase
2. Understand new domain on its own terms
3. Generate native solution
4. Document why transfer failed for future reference

---

## Quick Reference

```
ANALOGICAL:   Similar structure? Map concepts, apply solution.
ABSTRACTION:  Climb to principle, descend to new domain.
FAILURE:      What failed before? Don't repeat it.
TEMPLATE:     Known category? Use established pattern.
CROSS-DOMAIN: Deep structure match? Adapt the metaphor.
```

**Remember:** Transfer is a hypothesis. Always verify it works in the new context.
