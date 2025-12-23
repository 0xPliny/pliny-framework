# Universal H-A-R-V-E-S-T Framework

**Version:** 2.0 (Universal)
**Purpose:** Domain-agnostic systematic documentation and knowledge extraction methodology

---

## Overview

H-A-R-V-E-S-T is a 7-phase approach for **extracting knowledge from existing artifacts** and **transforming it into structured documentation**. It works for any domain; domain-specific standards are injected via modules.

```
┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐
│ HARVEST  │→ │ ANALYZE  │→ │RESTRUCTURE│→ │  VERIFY  │→ │  EXTEND  │→ │SYNTHESIZE│→ │TRANSFORM │
│ Extract  │  │ Patterns │  │ Template │  │ Accuracy │  │ Examples │  │  Links   │  │  Output  │
└──────────┘  └──────────┘  └──────────┘  └──────────┘  └──────────┘  └──────────┘  └──────────┘
      ↑                                                                                   │
      └─────────────────────────── Iterate until 95%+ quality ────────────────────────────┘
```

---

## When to Use HARVEST

### Use HARVEST For:

- Documenting existing code, systems, or processes
- Extracting knowledge from legacy systems
- Creating reference documentation
- Building knowledge bases
- Onboarding documentation
- API documentation generation
- Understanding unfamiliar codebases

### Do NOT Use HARVEST For:

- Creating new systems (use R-I-S-E)
- Quick bug fixes (use C-A-R-E)
- Designing architecture (use R-I-S-E)
- Problems requiring implementation (use R-I-S-E or C-A-R-E)

---

## Phase 1: HARVEST (Extract)

**Goal:** Gather all raw information from source artifacts

**Maximum Duration:** 25% of total time budget

### Universal Steps

1. **Identify Source Artifacts**
   - Source code files
   - Existing documentation (even if outdated)
   - Configuration files
   - Database schemas
   - API specifications
   - Log files and error messages
   - Comments and inline documentation

2. **Extract Raw Information**
   - Function signatures and parameters
   - Class structures and relationships
   - Data types and schemas
   - Configuration keys and values
   - Dependencies and imports
   - Error codes and status values

3. **Catalog Entities**
   - Create list of all identifiable entities
   - Note entity types (process, table, function, config)
   - Record source location for each entity

4. **Flag Gaps**
   - What entities are referenced but not found?
   - What documentation is missing entirely?
   - What appears incomplete?

### HARVEST Checklist

- [ ] All source artifacts identified
- [ ] Entity list complete
- [ ] Entity types categorized
- [ ] Source locations recorded
- [ ] Gaps flagged for follow-up

### HARVEST Output

```yaml
harvest_output:
  artifacts_processed:
    - path: "[source file path]"
      type: "[code|config|docs|schema]"
      entities_found: ["entity1", "entity2"]

  entity_catalog:
    - name: "[entity name]"
      type: "[process|table|function|config|class]"
      source: "[file:line]"
      status: "found|referenced|missing"

  gaps_identified:
    - entity: "[name]"
      issue: "[missing|incomplete|outdated]"
      priority: "[high|medium|low]"
```

---

## Phase 2: ANALYZE (Understand)

**Goal:** Understand structure, patterns, and relationships

**Maximum Duration:** 20% of total time budget

### Universal Steps

1. **Identify Structure**
   - How are entities organized?
   - What is the hierarchy?
   - What groups naturally form?

2. **Map Relationships**
   - Which entities call/use which?
   - What are the data flows?
   - What are the dependencies?

3. **Recognize Patterns**
   - What design patterns are used?
   - What naming conventions exist?
   - What code styles are followed?

4. **Determine Purpose**
   - Why does each entity exist?
   - What problem does it solve?
   - What would break without it?

### ANALYZE Checklist

- [ ] Entity hierarchy understood
- [ ] Relationships mapped
- [ ] Patterns identified
- [ ] Purpose determined for key entities
- [ ] Data flows traced

### ANALYZE Output

```yaml
analyze_output:
  structure:
    hierarchy:
      - level: 1
        entities: ["top-level-1", "top-level-2"]
      - level: 2
        parent: "top-level-1"
        entities: ["child-1", "child-2"]

  relationships:
    - from: "[entity A]"
      to: "[entity B]"
      type: "[calls|reads|writes|triggers|configures]"

  patterns:
    - name: "[pattern name]"
      instances: ["entity1", "entity2"]
      description: "[how pattern is used]"
```

---

## Phase 3: RESTRUCTURE (Organize)

**Goal:** Apply documentation template and organize content

**Maximum Duration:** 15% of total time budget

### Universal Steps

1. **Select Documentation Template**
   - Process documentation template
   - Table/schema documentation template
   - API documentation template
   - Configuration reference template
   - Quick reference template

2. **Map Entities to Sections**
   - Where does each entity belong?
   - What level of detail is needed?
   - What groupings make sense?

3. **Define Section Structure**
   - Overview sections
   - Detail sections
   - Reference sections
   - Quick lookup sections

4. **Apply Consistent Formatting**
   - Headers and hierarchy
   - Code block formatting
   - Table formatting
   - Cross-reference format

### RESTRUCTURE Checklist

- [ ] Template selected
- [ ] Entities mapped to sections
- [ ] Section structure defined
- [ ] Formatting consistent
- [ ] Navigation clear

### Standard Document Structure

```markdown
# [Entity/Topic Name]

## Overview
[1-2 sentence description]

## Purpose
[Why this exists, what problem it solves]

## [Detail Sections - vary by entity type]

## Configuration
[If applicable]

## Error Handling
[If applicable]

## Examples
[Working examples]

## Troubleshooting
[Common issues and solutions]

## Related Documentation
[Cross-references]
```

---

## Phase 4: VERIFY (Validate)

**Goal:** Ensure accuracy against source material

**Maximum Duration:** 15% of total time budget

### Universal Steps

1. **Cross-Check Facts**
   - Does documentation match source code?
   - Are types and signatures correct?
   - Are status values accurate?
   - Do examples actually work?

2. **Validate Completeness**
   - Are all required sections present?
   - Are all entities documented?
   - Are all relationships shown?

3. **Check Consistency**
   - Is terminology consistent?
   - Are formatting rules followed?
   - Do cross-references resolve?

4. **Flag Uncertainties**
   - Mark assumptions clearly
   - Note where source is ambiguous
   - Indicate confidence level

### VERIFY Checklist

- [ ] All facts cross-checked against source
- [ ] All required sections present
- [ ] Terminology consistent
- [ ] Cross-references valid
- [ ] Uncertainties flagged

### Confidence Levels

| Level | Meaning | When to Use |
|-------|---------|-------------|
| **High** | Verified directly from source | Code inspection, running tests |
| **Medium** | Inferred from context | Pattern matching, documentation |
| **Low** | Assumption based on limited info | Missing source, outdated docs |

---

## Phase 5: EXTEND (Enrich)

**Goal:** Add practical examples, edge cases, and troubleshooting

**Maximum Duration:** 10% of total time budget

### Universal Steps

1. **Add Working Examples**
   - Code snippets that compile/run
   - SQL queries that return results
   - Configuration examples
   - Command-line examples

2. **Document Edge Cases**
   - What happens with null/empty input?
   - What are the boundary conditions?
   - What causes errors?

3. **Add Troubleshooting Guidance**
   - Common problems and solutions
   - Diagnostic queries/commands
   - Error message explanations

4. **Include Gotchas**
   - Non-obvious behaviors
   - Common mistakes
   - Performance considerations

### EXTEND Checklist

- [ ] Working examples added
- [ ] Edge cases documented
- [ ] Troubleshooting section present
- [ ] Common gotchas noted

---

## Phase 6: SYNTHESIZE (Connect)

**Goal:** Create cross-references and build the knowledge graph

**Maximum Duration:** 10% of total time budget

### Universal Steps

1. **Build Entity Index**
   - List all documented entities
   - Create searchable index
   - Add entity type classifications

2. **Inject Cross-References**
   - Link entity mentions to their documentation
   - Add "Related Documentation" sections
   - Create bidirectional links

3. **Create Navigation**
   - Table of contents
   - Quick reference links
   - Category navigation

4. **Generate Relationship Diagrams**
   - Mermaid diagrams for flows
   - Entity relationship diagrams
   - State machine diagrams

### SYNTHESIZE Checklist

- [ ] Entity index created
- [ ] Cross-references injected
- [ ] Navigation complete
- [ ] Diagrams generated
- [ ] All links validated

### Cross-Reference Format

```markdown
## Related Documentation

### Processes
- [p_ar_movdp](../03_Move_Management/01_Move_Dispatcher.md) - Creates moves

### Database
- [MHC_MOVS](../06_Database_Reference/01_Core_Tables.md#mhc_movs) - Move records

### Configuration
- [DBINI](../07_Configuration_Reference/01_DBINI_Configuration.md) - Settings
```

---

## Phase 7: TRANSFORM (Output)

**Goal:** Generate final documentation in target format

**Maximum Duration:** 5% of total time budget

### Universal Steps

1. **Apply Final Formatting**
   - Syntax highlighting
   - Table alignment
   - Consistent spacing

2. **Generate Output Files**
   - Markdown files
   - Index files
   - Navigation files

3. **Quality Scoring**
   - Calculate completeness score
   - Calculate cross-reference density
   - Identify remaining gaps

4. **Version and Timestamp**
   - Add version number
   - Add generation date
   - Add framework attribution

### TRANSFORM Checklist

- [ ] Formatting applied
- [ ] Output files generated
- [ ] Quality scores calculated
- [ ] Version/timestamp added
- [ ] Final validation complete

### Quality Metrics

| Metric | Target | Calculation |
|--------|--------|-------------|
| **Completeness** | 95%+ | Required sections present / Total required |
| **Accuracy** | 98%+ | Verified facts / Total facts |
| **Cross-Reference Density** | 10+/file | Links per documentation file |
| **Examples** | 90%+ | Entities with examples / Total entities |
| **Freshness** | <7 days | Days since source code change |

---

## Domain Module Integration

HARVEST uses domain modules to inject domain-specific standards.

### Module Injection Points

```yaml
harvest_injection:
  phase_1_harvest:
    - "[ENTITY_TYPES]"      # Domain-specific entity categories
    - "[SOURCE_PATTERNS]"   # How to identify entities in source

  phase_3_restructure:
    - "[DOC_TEMPLATE]"      # Domain-specific documentation template
    - "[SECTION_STANDARDS]" # Required sections for this domain

  phase_4_verify:
    - "[QUALITY_GATES]"     # Domain-specific quality thresholds
    - "[STANDARDS]"         # Coding/naming standards to verify

  phase_5_extend:
    - "[EXAMPLE_FORMAT]"    # How examples should be formatted
    - "[TROUBLESHOOTING]"   # Domain-specific troubleshooting patterns
```

### Loading Domain Module

```bash
pliny module load murata_mhc    # Load before running HARVEST
pliny harvest <file>            # Run HARVEST with module standards
```

---

## Iteration Criteria

### Continue Iterating When:

- Quality score below 95%
- Missing cross-references identified
- Accuracy issues found
- User feedback indicates gaps

### Stop Iterating When:

- Quality score 95%+ achieved
- All required sections complete
- Cross-references validated
- User accepts documentation

### Maximum Iterations: 5

After 5 iterations without reaching 95%, escalate to human review.

---

## Self-Improving Loop

HARVEST can be run iteratively with gap analysis:

```
┌─────────────────────────────────────────────────────────────────┐
│                    HARVEST SELF-IMPROVEMENT                      │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Iteration 1: Initial HARVEST → ~60% quality                    │
│       ↓                                                          │
│  Gap Analysis: "What's missing?"                                │
│       ↓                                                          │
│  Iteration 2: Fill gaps → ~80% quality                          │
│       ↓                                                          │
│  Cross-Reference: "What should link where?"                     │
│       ↓                                                          │
│  Iteration 3: Add links → ~90% quality                          │
│       ↓                                                          │
│  Polish: "Improve readability"                                  │
│       ↓                                                          │
│  Iteration 4: Final polish → ~95% quality                       │
│       ↓                                                          │
│  COMPLETE                                                        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## CLI Commands

```bash
# Run full HARVEST cycle
pliny harvest <file_or_directory>

# Run specific phase
pliny harvest <file> --phase analyze

# Check quality score
pliny harvest score <documentation_file>

# Inject cross-references
pliny harvest xref <docs_directory>

# Generate gap analysis
pliny harvest gaps <docs_directory>
```

---

## Quick Reference

```
H - HARVEST:     Extract raw information from source artifacts
A - ANALYZE:     Understand structure, patterns, relationships
R - RESTRUCTURE: Apply template, organize content
V - VERIFY:      Validate accuracy against source
E - EXTEND:      Add examples, edge cases, troubleshooting
S - SYNTHESIZE:  Create cross-references, build knowledge graph
T - TRANSFORM:   Generate final output, calculate quality score

Time Budget:
  HARVEST:     25%
  ANALYZE:     20%
  RESTRUCTURE: 15%
  VERIFY:      15%
  EXTEND:      10%
  SYNTHESIZE:  10%
  TRANSFORM:    5%

Quality Targets:
  Completeness:    95%+
  Accuracy:        98%+
  Cross-refs:      10+ per file
  Examples:        90%+ coverage
```

---

## Error Handling and Quality Threshold Failures

### Quality Threshold Handling

HARVEST has a quality target of 95%+. When quality remains below threshold after 5 iterations:

#### Quality Below Threshold After 5 Iterations

**Condition:** Overall quality score < 95% after 5 complete iterations

**Assessment Steps:**

1. **Identify Quality Gap**
   ```yaml
   quality_assessment:
     overall_score: 0.87
     completeness: 0.92
     accuracy: 0.95
     structure: 0.83
     cross_references: 0.78
     examples: 0.90
     gap_analysis: "Structure and cross-references below target"
   ```

2. **Determine Root Cause**

   ```
   IF source material insufficient:
       → Missing artifacts
       → Incomplete source documentation
       → Legacy/unmaintained code
       
   ELSE IF structural issues:
       → Template mismatch
       → Organization problems
       → Formatting inconsistencies
       
   ELSE IF accuracy issues:
       → Source code out of sync
       → Conflicting information
       → Ambiguous implementations
   ```

#### Recovery Strategies

**Scenario 1: Insufficient Source Material**

**When:** Source artifacts are missing, incomplete, or poorly documented

**Handling:**
1. Document gaps explicitly in output
2. Mark incomplete sections clearly
3. Note what information is missing
4. Proceed with available information
5. Add disclaimer: "Documentation incomplete due to missing sources"

**Output Format:**
```markdown
## Component X

[Documentation based on available sources]

**⚠️ Documentation Gap:** The following information is missing:
- API endpoint specifications
- Error handling procedures
- Configuration options

**Source Status:** 
- Source files: Partially available
- Documentation: Missing
- Tests: Available but incomplete
```

**Scenario 2: Structural Issues**

**When:** Quality issues relate to organization, structure, or formatting

**Handling:**
1. Try alternative template
2. Simplify structure if too complex
3. Focus on most critical sections first
4. Accept lower structure score if content is accurate
5. Note structural limitations in output

**Recovery Actions:**
- Review template selection
- Try simpler organization scheme
- Prioritize critical sections
- Defer polish for later iteration

**Scenario 3: Accuracy Issues**

**When:** Information conflicts or is ambiguous

**Handling:**
1. Request user verification for uncertain sections
2. Mark uncertain sections explicitly
3. Provide source references for user review
4. Document conflicts and ambiguities
5. Allow user to correct during review

**Markup Format:**
```markdown
## Function: processData()

Processes input data according to configuration.

**⚠️ Verification Needed:** The following details need user confirmation:
- Expected input format (source code suggests JSON, but tests use XML)
- Error handling behavior (two different patterns found)
- Return value type (declared as `string` but returns `object` in some paths)

**Sources:**
- Implementation: `src/processData.ts:45-120`
- Tests: `tests/processData.test.ts:12-45`
- Documentation: Missing
```

#### Accepting Partial Quality

**When:** Quality cannot reach 95% threshold despite best efforts

**Decision Criteria:**
- Quality > 85%: Acceptable with explicit gap documentation
- Quality 75-85%: Accept with strong warnings and gap analysis
- Quality < 75%: Request user intervention or source improvement

**Acceptance Format:**
```yaml
harvest_completion:
  quality_score: 0.87
  threshold: 0.95
  status: "Accepted with documented gaps"
  gaps_documented: true
  user_review_recommended: true
  follow_up_scheduled: false
```

#### Phase-Specific Error Handling

**HARVEST Phase Failure:**

**When:** Cannot extract information from source artifacts

**Recovery:**
- Try alternative extraction methods
- Ask user for additional source locations
- Proceed with available artifacts
- Document what could not be extracted

**ANALYZE Phase Failure:**

**When:** Cannot identify structure or patterns

**Recovery:**
- Simplify analysis approach
- Focus on most obvious structures first
- Use basic patterns as fallback
- Request user input on structure

**RESTRUCTURE Phase Failure:**

**When:** Cannot organize content into template

**Recovery:**
- Try simpler template
- Organize manually
- Focus on key sections
- Accept less structured output

**VERIFY Phase Failure:**

**When:** Cannot verify accuracy or conflicts found

**Recovery:**
- Mark uncertain sections
- Document conflicts
- Request user verification
- Proceed with disclaimers

**EXTEND Phase Failure:**

**When:** Cannot add examples or extensions

**Recovery:**
- Skip examples if source insufficient
- Use generic examples where possible
- Document example gaps
- Focus on core documentation

**SYNTHESIZE Phase Failure:**

**When:** Cannot create cross-references or knowledge graph

**Recovery:**
- Create minimal cross-references
- Focus on most important links
- Skip advanced synthesis features
- Document synthesis limitations

**TRANSFORM Phase Failure:**

**When:** Cannot generate final output format

**Recovery:**
- Use simpler output format
- Generate markdown if format fails
- Provide raw structured data
- Allow user to format manually

### Error Learning Record

All HARVEST quality failures should be logged:

```yaml
harvest_failure_learning:
  iterations_completed: 5
  quality_scores: [0.75, 0.80, 0.83, 0.85, 0.87]
  final_score: 0.87
  threshold: 0.95
  root_cause: "Insufficient source material"
  recovery_action: "Documented gaps explicitly"
  lesson: "Set expectations for incomplete source scenarios"
  pattern: "Missing sources → Lower quality ceiling"
```

### See Also

- [Error Handling Protocol](error_handling_protocol.md) - Comprehensive error handling framework
- [Verification Framework](verification_framework.md) - Quality validation procedures
- [Troubleshooting Guide](../docs/TROUBLESHOOTING.md) - Common HARVEST issues

---

## Related Documentation

### Frameworks
- [R-I-S-E Framework](universal_rise.md) - For creating new systems
- [C-A-R-E Framework](universal_care.md) - For quick iterations
- [Meta-Framework](meta_framework.md) - Framework orchestration

### Supporting Systems
- [Problem Classifier](problem_classifier.md) - Selects appropriate framework
- [Verification Framework](verification_framework.md) - Quality validation
- [Knowledge Transfer](knowledge_transfer.md) - Pattern reuse

### Domain Modules
- [Murata MHC Module](../modules/murata_mhc.yaml) - Industrial automation standards
- [Web Development Module](../modules/web_development.yaml) - Web/frontend standards
- [Python Data Module](../modules/python_data.yaml) - Data science standards

---

**Document Version:** 2.0
**Created:** December 22, 2025
**Author:** CmL
**Framework:** Pliny
