---
description: Verify MHC documentation against source code to ensure accuracy
---

# Verify MHC Documentation Against Source Code

## Prerequisites

- MHC-Developers-Guide cloned
- Access to D:\ICIS\Fast-DhubDev source code
- PlinyHub 5-Layer Verification System knowledge

## Steps

### Layer 1: Syntax Verification

// turbo

```bash
cd MHC-Developers-Guide
# Check markdown syntax
Get-ChildItem -Recurse -Filter "*.md" | ForEach-Object { 
    $content = Get-Content $_.FullName -Raw
    if ($content -match "^#{5,}") { Write-Host "Deep heading: $($_.Name)" }
}
```

### Layer 2: Semantic Verification

Check that documented patterns exist in source:

```bash
# Verify documented stored procedures exist
$procs = Get-Content "07_Database_Reference/stored_procedures.md" | 
    Select-String -Pattern "^\|\s*(\w+)\s*\|" | 
    ForEach-Object { $_.Matches.Groups[1].Value }

foreach ($proc in $procs) {
    if (Test-Path "D:\ICIS\Fast-DhubDev\SQL Generated Stored Procedures\$proc.sql") {
        Write-Host "✓ $proc exists"
    } else {
        Write-Host "✗ $proc MISSING" -ForegroundColor Red
    }
}
```

### Layer 3: Integration Verification

Verify documented data flows match actual code:
// turbo

```bash
# Check if documented functions exist in source
grep -r "findwork" D:\ICIS\Fast-DhubDev\MSVC Programs\area\p_ar_movdp\ | head -5
```

### Layer 4: System Verification

Test documented patterns work end-to-end:

1. Start test environment
2. Execute documented scenarios
3. Verify expected outcomes

### Layer 5: Human Review

Flag items for expert review:

- Complex state machine transitions
- Error handling edge cases
- Performance-critical patterns

## Output

Create a verification report:

```markdown
# Documentation Verification Report

## Date: [YYYY-MM-DD]

## Summary
- Total procedures documented: X
- Verified in source: Y
- Missing from source: Z

## Discrepancies
| Document | Issue | Recommendation |
|----------|-------|----------------|
| 03_Stored_Procedures.md | `OldProc` removed | Remove from docs |

## Next Actions
1. Update outdated references
2. Add newly discovered procedures
3. Request expert review for [items]
```

## Verification

- [ ] All documented items traced to source
- [ ] Discrepancies logged
- [ ] Report generated
