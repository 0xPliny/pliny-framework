---
description: Inject cross-references throughout MHC-Developers-Guide using HARVEST methodology
---

# Inject Cross-References in MHC-Developers-Guide

## Prerequisites

- Repository cloned locally
- Understanding of section relationships

## Steps

### 1. Harvest - Collect Relationship Data

// turbo

```bash
cd MHC-Developers-Guide
# Find all section references
grep -rh "Section [0-9]" --include="*.md" | sort | uniq -c | sort -rn | head -20
```

### 2. Analyze - Map Relationships

Create a relationship matrix:

| Section | Should Reference |
|---------|-----------------|
| 02_Coding_Standards | 04_Implementation_Patterns, 06_Testing |
| 04_Implementation_Patterns | 02_Coding_Standards, 06_Testing, 01_Architecture |
| 05_Build_and_Deployment | 00_Environment_Setup, 06_Testing |
| 06_Testing | 02_Coding_Standards, 04_Implementation_Patterns |

### 3. Restructure - Create Reference Template

Standard "Related Documentation" section format:

```markdown
---

## Related Documentation

### Processes
- [Implementation Patterns](../04_Implementation_Patterns/) - Design patterns used
- [Coding Standards](../02_Coding_Standards/) - Required coding conventions

### Technical Reference
- [System Architecture](../01_System_Architecture/) - Overall system design
- [Database Reference](../07_Database_Reference/) - Data structures

### Troubleshooting
- [Testing & Debugging](../06_Testing_and_Debugging/) - Debug procedures
```

### 4. Verify - Check Link Validity

// turbo

```bash
# Find potentially broken relative links
grep -r "\.\./[0-9]" --include="*.md" | grep -v "exists" | head -10
```

### 5. Extend - Add to Each File

For each major file, append the Related Documentation section with appropriate links.

Priority files:

1. Each README.md in numbered folders
2. Implementation pattern files in 04_*
3. Architecture files in 01_*

### 6. Synthesize - Verify Bidirectional Links

Ensure if A references B, then B references A:

```bash
# Check reverse references
grep -l "02_Coding" 04_Implementation_Patterns/*.md
grep -l "04_Implementation" 02_Coding_Standards/*.md
```

### 7. Transform - Commit Changes

```bash
git add -A
git commit -m "docs: Add comprehensive cross-references across all sections"
git push origin main
```

## Verification

- [ ] Each numbered section has Related Documentation
- [ ] Links are bidirectional where appropriate
- [ ] No broken relative links
