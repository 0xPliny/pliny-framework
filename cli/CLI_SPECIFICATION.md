# Pliny CLI - Complete Command Reference

**Version:** 2.0
**Purpose:** Command-line interface for the PlinyHub framework

---

## Overview

The Pliny CLI provides automation for:

- Problem classification
- Framework execution
- Learning management (OMEGA Loop)
- Domain module management
- Solution verification
- Metrics and analytics

---

## Installation

```bash
# Clone framework
git clone https://github.com/yourorg/plinyhub.git
cd plinyhub

# Install dependencies
npm install

# Make CLI available globally
npm link

# Verify installation
pliny --version
```

---

## Command Reference

### Classification Commands

```bash
# ─────────────────────────────────────────────────────────────────────────────
# pliny classify - Classify a problem
# ─────────────────────────────────────────────────────────────────────────────

# Full classification with explanation
pliny classify "<problem description>"

# Example:
pliny classify "Create a React component for filtering notifications"
# Output:
# ┌─────────────────────────────────────────────────────┐
# │ CLASSIFICATION RESULT                               │
# ├─────────────────────────────────────────────────────┤
# │ Category:   CREATION              Confidence: 92%  │
# │ Domain:     web_development       Confidence: 95%  │
# │ Framework:  R-I-S-E               Confidence: 85%  │
# │ Complexity: moderate              Confidence: 80%  │
# ├─────────────────────────────────────────────────────┤
# │ Overall Confidence: 88%                            │
# │ First Step: Research notification structure        │
# │ Estimated Time: 30-45 minutes                      │
# └─────────────────────────────────────────────────────┘

# Interactive mode - asks clarifying questions
pliny classify --interactive

# Quick classification (minimal output)
pliny classify --quick "<problem>"
# Output: CREATION | web_development | R-I-S-E | moderate

# With context from files
pliny classify "<problem>" --context ./src/components/
```

---

### Framework Execution Commands

```bash
# ─────────────────────────────────────────────────────────────────────────────
# pliny rise - Execute R-I-S-E framework  
# ─────────────────────────────────────────────────────────────────────────────

pliny rise "<problem description>"
# Starts R-I-S-E with guided prompts:
# Phase 1: RESEARCH - What do you already know? What's missing?
# Phase 2: IDENTIFY - What patterns apply? What could go wrong?
# Phase 3: SYNTHESIZE - What are your options? Which is best?
# Phase 4: EXECUTE - Implement with domain standards

# Start from specific phase
pliny rise "<problem>" --phase identify

# With domain module
pliny rise "<problem>" --domain web_development

# ─────────────────────────────────────────────────────────────────────────────
# pliny care - Execute C-A-R-E iteration cycle
# ─────────────────────────────────────────────────────────────────────────────

pliny care "<problem description>"
# Starts C-A-R-E iteration loop:
# Phase 1: CONTEXT - Load state, understand goal
# Phase 2: ANALYZE - Decompose, plan approach
# Phase 3: RESPOND - Execute with standards
# Phase 4: EVALUATE - Check quality, iterate if needed

# Set iteration limit
pliny care "<problem>" --max-iterations 5

# ─────────────────────────────────────────────────────────────────────────────
# pliny harvest - Execute HARVEST documentation loop
# ─────────────────────────────────────────────────────────────────────────────

pliny harvest <file>
# Runs HARVEST documentation automation on file

# Options:
pliny harvest <file> --output docs/output.md
pliny harvest <file> --quality 0.95
pliny harvest <file> --max-iterations 5
pliny harvest <file> --format markdown|html|rst
```

---

### OMEGA Loop Commands

```bash
# ─────────────────────────────────────────────────────────────────────────────
# pliny omega - Self-improvement master loop
# ─────────────────────────────────────────────────────────────────────────────

# Start OMEGA tracking for session
pliny omega start
# Output: OMEGA loop started. Session ID: abc-123-def

# Check current OMEGA state
pliny omega status
# Output:
# Session: abc-123-def
# Duration: 45 minutes
# Phase: GENERATE
# Quality so far: 0.92

# Manually trigger learning capture
pliny omega learn
# Output: Captured 3 patterns, 1 anti-pattern from current session

# Export learnings to file
pliny omega export [filename]
# Output: Exported 12 learning records to learnings_2025-12-20.yaml

# Import learnings from file
pliny omega import <filename>
# Output: Imported 47 learning records

# End session and save learnings
pliny omega end
# Output: Session ended. Learnings saved. Error rate reduced by 12%
```

---

### Learning System Commands

```bash
# ─────────────────────────────────────────────────────────────────────────────
# pliny learn - Cross-session learning management
# ─────────────────────────────────────────────────────────────────────────────

# Export all learnings to YAML file
pliny learn export [file]
# Output: Saved 47 learning records to ~/.pliny/learnings/2025-12-20.yaml

# Import learnings from file
pliny learn import <file>
# Output: Loaded 12 learning records from archive.yaml

# Show accumulated learnings
pliny learn show
# Output:
# 47 learning records across 5 domains
# Top patterns:
#   1. Container/Presentation Split (14 uses, 95% success)
#   2. Early Validation Pattern (12 uses, 92% success)
# Common failures:
#   1. Premature optimization (7 occurrences)
#   2. Missing edge cases (5 occurrences)

# Show learnings for specific domain
pliny learn show --domain murata_mhc
# Output:
# 23 learning records for murata_mhc
# Success rate: 94%
# Avg iterations: 2.3

# Apply relevant learnings to current problem
pliny learn apply "<problem description>"
# Output:
# Found 5 relevant learnings:
# 1. [Container/Presentation Split] - 92% relevance
# 2. [Avoid: Premature Optimization] - 87% relevance
# 3. [Early Validation Pattern] - 84% relevance

# Search learnings
pliny learn search "<query>"
# Output: 3 matching records found

# Get statistics
pliny learn stats
# Output:
# Total records: 47
# By category: CREATION(15), REPAIR(12), OPTIMIZATION(10), TRANSFORMATION(6), UNDERSTANDING(4)
# By domain: murata_mhc(23), web(14), python(7), general(3)
# Success rate: 91%
# Avg quality: 0.94
# Avg iterations: 2.7
```

---

### Meta-Framework Commands

```bash
# ─────────────────────────────────────────────────────────────────────────────
# pliny genesis - Framework creation (Layer 3)
# ─────────────────────────────────────────────────────────────────────────────

# Start new framework creation wizard
pliny genesis new
# Guides through:
# 1. Identify gap in existing frameworks
# 2. Design phases and structure
# 3. Define quality gates
# 4. Validate on test problems
# 5. Integrate into system

# Validate a framework definition
pliny genesis validate <framework-file>
# Output: Framework valid. All required fields present.

# Test framework against a problem
pliny genesis test <framework-file> "<problem>"
# Output: Framework applied successfully. Quality: 0.89

# ─────────────────────────────────────────────────────────────────────────────
# pliny orchestrate - Multi-framework coordination (Layer 2)
# ─────────────────────────────────────────────────────────────────────────────

pliny orchestrate "<complex problem>"
# Decomposes problem and coordinates multiple frameworks:
# Output:
# Decomposed into 4 sub-problems:
#   SP-1: Design API (R-I-S-E)
#   SP-2: Implement backend (C-A-R-E)
#   SP-3: Build frontend (R-I-S-E → C-A-R-E)
#   SP-4: Document (HARVEST)
# Execution order: SP-1 → [SP-2, SP-3 parallel] → SP-4
```

---

### Domain Module Commands

```bash
# ─────────────────────────────────────────────────────────────────────────────
# pliny module - Domain module management
# ─────────────────────────────────────────────────────────────────────────────

# List available modules
pliny module list
# Output:
# murata_mhc       - Murata Material Handling Control (VB.NET, C++)
# web_development  - React, TypeScript, FastAPI
# python_data      - Python, pandas, ML/Data Science
# general_reasoning - Logic, decisions, analysis

# Load a domain module
pliny module load <name>
# Output: Loaded murata_mhc module (23 standards, 4 quality gates)

# Show currently loaded module
pliny module show
# Output: Currently loaded: web_development v1.0
# Standards: 12 required, 8 forbidden, 6 recommended
# Quality gates: completeness (0.95), accuracy (0.98), consistency (0.90)

# Validate a module definition
pliny module validate <file>
# Output: Module valid. All fields correctly defined.

# Interactive module creation wizard
pliny module create
# Guides through creating a new domain module
```

---

### Verification Commands

```bash
# ─────────────────────────────────────────────────────────────────────────────
# pliny verify - Solution verification
# ─────────────────────────────────────────────────────────────────────────────

# Standard verification (Layers 1-3)
pliny verify <file>
# Output:
# Layer 1 (Formal): PASS (0 errors, 0 warnings)
# Layer 2 (Testing): PASS (24/24 tests, 87% coverage)
# Layer 3 (Statistical): PASS (no regression)
# VERIFIED ✓

# Quick verification (Layers 1-2 only)
pliny verify --quick <file>

# Full verification (Layers 1-5)
pliny verify --full <file>
# Includes ensemble verification and human review prompt

# Verify with specific domain standards
pliny verify <file> --domain murata_mhc

# Generate verification report
pliny verify <file> --report
# Outputs detailed YAML report

# Check specific layer only
pliny verify <file> --layer 2
```

---

### Standards Checking Commands

```bash
# ─────────────────────────────────────────────────────────────────────────────
# pliny check - Standards enforcement
# ─────────────────────────────────────────────────────────────────────────────

# Check file against loaded domain standards
pliny check <file>
# Output:
# Checking against web_development standards...
# ✓ WEB-REQ-001: TypeScript types present
# ✓ WEB-REQ-002: Error handling present
# ✗ WEB-REQ-003: Missing ARIA labels (line 45)
# 
# 2/3 standards passed
# Fix suggestions:
#   Line 45: Add aria-label to button element

# Check against specific domain
pliny check <file> --domain murata_mhc

# Check multiple files
pliny check src/**/*.ts

# Auto-fix where possible
pliny check <file> --fix
```

---

### Template Commands

```bash
# ─────────────────────────────────────────────────────────────────────────────
# pliny template - Template management
# ─────────────────────────────────────────────────────────────────────────────

# List available templates
pliny template list
# Output:
# rise/
#   documentation.md - R-I-S-E documentation template
#   feature.md - R-I-S-E feature development template
# care/
#   iteration.md - C-A-R-E iteration template
#   bugfix.md - C-A-R-E bug fix template
# harvest/
#   legacy-code.md - HARVEST legacy documentation template

# Apply a template
pliny template apply <name>

# Create template from current work
pliny template create --from <file> --name <template-name>
```

---

### Cycle Tracking Commands

```bash
# ─────────────────────────────────────────────────────────────────────────────
# pliny cycle - Pliny Cycle project tracking
# ─────────────────────────────────────────────────────────────────────────────

# Start Pliny Cycle tracking for project
pliny cycle start "<project name>"
# Output: Pliny Cycle started for "Notification System"
# Current phase: PLAN

# Show current cycle status
pliny cycle status
# Output:
# Project: Notification System
# Phase: IMPLEMENT (3/6)
# Progress: 45%
# Quality: 0.91

# Advance to next phase
pliny cycle advance
# Output: Advanced to REVIEW phase

# Mark cycle complete
pliny cycle complete
# Output: Cycle completed. Creating summary...
```

---

### Metrics Commands

```bash
# ─────────────────────────────────────────────────────────────────────────────
# pliny metrics - Framework effectiveness metrics
# ─────────────────────────────────────────────────────────────────────────────

# Show framework effectiveness metrics
pliny metrics show
# Output:
# Framework Usage (last 30 days):
#   R-I-S-E: 23 uses, 91% success, avg 2.3 iterations
#   C-A-R-E: 45 uses, 94% success, avg 1.8 iterations
#   HARVEST: 12 uses, 97% success, avg 1.2 iterations
#
# Quality Trends:
#   Completeness: 94% (↑3% from last month)
#   Accuracy: 96% (↑2% from last month)
#
# Time Savings:
#   Documentation: 56x faster with HARVEST
#   Standards checks: 240x faster automated

# Export metrics to file
pliny metrics export [file]

# Reset metrics (with confirmation)
pliny metrics reset
```

---

### Configuration Commands

```bash
# ─────────────────────────────────────────────────────────────────────────────
# pliny config - Configuration management
# ─────────────────────────────────────────────────────────────────────────────

# Show current configuration
pliny config show
# Output:
# default_domain: web_development
# quality_threshold: 0.95
# max_iterations: 5
# data_path: ~/.pliny/

# Set configuration value
pliny config set <key> <value>
# Example: pliny config set default_domain murata_mhc

# Reset to defaults
pliny config reset
```

---

### Help Commands

```bash
# ─────────────────────────────────────────────────────────────────────────────
# pliny help - Get help
# ─────────────────────────────────────────────────────────────────────────────

# General help
pliny help
pliny --help

# Help for specific command
pliny help classify
pliny classify --help

# Show version
pliny --version
```

---

## Quick Reference Card

```
CLASSIFY:    pliny classify "<problem>"
FRAMEWORKS:  pliny rise | care | harvest
OMEGA:       pliny omega start | learn | end
LEARN:       pliny learn show | apply | search
GENESIS:     pliny genesis new | validate | test
MODULES:     pliny module list | load | create
VERIFY:      pliny verify <file> [--quick | --full]
CHECK:       pliny check <file> [--fix]
METRICS:     pliny metrics show | export
```

---

## Environment Variables

```bash
PLINY_DATA_PATH    # Data storage location (default: ~/.pliny/)
PLINY_DOMAIN       # Default domain module
ANTHROPIC_API_KEY  # API key for HARVEST engine
PLINY_QUALITY      # Default quality threshold (0.0-1.0)
PLINY_LOG_LEVEL    # Logging level (debug, info, warn, error)
```
