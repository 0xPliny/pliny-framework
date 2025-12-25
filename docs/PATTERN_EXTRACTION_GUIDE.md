# Pattern Extraction Guide

**Version:** 1.0.0
**Last Updated:** 2025-01-XX
**Purpose:** Systematic methodology for extracting reusable patterns from reference frameworks

---

## Overview

This guide provides a step-by-step methodology for extracting documentation engineering patterns from reference frameworks and documenting them for reuse. This process was successfully applied to extract patterns from pliny-framework and apply them to Shannon documentation projects.

---

## When to Extract Patterns

**Extract Patterns When:**
- You have a reference framework with proven documentation
- You want to apply successful patterns to new projects
- You need to document reusable methodologies
- You want to create templates from successful examples

**Do NOT Extract Patterns When:**
- Reference framework is incomplete or untested
- Patterns are domain-specific without generalization
- Documentation quality is inconsistent
- Patterns are not proven effective

---

## Extraction Process

### Phase 1: Analyze Reference Framework

**Goal:** Understand the structure, content, and approach of the reference framework.

**Steps:**

1. **Inventory Documentation Structure**
   - List all documentation files
   - Map directory hierarchy
   - Identify naming conventions
   - Note organizational patterns

2. **Analyze Content Patterns**
   - Review code example formats
   - Identify documentation templates
   - Note writing style
   - Catalog diagram types

3. **Examine Writing Patterns**
   - Analyze tone and voice
   - Review audience targeting
   - Study explanation methodology
   - Note troubleshooting approach

4. **Study Engineering Patterns**
   - Understand codebase mapping
   - Review cross-referencing approach
   - Analyze quality metrics
   - Examine version control integration

**Output:** Analysis report documenting structure, content, writing, and engineering approaches.

---

### Phase 2: Identify Reusable Patterns

**Goal:** Distinguish between reusable patterns and domain-specific content.

**Criteria for Reusable Patterns:**

**✅ Reusable (100%):**
- Structural organization
- Naming conventions
- Writing style
- Quality metrics
- Cross-referencing approach

**🔄 Domain-Adaptive (80% reusable):**
- Code example formats (structure reusable, content adapts)
- Documentation templates (structure reusable, content adapts)
- Diagram types (approach reusable, content adapts)

**❌ Domain-Specific (Not Reusable):**
- Domain terminology
- Technology-specific examples
- Business logic explanations
- Use case details

**Process:**

1. **Categorize Each Pattern**
   - Is it structural? → Likely 100% reusable
   - Is it content-based? → Likely 80% reusable (structure)
   - Is it domain-specific? → Not reusable

2. **Document Pattern Abstraction**
   - What is the core pattern?
   - What can be abstracted?
   - What must adapt to domain?
   - What are the key elements?

3. **Identify Pattern Relationships**
   - Which patterns work together?
   - What are dependencies?
   - What are alternatives?

**Output:** Pattern catalog with reusability classifications.

---

### Phase 3: Document Patterns

**Goal:** Create comprehensive pattern documentation.

**Documentation Template:**

```markdown
## Pattern Name

**Description:** What the pattern is

**Reusability:** 100% / 80% / Domain-specific

**Key Elements:**
- Element 1
- Element 2
- Element 3

**When to Use:**
- Situation 1
- Situation 2

**Benefits:**
- Benefit 1
- Benefit 2

**Example:**
[Example from reference framework]

**Proven Results:**
- Metric 1: Result
- Metric 2: Result
```

**Documentation Checklist:**

- [ ] Pattern clearly described
- [ ] Reusability classified
- [ ] Key elements identified
- [ ] When to use documented
- [ ] Benefits explained
- [ ] Example provided
- [ ] Proven results included

**Output:** Pattern library documentation.

---

### Phase 4: Create Templates

**Goal:** Convert patterns into reusable templates.

**Template Types:**

1. **Structural Templates**
   - Directory structure templates
   - File naming templates
   - Index file templates

2. **Content Templates**
   - Documentation section templates
   - Code example templates
   - Function documentation templates

3. **Process Templates**
   - HARVEST phase templates
   - Quality check templates
   - Cross-reference templates

**Template Format:**

```markdown
# Template: [Template Name]

**Purpose:** [What this template is for]

**When to Use:** [When to apply this template]

**Structure:**
[Template structure with placeholders]

**Example:**
[Example of filled template]
```

**Output:** Template library.

---

## Extraction Checklist

### Pre-Extraction

- [ ] Reference framework identified
- [ ] Reference framework proven effective
- [ ] Documentation quality verified
- [ ] Extraction scope defined

### During Extraction

- [ ] Structure analyzed
- [ ] Content patterns identified
- [ ] Writing patterns documented
- [ ] Engineering patterns cataloged
- [ ] Reusability classified
- [ ] Patterns documented
- [ ] Templates created

### Post-Extraction

- [ ] Patterns validated
- [ ] Templates tested
- [ ] Documentation complete
- [ ] Integration points identified

---

## Example: Extracting from pliny-framework

### Reference Framework Analysis

**Structure:**
- Hierarchical: `00_Project_Overview/` → `01_System_Architecture/`
- Numbered prefixes: `00_*`, `01_*`, `02_*`
- Index files: `00_*.md` in each section
- Nested directories: Grouped by topic

**Content:**
- Multi-layer: Quick Start → Guide → Reference
- Code examples: Language tags, purpose comments
- Function docs: Purpose, Parameters, Returns, Examples
- ASCII diagrams: Box-drawing characters

**Writing:**
- Professional tone
- Multi-audience approach
- Conceptual → Practical flow
- Structured troubleshooting

**Engineering:**
- Codebase mapping: `src/` → `docs/`
- Cross-references: 5+ per document
- Quality metrics: 95%+ completeness
- Version control: Markdown in Git

### Pattern Identification

**100% Reusable:**
- Hierarchical organization
- Numbered prefixes
- Index files
- Multi-layer architecture
- Professional tone
- Multi-audience approach
- Conceptual → Practical flow
- Codebase mapping
- Cross-referencing standards
- Quality metrics

**80% Reusable:**
- Code example format (structure reusable, content adapts)
- Function documentation template (structure reusable, content adapts)
- ASCII diagrams (approach reusable, content adapts)

### Pattern Documentation

Created [Pattern Library](./PATTERN_LIBRARY.md) with 16 documented patterns.

### Template Creation

Created templates for:
- JavaScript documentation
- Multi-agent architecture
- Code documentation

---

## Common Pitfalls

### Pitfall 1: Over-Abstraction

**Problem:** Abstracting patterns too much, losing practical value.

**Solution:** Keep patterns concrete enough to be actionable.

### Pitfall 2: Under-Abstraction

**Problem:** Not abstracting enough, patterns too domain-specific.

**Solution:** Identify core pattern, abstract domain specifics.

### Pitfall 3: Missing Context

**Problem:** Documenting pattern without context or examples.

**Solution:** Always include examples and proven results.

### Pitfall 4: Ignoring Domain Adaptation

**Problem:** Treating all patterns as 100% reusable.

**Solution:** Classify reusability, document adaptation needs.

---

## Quality Criteria

**Pattern Documentation Quality:**

- **Clarity:** Pattern clearly described and understandable
- **Completeness:** All key elements documented
- **Examples:** Real examples from reference framework
- **Proven Results:** Metrics showing effectiveness
- **Reusability:** Correctly classified

**Template Quality:**

- **Usability:** Template is easy to use
- **Completeness:** Template covers all necessary elements
- **Examples:** Filled template examples provided
- **Flexibility:** Template adapts to different contexts

---

## Related Documentation

- [Pattern Library](./PATTERN_LIBRARY.md) - Comprehensive pattern catalog
- [Pattern Application Guide](./PATTERN_APPLICATION_GUIDE.md) - How to apply patterns
- [HARVEST Framework](../frameworks/universal_harvest.md) - Documentation methodology
- [Success Metrics](./SUCCESS_METRICS.md) - Examples of high-quality documentation

---

**Document Version:** 1.0
**Created:** 2025-01-XX
**Framework:** Pliny Documentation Engineering Patterns

