---
description: Fix README merge conflicts in MHC-Developers-Guide using C-A-R-E framework
---

# Fix MHC-Developers-Guide README Merge Conflict

## Prerequisites

- Repository cloned locally
- Write access to repo

## Steps

### 1. Context (C)

// turbo

```bash
git clone https://github.com/0xPliny/MHC-Developers-Guide.git
cd MHC-Developers-Guide
```

View the conflict:

```bash
cat README.md | Select-String -Pattern "<<<<<<<|=======|>>>>>>>" -Context 3
```

### 2. Action (A)

Open README.md and locate conflict markers:

- `<<<<<<< HEAD` - Start of your changes
- `=======` - Separator
- `>>>>>>> branch` - End of incoming changes

Resolve by keeping the best of both sections. Typically:

- Keep all section links that are valid
- Remove duplicate entries
- Ensure numbered sections (00-17) are complete

### 3. Result (R)

// turbo

```bash
git add README.md
git commit -m "fix: Resolve README merge conflict - consolidate section links"
git push origin main
```

### 4. Evolution (E)

Add a pre-commit hook to validate README structure:

```bash
# .git/hooks/pre-commit
grep -q "<<<<<<<" README.md && echo "Merge conflict detected!" && exit 1
exit 0
```

## Verification

- [ ] No conflict markers remain
- [ ] All section links (00-17) present
- [ ] README renders correctly on GitHub
