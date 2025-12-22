# PlinyHub Templates

Reusable templates for common problem-solving scenarios.

---

## Quick Reference

| Template | Framework | Use When |
|----------|-----------|----------|
| [Feature Development](rise/feature_development.md) | R-I-S-E | Building a new feature |
| [System Design](rise/system_design.md) | R-I-S-E | Designing architecture |
| [Investigation](rise/investigation.md) | R-I-S-E | Researching unknowns |
| [Bug Fix](care/bug_fix.md) | C-A-R-E | Fixing a specific bug |
| [Code Review](care/code_review.md) | C-A-R-E | Reviewing a PR/change |
| [Quick Enhancement](care/quick_enhancement.md) | C-A-R-E | Small improvements |
| [Code Documentation](harvest/code_documentation.md) | HARVEST | Documenting code |
| [Legacy Analysis](harvest/legacy_analysis.md) | HARVEST | Understanding legacy code |
| [Session Capture](omega/session_capture.md) | OMEGA | End-of-session learning |

---

## Templates by Framework

### R-I-S-E Templates

For **complex, thorough** work requiring research first.

- **[feature_development.md](rise/feature_development.md)** - New feature creation
- **[system_design.md](rise/system_design.md)** - Architecture and design
- **[investigation.md](rise/investigation.md)** - Research and analysis

### C-A-R-E Templates

For **fast, iterative** work with quick feedback loops.

- **[bug_fix.md](care/bug_fix.md)** - Debugging and fixes
- **[code_review.md](care/code_review.md)** - PR reviews
- **[quick_enhancement.md](care/quick_enhancement.md)** - Small improvements

### HARVEST Templates

For **documentation** and understanding existing code.

- **[code_documentation.md](harvest/code_documentation.md)** - Generate docs
- **[legacy_analysis.md](harvest/legacy_analysis.md)** - Understand legacy code

### OMEGA Templates

For **learning capture** and framework improvement.

- **[session_capture.md](omega/session_capture.md)** - End-of-session learning

---

## How to Use

### 1. Copy the Template

```bash
# Copy to your working directory
cp templates/rise/feature_development.md ./TASK_NAME.md
```

### 2. Fill in the Sections

Work through each section, filling in the blanks and checking boxes.

### 3. Follow the Framework Phases

Templates guide you through R-I-S-E, C-A-R-E, or HARVEST phases.

### 4. Capture Learnings

Use the OMEGA section at the end to record what you learned.

---

## Template Selection Guide

```
CREATING something new?
├── Complex/unfamiliar → rise/feature_development.md
├── Architecture → rise/system_design.md
└── Simple → care/quick_enhancement.md

FIXING something?
├── Bug → care/bug_fix.md
├── Performance → care/quick_enhancement.md
└── Unknown cause → rise/investigation.md

UNDERSTANDING something?
├── Code → harvest/code_documentation.md
├── Legacy system → harvest/legacy_analysis.md
└── Problem space → rise/investigation.md

REVIEWING something?
└── Code/PR → care/code_review.md

END OF SESSION?
└── Capture learnings → omega/session_capture.md
```

---

## Creating Custom Templates

Base your custom templates on existing ones:

1. Copy the closest template
2. Modify sections for your use case
3. Save to `templates/[framework]/your_template.md`
4. Add to this index

**Required sections:**

- Metadata block with framework/use_case
- Each phase of the chosen framework
- Verification checklist
- OMEGA learning capture
