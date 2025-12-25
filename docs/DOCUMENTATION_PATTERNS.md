# Documentation-Specific Patterns

**Version:** 1.0.0
**Last Updated:** 2025-01-XX
**Purpose:** Documentation-specific patterns and best practices

---

## Overview

This document provides documentation-specific patterns that complement the general patterns in the [Pattern Library](./PATTERN_LIBRARY.md). These patterns focus specifically on documentation creation, maintenance, and quality.

---

## Documentation Structure Patterns

### Pattern: Progressive Disclosure

**Description:** Structure documentation to reveal information progressively.

**Implementation:**
- Quick Start (5 minutes) - Essential information only
- Comprehensive Guide (30-60 minutes) - Detailed information
- Reference Documentation (as needed) - Complete information
- Troubleshooting (problem-solving) - Solutions to problems

**Benefits:**
- Prevents information overload
- Serves different audiences
- Enables quick access
- Supports progressive learning

---

### Pattern: Multiple Entry Points

**Description:** Provide multiple ways to access documentation.

**Entry Points:**
- Quick Start Guide (new users)
- Architecture Overview (architects)
- Code Reference (developers)
- Troubleshooting (problem-solvers)
- Configuration Guide (operators)

**Benefits:**
- Increases discoverability
- Serves different use cases
- Reduces navigation time
- Improves user experience

---

## Content Organization Patterns

### Pattern: Conceptual Before Practical

**Description:** Always explain concepts before showing practical usage.

**Order:**
1. What is it? (Concept)
2. Why does it exist? (Purpose)
3. How does it work? (Mechanism)
4. How to use it? (Practical)
5. Examples (Application)

**Benefits:**
- Builds understanding
- Prevents confusion
- Enables better usage
- Improves retention

---

### Pattern: Examples-First Learning

**Description:** Provide examples early, then explain details.

**Structure:**
- Quick example at start
- Detailed explanation
- More examples
- Advanced usage

**Benefits:**
- Shows value immediately
- Provides context
- Enables experimentation
- Improves learning

---

## Writing Patterns

### Pattern: Active Voice

**Description:** Use active voice for instructions and descriptions.

**Examples:**
- ✅ "You can configure the system by editing the YAML file."
- ❌ "The system may be configured through YAML file modification."

**Benefits:**
- Clearer instructions
- More engaging
- Easier to follow
- Better readability

---

### Pattern: Second Person for Instructions

**Description:** Address readers directly using "you" for instructions.

**Examples:**
- ✅ "To install, run: `npm install`"
- ❌ "To install, one should run: `npm install`"

**Benefits:**
- More personal
- Clearer instructions
- Better engagement
- Easier to follow

---

### Pattern: Consistent Terminology

**Description:** Use consistent terminology throughout documentation.

**Guidelines:**
- Define terms on first use
- Use same term for same concept
- Avoid synonyms for same concept
- Maintain glossary

**Benefits:**
- Reduces confusion
- Improves clarity
- Enables search
- Professional appearance

---

## Code Example Patterns

### Pattern: Complete Working Examples

**Description:** Provide complete, runnable examples, not fragments.

**Structure:**
```javascript
// Purpose: Brief description of why this example exists

// Imports/requires
const { Component } = require('./component');

// Setup
const instance = new Component(config);

// Usage
const result = await instance.method();

// Output
console.log(result);
```

**Benefits:**
- Examples actually work
- Users can copy-paste
- Reduces frustration
- Improves learning

---

### Pattern: Purpose Comments

**Description:** Include comments explaining why, not just what.

**Examples:**
- ✅ `// Purpose: Demonstrate async error handling pattern`
- ❌ `// Error handling`

**Benefits:**
- Explains context
- Shows intent
- Improves understanding
- Enables learning

---

### Pattern: Progressive Examples

**Description:** Provide examples from simple to complex.

**Structure:**
- Basic example (minimal)
- Common usage example
- Advanced example
- Edge case example

**Benefits:**
- Supports progressive learning
- Shows evolution
- Covers all use cases
- Improves understanding

---

## Cross-Reference Patterns

### Pattern: Category Grouping

**Description:** Group cross-references by category.

**Format:**
```markdown
## Related Documentation

### Components
- [Component A](../path/to/a.md) - Description
- [Component B](../path/to/b.md) - Description

### Configuration
- [Config A](../path/to/config-a.md) - Description

### Workflows
- [Workflow A](../path/to/workflow-a.md) - Description
```

**Benefits:**
- Organized references
- Easy to scan
- Better context
- Improved navigation

---

### Pattern: Descriptive Links

**Description:** Use descriptive link text, not generic "here" or "this".

**Examples:**
- ✅ "[Component Documentation](../path/to/component.md) - Details on component usage"
- ❌ "[Click here](../path/to/component.md) for more information"

**Benefits:**
- Clearer purpose
- Better accessibility
- Improved scanning
- Professional appearance

---

## Quality Patterns

### Pattern: Quality Metrics Tracking

**Description:** Track quality metrics throughout documentation process.

**Metrics:**
- Completeness (95%+ target)
- Accuracy (98%+ target)
- Cross-reference density (5+ minimum, 6-7 average recommended)
- Example coverage (90%+ target)

**Benefits:**
- Objective quality assessment
- Identifies gaps
- Enables improvement
- Maintains standards

---

### Pattern: Iterative Improvement

**Description:** Iterate documentation until quality thresholds met.

**Process:**
1. Generate initial documentation
2. Calculate quality metrics
3. Identify gaps
4. Fill gaps
5. Recalculate metrics
6. Repeat until thresholds met

**Benefits:**
- Ensures quality
- Prevents documentation debt
- Systematic improvement
- Maintains standards

---

## Maintenance Patterns

### Pattern: Version Control Integration

**Description:** Integrate documentation with version control.

**Approach:**
- Markdown files in Git
- Version with code
- Track changes
- Maintain history

**Benefits:**
- Change tracking
- Collaboration support
- History preservation
- Rollback capability

---

### Pattern: Freshness Maintenance

**Description:** Keep documentation current with code changes.

**Target:** Update documentation within 7 days of code changes

**Process:**
- Monitor code changes
- Update affected documentation
- Verify examples still work
- Update cross-references if needed

**Benefits:**
- Prevents stale information
- Maintains accuracy
- Reduces confusion
- Improves trust

---

## Related Documentation

- [Pattern Library](./PATTERN_LIBRARY.md) - Comprehensive pattern catalog
- [Pattern Extraction Guide](./PATTERN_EXTRACTION_GUIDE.md) - How to extract patterns
- [Pattern Application Guide](./PATTERN_APPLICATION_GUIDE.md) - How to apply patterns
- [Success Metrics](./SUCCESS_METRICS.md) - Examples of high-quality documentation
- [HARVEST Framework](../frameworks/universal_harvest.md) - Documentation methodology

---

**Document Version:** 1.0
**Created:** 2025-01-XX
**Framework:** Pliny Documentation Engineering Patterns

