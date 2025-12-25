# Pattern Application Guide

**Version:** 1.0.0
**Last Updated:** 2025-01-XX
**Purpose:** Step-by-step guide for applying extracted patterns to new documentation projects

---

## Overview

This guide provides a systematic approach for applying documentation patterns extracted from reference frameworks to new projects. This process was successfully used to apply pliny-framework patterns to Shannon documentation, achieving 98% completeness.

---

## Pre-Application Checklist

Before applying patterns, ensure:

- [ ] Patterns extracted and documented (see [Pattern Extraction Guide](./PATTERN_EXTRACTION_GUIDE.md))
- [ ] Target project codebase analyzed
- [ ] Documentation scope defined
- [ ] Quality standards established
- [ ] HARVEST framework ready

---

## Application Process

### Phase 1: Project Analysis

**Goal:** Understand target project structure and requirements.

**Steps:**

1. **Audit Codebase**
   - Map directory structure
   - Identify major components
   - List key files and modules
   - Note technology stack

2. **Identify Documentation Needs**
   - What needs to be documented?
   - Who is the audience?
   - What is the scope?
   - What are the priorities?

3. **Assess Current State**
   - Existing documentation inventory
   - Documentation gaps
   - Quality of existing docs
   - Maintenance status

**Output:** Project analysis report with structure, needs, and current state.

---

### Phase 2: Pattern Selection

**Goal:** Select appropriate patterns for the project.

**Selection Criteria:**

**Always Apply:**
- Hierarchical Organization (Pattern 1)
- Numbered Prefixes (Pattern 2)
- Multi-Layer Architecture (Pattern 5)
- Cross-Referencing Standards (Pattern 14)
- Quality Metrics Application (Pattern 15)

**Apply Based on Project Type:**

**Code Documentation Projects:**
- Documentation-Codebase Mapping (Pattern 13)
- Function Documentation Template (Pattern 7)
- Code Example Format (Pattern 6)

**User Documentation Projects:**
- Multi-Audience Approach (Pattern 10)
- Conceptual → Practical Flow (Pattern 11)
- Structured Troubleshooting (Pattern 12)

**API Documentation Projects:**
- Function Documentation Template (Pattern 7)
- Code Example Format (Pattern 6)
- ASCII Diagrams (Pattern 8)

**Selection Process:**

1. Review [Pattern Library](./PATTERN_LIBRARY.md)
2. Identify project type
3. Select core patterns (always apply)
4. Select type-specific patterns
5. Document pattern selection rationale

**Output:** Pattern selection list with rationale.

---

### Phase 3: Structure Design

**Goal:** Design documentation structure using selected patterns.

**Process:**

1. **Apply Hierarchical Organization**
   - Create `00_Project_Overview/` root
   - Design nested directory structure
   - Plan numbered prefix scheme
   - Design index file locations

2. **Map Codebase to Documentation**
   - `src/phases/` → `docs/03_Code_Reference/02_Phases/`
   - `src/ai/` → `docs/03_Code_Reference/03_AI_Integration/`
   - Maintain codebase structure in docs

3. **Plan Multi-Layer Architecture**
   - Quick Start Guide location
   - Comprehensive Guide sections
   - Reference documentation structure
   - Troubleshooting section design

**Example Structure:**

```
docs/
├── 00_Project_Overview/
│   ├── 00_Executive_Summary.md
│   ├── 00_Quick_Start_Guide.md
│   ├── 01_System_Architecture/
│   │   ├── 00_Architecture_Overview.md
│   │   └── ...
│   └── ...
├── 03_Code_Reference/
│   ├── 00_Code_Index.md
│   └── ...
└── ...
```

**Output:** Documentation structure design.

---

### Phase 4: Template Application

**Goal:** Apply templates to create initial documentation structure.

**Process:**

1. **Select Templates**
   - Choose templates matching project type
   - Select language-specific templates
   - Pick architecture templates if needed

2. **Apply Templates**
   - Create files from templates
   - Fill placeholders with project info
   - Adapt templates to project needs
   - Maintain template structure

3. **Validate Structure**
   - Check all required files created
   - Verify naming conventions
   - Validate directory structure
   - Confirm index files present

**Output:** Initial documentation structure with templates applied.

---

### Phase 5: Content Generation

**Goal:** Generate documentation content following patterns.

**Process:**

1. **Follow HARVEST Framework**
   - HARVEST: Extract information
   - ANALYZE: Understand patterns
   - RESTRUCTURE: Apply templates
   - VERIFY: Validate accuracy
   - EXTEND: Add examples
   - SYNTHESIZE: Create cross-references
   - TRANSFORM: Generate output

2. **Apply Writing Patterns**
   - Use professional tone
   - Target multiple audiences
   - Follow conceptual → practical flow
   - Structure troubleshooting content

3. **Apply Content Patterns**
   - Use code example format
   - Apply function documentation template
   - Create ASCII diagrams
   - Follow multi-layer architecture

**Output:** Complete documentation content.

---

### Phase 6: Cross-Reference Creation

**Goal:** Create comprehensive cross-references.

**Process:**

1. **Identify Cross-Reference Opportunities**
   - Component mentions
   - Configuration references
   - Workflow connections
   - Related concepts

2. **Create Cross-References**
   - Minimum 5+ per document
   - Target 6-7 average
   - Group by category
   - Use relative paths

3. **Validate Cross-References**
   - Check all links resolve
   - Verify anchor links work
   - Confirm relative paths correct
   - Test navigation

**Output:** Complete cross-reference network.

---

### Phase 7: Quality Validation

**Goal:** Ensure documentation meets quality standards.

**Quality Checks:**

1. **Completeness (95%+ target)**
   - All required sections present
   - All major components documented
   - All workflows explained
   - All configurations covered

2. **Accuracy (98%+ target)**
   - Examples verified against codebase
   - Facts cross-checked
   - Terminology consistent
   - Links validated

3. **Cross-Reference Density (5+ minimum, 6-7 average)**
   - Count cross-references per document
   - Calculate average
   - Identify gaps
   - Add missing references

4. **Example Coverage (90%+ target)**
   - Count entities with examples
   - Calculate coverage percentage
   - Identify missing examples
   - Add examples for gaps

**Output:** Quality metrics report.

---

## Domain Adaptation Guidelines

### Adapting Structural Patterns

**Structural patterns are 100% reusable** - apply as-is:
- Hierarchical organization works for all domains
- Numbered prefixes work for all domains
- Index files work for all domains
- Nested directories work for all domains

**No adaptation needed.**

---

### Adapting Content Patterns

**Content patterns are 80% reusable** - adapt content, maintain structure:

**Code Example Format:**
- ✅ Structure: Language tags, purpose comments, complete examples
- 🔄 Content: Adapt to project's language and technology

**Function Documentation Template:**
- ✅ Structure: Purpose, Parameters, Returns, Examples
- 🔄 Content: Adapt to project's function signatures and conventions

**ASCII Diagrams:**
- ✅ Structure: Box-drawing characters, labels, annotations
- 🔄 Content: Adapt to project's architecture and components

---

### Adapting Writing Patterns

**Writing patterns are 100% reusable** - apply as-is:
- Professional tone works for all domains
- Multi-audience approach works for all domains
- Conceptual → Practical flow works for all domains
- Structured troubleshooting works for all domains

**No adaptation needed.**

---

### Adapting Engineering Patterns

**Engineering patterns are 100% reusable** - apply as-is:
- Documentation-codebase mapping works for all domains
- Cross-referencing standards work for all domains
- Quality metrics work for all domains
- Version control integration works for all domains

**No adaptation needed.**

---

## Quality Maintenance During Application

### Continuous Quality Checks

**During Content Generation:**
- Verify examples against codebase
- Check terminology consistency
- Validate cross-references as created
- Track quality metrics

**During Cross-Reference Creation:**
- Ensure minimum 5+ per document
- Target 6-7 average
- Validate all links
- Group by category

**During Final Review:**
- Calculate completeness score
- Calculate accuracy score
- Count cross-references
- Measure example coverage

### Iteration Until Quality Thresholds Met

**Iteration Process:**

1. Generate initial documentation
2. Calculate quality metrics
3. Identify gaps and issues
4. Fill gaps and fix issues
5. Recalculate metrics
6. Repeat until thresholds met

**Stop When:**
- Completeness ≥ 95%
- Accuracy ≥ 98%
- Cross-references ≥ 5+ per doc (6-7 avg recommended)
- Examples ≥ 90% coverage

---

## Example: Applying Patterns to Shannon

### Project Analysis

**Codebase Structure:**
- JavaScript/Node.js project
- Multi-agent architecture
- Docker deployment
- YAML configuration

**Documentation Needs:**
- Code reference documentation
- Architecture documentation
- Configuration documentation
- Workflow documentation

### Pattern Selection

**Core Patterns (Always Apply):**
- Hierarchical Organization
- Numbered Prefixes
- Multi-Layer Architecture
- Cross-Referencing Standards
- Quality Metrics Application

**Code Documentation Patterns:**
- Documentation-Codebase Mapping
- Function Documentation Template
- Code Example Format

**Architecture Patterns:**
- ASCII Diagrams
- Multi-Agent Architecture Template

### Structure Design

```
docs/
├── 00_Project_Overview/
│   ├── 00_Executive_Summary.md
│   ├── 00_Quick_Start_Guide.md
│   ├── 01_System_Architecture/
│   │   ├── 00_Architecture_Overview.md
│   │   ├── 01_Component_Dependency_Map.md
│   │   ├── 02_Data_Flow_Diagrams.md
│   │   ├── 03_Phase_Orchestration.md
│   │   └── 04_Multi_Agent_Architecture.md
│   └── ...
├── 03_Code_Reference/
│   ├── 00_Code_Index.md
│   ├── 01_Core_Orchestration/
│   ├── 02_Phases/
│   ├── 03_AI_Integration/
│   └── ...
└── ...
```

### Results

**Quality Metrics Achieved:**
- Completeness: 98% (exceeded 95% target)
- Accuracy: 98%+ (met target)
- Cross-References: 6-7 average (exceeded 5+ minimum)
- Examples: 90%+ (met target)

**Documentation Generated:**
- 28 documentation files
- 180+ cross-references
- Complete code reference
- Comprehensive architecture docs

---

## Common Challenges

### Challenge 1: Domain-Specific Content

**Problem:** How to adapt patterns to domain-specific content.

**Solution:** Maintain pattern structure, adapt content. Use domain modules for domain-specific standards.

### Challenge 2: Large Codebase

**Problem:** How to document large codebase systematically.

**Solution:** Use codebase mapping pattern, create index files, group by component type.

### Challenge 3: Missing Source Material

**Problem:** Incomplete source code or missing documentation.

**Solution:** Document gaps explicitly, mark incomplete sections, proceed with available information.

### Challenge 4: Quality Threshold Not Met

**Problem:** Quality metrics below thresholds after initial generation.

**Solution:** Iterate using HARVEST framework, identify gaps, fill systematically, recalculate metrics.

---

## Related Documentation

- [Pattern Library](./PATTERN_LIBRARY.md) - Comprehensive pattern catalog
- [Pattern Extraction Guide](./PATTERN_EXTRACTION_GUIDE.md) - How to extract patterns
- [HARVEST Framework](../frameworks/universal_harvest.md) - Documentation methodology
- [Success Metrics](./SUCCESS_METRICS.md) - Examples of high-quality documentation

---

**Document Version:** 1.0
**Created:** 2025-01-XX
**Framework:** Pliny Documentation Engineering Patterns

