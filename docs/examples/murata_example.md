# Example: Solving a Murata MHC Problem with PlinyHub

This walkthrough demonstrates using PlinyHub to solve a real Murata MHC problem from start to finish.

---

## The Problem

> "The Aurora AS/RS crane is assigning pallets to incorrect storage locations when the location type doesn't match the pallet type. We need to fix the allocation logic."

---

## Step 1: CLASSIFY

Let's run the problem through the classifier:

```bash
pliny classify "Fix Aurora crane pallet allocation to wrong location types"
```

**Results:**

```
Category:   REPAIR            Confidence: 94%
Domain:     murata_mhc        Confidence: 97%
Framework:  C-A-R-E           Confidence: 88%
Complexity: moderate          Confidence: 75%

Rationale: 
- "Fix" signals REPAIR category
- "Aurora", "crane", "pallet" signal murata_mhc domain
- Bug fix with known location → C-A-R-E for fast iteration
```

**Decision:** Use C-A-R-E with murata_mhc domain module.

---

## Step 2: Load Domain Module

```bash
pliny module load murata_mhc
```

Now we have these standards enforced:

- Use `cc_str` for string operations
- Use generated classes for database access
- Use `cs_log_printf` for logging
- Return `GP.GOOD` / `GP.BAD` / `SQL.HELD`

---

## Step 3: Execute C-A-R-E Framework

### Phase 1: CONTEXT

**What's the current state?**

- Aurora crane allocates pallets to storage locations
- Problem: Location type not checked against pallet type
- Result: Wrong allocations causing downstream issues

**What's the goal?**

- Allocation should only succeed when `pallet.type == location.type`
- Mismatches should be rejected with appropriate logging

**What files are involved?**

- `D:\ICIS\Aurora\Dispatcher\CraneAllocator.cpp`
- `D:\ICIS\Aurora\Common\z_locations.h` (generated class)
- `D:\ICIS\Aurora\Common\z_pallets.h` (generated class)

**Prior context loaded:**

- Past learning: "Always validate types before allocation" (from similar bug 6 months ago)

---

### Phase 2: ANALYZE

**Break down the task:**

1. Find the allocation function in CraneAllocator.cpp
2. Identify where pallet is matched to location
3. Add type validation before confirming allocation
4. Add cs_log_printf for rejection cases
5. Test with different pallet/location type combinations

**Approach:**

- Add validation check using generated class methods
- Early return with GP.BAD if types don't match
- Minimal change to reduce regression risk

**Estimated steps:** 3-4

---

### Phase 3: RESPOND

**Implementation:**

```cpp
// CmL 12/20/2025: Added type validation for pallet-location match

int CraneAllocator::AllocatePallet(int nPalletId, int nLocationId)
{
    cs_log_printf(LOG_INFO, "CraneAllocator: Allocating pallet %d to location %d", 
                  nPalletId, nLocationId);
    
    // Load pallet using generated class
    z_pallets pallet;
    pallet.pallet_id = nPalletId;
    if (pallet.load_by_pk() != SQL_GOOD)
    {
        cs_log_printf(LOG_ERROR, "CraneAllocator: Failed to load pallet %d", nPalletId);
        return GP.BAD;
    }
    
    // Load location using generated class
    z_locations location;
    location.location_id = nLocationId;
    if (location.load_by_pk() != SQL_GOOD)
    {
        cs_log_printf(LOG_ERROR, "CraneAllocator: Failed to load location %d", nLocationId);
        return GP.BAD;
    }
    
    // CmL 12/20/2025: NEW - Validate type match before allocation
    if (cc_str.comp(pallet.pallet_type, location.location_type) != 0)
    {
        cs_log_printf(LOG_WARN, 
            "CraneAllocator: Type mismatch - pallet type '%s' != location type '%s'",
            pallet.pallet_type.c_str(), location.location_type.c_str());
        return GP.BAD;
    }
    
    // Proceed with allocation
    location.assigned_pallet = nPalletId;
    location.status = LOC_STATUS_RESERVED;
    
    if (location.update() != SQL_GOOD)
    {
        cs_log_printf(LOG_ERROR, "CraneAllocator: Failed to update location %d", nLocationId);
        return GP.BAD;
    }
    
    cs_log_printf(LOG_INFO, "CraneAllocator: Successfully allocated pallet %d to location %d", 
                  nPalletId, nLocationId);
    return GP.GOOD;
}
```

**Standards applied:**

- ✅ Used `z_pallets` and `z_locations` generated classes
- ✅ Used `cc_str.comp()` for string comparison
- ✅ Used `cs_log_printf` with appropriate LOG levels
- ✅ Returns `GP.GOOD` / `GP.BAD`
- ✅ CmL branding with date

---

### Phase 4: EVALUATE

**Standards Check:**

```bash
pliny check CraneAllocator.cpp --domain murata_mhc
```

Results:

```
✓ MHC-REQ-001: cc_str used for strings
✓ MHC-REQ-002: Generated classes for database
✓ MHC-REQ-003: cs_log_printf for logging
✓ MHC-REQ-005: Standard return codes

All standards passed ✓
```

**Testing:**

```
Test 1: Pallet type "A" → Location type "A" → PASS (GP.GOOD)
Test 2: Pallet type "A" → Location type "B" → PASS (GP.BAD, logged warning)
Test 3: Invalid pallet ID → PASS (GP.BAD, logged error)
Test 4: Invalid location ID → PASS (GP.BAD, logged error)
```

**Quality Score:** 0.96 (completeness: 0.98, accuracy: 0.97, consistency: 0.93)

**Decision:** COMPLETE ✓ (Quality > 0.95 threshold)

---

## Step 4: OMEGA Learn

Captured learnings:

```yaml
learning_record:
  session_id: "550e8400-e29b-41d4-a716-446655440000"
  timestamp: "2025-12-20T20:00:00Z"
  
  problem_category: "REPAIR"
  domain: "murata_mhc"
  framework_used: "C-A-R-E"
  
  successful_patterns:
    - pattern: "Type Validation Before Assignment"
      description: "Always validate types match before any assignment operation"
      reuse_conditions: "Any pallet/location/bin allocation"
  
  quality_achieved:
    completeness: 0.98
    accuracy: 0.97
    consistency: 0.93
    overall: 0.96
  
  iterations_needed: 1
  time_to_solution: 25  # minutes
```

---

## Summary

| Phase | Action | Time |
|-------|--------|------|
| CLASSIFY | Identified as REPAIR in murata_mhc | 1 min |
| CONTEXT | Loaded state, understood goal | 5 min |
| ANALYZE | Broke down into 5 steps | 3 min |
| RESPOND | Implemented with Murata standards | 12 min |
| EVALUATE | Tested, passed all checks | 4 min |

**Total Time:** 25 minutes
**Quality Score:** 96%
**Iterations:** 1

---

## Key Takeaways

1. **C-A-R-E is fast for familiar bug fixes** - Single iteration when problem is well-understood
2. **Domain module catches standards early** - Murata standards enforced during development
3. **Logging is essential** - `cs_log_printf` made debugging clear
4. **Generated classes prevent SQL errors** - No raw SQL means no SQL injection or typos
