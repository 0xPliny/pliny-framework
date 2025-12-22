# R-I-S-E Template: Feature Development

Use this template when **building a new feature** in any domain.

---

## Metadata

```yaml
framework: R-I-S-E
use_case: feature-development
category: CREATION
estimated_time: 1-4 hours
domain: "[DOMAIN]"  # web_development, murata_mhc, python_data, etc.
```

---

## Phase 1: RESEARCH

### What do I already know?

- [ ] Requirements are clear
- [ ]

### What don't I know?

- [ ]

### What do I need to find out?

- [ ]

### Relevant past learnings

```
pliny learn apply "[brief problem description]"
```

-

### Research Checklist

- [ ] Requirements understood
- [ ] Constraints identified
- [ ] Prior art reviewed
- [ ] Relevant learnings loaded

---

## Phase 2: IDENTIFY

### Requirements

| Requirement | Type | Priority | Source |
|-------------|------|----------|--------|
| | Functional | Must | |
| | Functional | Should | |
| | Non-functional | Must | |

### Patterns to Apply

- [ ] Pattern:
  - Why:
- [ ] Pattern:
  - Why:

### Risks & Mitigation

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| | | | |

### Alternative Approaches

1. **Approach A:**
   - Pros:
   - Cons:
2. **Approach B:**
   - Pros:
   - Cons:

**Selected:** Approach ___because___

---

## Phase 3: SYNTHESIZE

### Architecture

```
[Draw or describe component structure]
```

### Files to Create/Modify

| File | Action | Purpose |
|------|--------|---------|
| | Create | |
| | Modify | |

### Implementation Order

1.
2.
3.

### Dependencies

- Before I start:
- Blocking others:

---

## Phase 4: EXECUTE

### Domain Standards

```bash
pliny module load [domain]
```

**Key standards to follow:**

- [ ] Standard 1:
- [ ] Standard 2:
- [ ] Standard 3:

### Implementation Notes

#### Step 1: [Name]

```
[Code or description]
```

#### Step 2: [Name]

```
[Code or description]
```

#### Step 3: [Name]

```
[Code or description]
```

### Verify Each Step

- [ ] Step 1 complete and working
- [ ] Step 2 complete and working
- [ ] Step 3 complete and working

---

## Verification

```bash
pliny verify [file] --domain [domain]
```

### Layer 1 (Formal)

- [ ] Compiles/lints without errors

### Layer 2 (Testing)

- [ ] Tests added
- [ ] All tests pass

### Layer 3 (Quality)

- [ ] Standards followed
- [ ] Performance acceptable

---

## OMEGA Learning Capture

**What worked well:**
-

**What didn't work:**
-

**Patterns discovered:**
-

**Add to knowledge base:**

```bash
pliny omega learn
```
