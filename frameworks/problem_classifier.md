# Enhanced Problem Classifier

**Version:** 2.0
**Purpose:** Automatically classify ANY problem with confidence scoring

---

## Overview

The Enhanced Problem Classifier uses a 4-step classification system with confidence scores. It asks clarifying questions when confidence is low.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    ENHANCED CLASSIFICATION PIPELINE                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  Step 1: UNIVERSAL CATEGORY                                                  │
│          ├── CREATION                                                       │
│          ├── TRANSFORMATION                                                 │
│          ├── UNDERSTANDING                                                  │
│          ├── REPAIR                                                         │
│          └── OPTIMIZATION                                                   │
│                    │                                                        │
│                    ▼                                                        │
│  Step 2: DOMAIN                                                             │
│          ├── murata_mhc                                                     │
│          ├── web_development                                                │
│          ├── python_data                                                    │
│          ├── research_analysis                                              │
│          └── general_reasoning                                              │
│                    │                                                        │
│                    ▼                                                        │
│  Step 3: FRAMEWORK                                                          │
│          ├── R-I-S-E (complex, unfamiliar)                                  │
│          ├── C-A-R-E (iterative, familiar)                                  │
│          └── HARVEST (documentation)                                        │
│                    │                                                        │
│                    ▼                                                        │
│  Step 4: COMPLEXITY                                                         │
│          ├── Simple (1-2 steps)                                             │
│          ├── Moderate (3-5 steps)                                           │
│          └── Complex (6+ steps)                                             │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## Step 1: Universal Problem Taxonomy (5 Categories)

These categories work for ANY domain—not just code.

| Category | Definition | Signal Words | Examples |
|----------|------------|--------------|----------|
| **CREATION** | Building something new from requirements | "create", "build", "implement", "design", "make", "develop" | "Create a login page", "Build a report" |
| **TRANSFORMATION** | Converting existing thing to new form | "convert", "migrate", "refactor", "port", "translate", "adapt" | "Migrate to TypeScript", "Refactor this class" |
| **UNDERSTANDING** | Analyzing/explaining existing thing | "explain", "analyze", "document", "research", "study", "investigate" | "Explain this code", "Research best practices" |
| **REPAIR** | Fixing broken/suboptimal thing | "fix", "debug", "troubleshoot", "resolve", "repair", "correct" | "Fix this bug", "Why isn't this working?" |
| **OPTIMIZATION** | Improving working thing | "optimize", "improve", "enhance", "speed up", "reduce", "streamline" | "Make this faster", "Reduce memory usage" |

### Category Detection Logic

```python
def detect_category(problem_text: str) -> tuple[str, float]:
    """Returns (category, confidence)"""
    
    signals = {
        "CREATION": ["create", "build", "implement", "design", "make", "develop", "new", "add"],
        "TRANSFORMATION": ["convert", "migrate", "refactor", "port", "translate", "change", "move"],
        "UNDERSTANDING": ["explain", "analyze", "document", "research", "why", "how", "understand"],
        "REPAIR": ["fix", "debug", "bug", "error", "broken", "not working", "troubleshoot", "issue"],
        "OPTIMIZATION": ["optimize", "improve", "faster", "better", "reduce", "enhance", "performance"]
    }
    
    scores = {}
    for category, words in signals.items():
        score = sum(1 for word in words if word.lower() in problem_text.lower())
        scores[category] = score
    
    if max(scores.values()) == 0:
        return ("CREATION", 0.5)  # Default with low confidence
    
    best_category = max(scores, key=scores.get)
    confidence = min(0.95, 0.5 + (scores[best_category] * 0.15))
    
    return (best_category, confidence)
```

---

## Step 2: Domain Detection

| Domain | File Signals | Keyword Signals | Context Signals |
|--------|--------------|-----------------|-----------------|
| **murata_mhc** | `.vb`, `.cpp`, `.h` | cc_str, cs_log, Aurora, crane, palletizer, ASRS | ICIS paths, DBINI.CNF |
| **web_development** | `.tsx`, `.ts`, `.jsx`, `.js`, `.css` | React, component, API, frontend, Next.js | package.json, node_modules |
| **python_data** | `.py`, `.ipynb` | pandas, numpy, dataframe, model, analysis | requirements.txt, jupyter |
| **research_analysis** | Any | hypothesis, study, literature, findings, methodology | Academic language |
| **general_reasoning** | None specific | decide, compare, evaluate, plan, strategy | No clear technical domain |

### Domain Detection Logic

```python
def detect_domain(problem_text: str, context: dict) -> tuple[str, float]:
    """Returns (domain, confidence)"""
    
    # Check file extensions in context
    if context.get("files"):
        extensions = [f.split(".")[-1] for f in context["files"]]
        if any(ext in ["vb", "cpp", "h"] for ext in extensions):
            return ("murata_mhc", 0.9)
        if any(ext in ["tsx", "ts", "jsx"] for ext in extensions):
            return ("web_development", 0.85)
        if any(ext in ["py", "ipynb"] for ext in extensions):
            return ("python_data", 0.8)
    
    # Check keywords
    murata_keywords = ["cc_str", "cs_log", "aurora", "crane", "mhc", "icis"]
    web_keywords = ["react", "component", "typescript", "api", "frontend"]
    python_keywords = ["pandas", "numpy", "dataframe", "jupyter", "model"]
    
    text_lower = problem_text.lower()
    
    if any(kw in text_lower for kw in murata_keywords):
        return ("murata_mhc", 0.9)
    if any(kw in text_lower for kw in web_keywords):
        return ("web_development", 0.85)
    if any(kw in text_lower for kw in python_keywords):
        return ("python_data", 0.8)
    
    # Default to general reasoning
    return ("general_reasoning", 0.6)
```

---

## Step 3: Framework Selection

### Category → Framework Mapping

| Category | Primary Framework | Secondary Framework | Selection Logic |
|----------|------------------|---------------------|-----------------|
| **CREATION** | R-I-S-E | C-A-R-E (for iterations) | New = R-I-S-E; Simple = C-A-R-E |
| **TRANSFORMATION** | R-I-S-E | C-A-R-E (for refinement) | Complex migration = R-I-S-E |
| **UNDERSTANDING** | HARVEST | R-I-S-E (for research) | Documentation = HARVEST |
| **REPAIR** | C-A-R-E | R-I-S-E (if root cause unclear) | Quick fix = C-A-R-E |
| **OPTIMIZATION** | C-A-R-E | R-I-S-E (if major redesign) | Incremental = C-A-R-E |

### Framework Selection Logic

```python
def select_framework(category: str, complexity: str, domain_familiar: bool) -> tuple[str, float]:
    """Returns (framework, confidence)"""
    
    # Default mappings
    mappings = {
        "CREATION": "R-I-S-E",
        "TRANSFORMATION": "R-I-S-E",
        "UNDERSTANDING": "HARVEST",
        "REPAIR": "C-A-R-E",
        "OPTIMIZATION": "C-A-R-E"
    }
    
    framework = mappings.get(category, "R-I-S-E")
    confidence = 0.85
    
    # Adjustments based on complexity
    if category in ["CREATION", "TRANSFORMATION"]:
        if complexity == "simple" and domain_familiar:
            framework = "C-A-R-E"
            confidence = 0.8
    
    if category == "REPAIR":
        if complexity == "complex" or not domain_familiar:
            framework = "R-I-S-E"
            confidence = 0.75
    
    return (framework, confidence)
```

---

## Step 4: Complexity Assessment

| Level | Signals | Typical Step Count | Time Estimate |
|-------|---------|-------------------|---------------|
| **Simple** | Single action, clear goal, familiar pattern | 1-2 steps | < 15 minutes |
| **Moderate** | Multiple steps, some unknowns, known domain | 3-5 steps | 15-60 minutes |
| **Complex** | Many unknowns, cross-cutting concerns, new domain | 6+ steps | 60+ minutes |

### Complexity Indicators

```yaml
simple_indicators:
  - "quick"
  - "just"
  - "simple"
  - "only"
  - Single file mentioned
  - Specific location given

moderate_indicators:
  - Multiple files mentioned
  - "should" or "need to"
  - Some uncertainty expressed
  - Known domain but new feature

complex_indicators:
  - "not sure"
  - "investigate"
  - "figure out"
  - Multiple systems mentioned
  - Cross-cutting concerns
  - New domain
  - "architecture" or "design"
```

---

## Confidence Scoring

Each classification step produces a confidence score (0.0 - 1.0).

```yaml
classification:
  category: "CREATION"
  category_confidence: 0.92
  
  domain: "web_development"
  domain_confidence: 0.87
  
  framework: "R-I-S-E"
  framework_confidence: 0.95
  
  complexity: "moderate"
  complexity_confidence: 0.78
  
  overall_confidence: 0.88  # Geometric mean
  
  clarification_needed: false
  clarification_question: null
```

### Overall Confidence Calculation

```python
from math import prod

def calculate_overall_confidence(confidences: list[float]) -> float:
    """Geometric mean of all confidence scores"""
    return prod(confidences) ** (1/len(confidences))
```

---

## Clarifying Questions

When confidence is low (< 0.7), ask targeted questions.

### Category Uncertainty (category_confidence < 0.7)

```
"I'm not sure if you want to:
 A) CREATE something new
 B) TRANSFORM something existing
 C) FIX something broken
 D) OPTIMIZE something working

Which best describes your goal?"
```

### Domain Uncertainty (domain_confidence < 0.7)

```
"I detected signals for multiple domains. Which is primary?
 A) Murata MHC (VB.NET, C++, Aurora)
 B) Web Development (React, TypeScript)
 C) Python/Data Science
 D) General reasoning/analysis"
```

### Framework Uncertainty (framework_confidence < 0.7)

```
"This could be approached with:
 A) R-I-S-E - Thorough research first, then implement
 B) C-A-R-E - Quick iterations with feedback loops

Do you prefer comprehensive or iterative?"
```

### Complexity Uncertainty (complexity_confidence < 0.7)

```
"How complex do you expect this to be?
 A) Simple - Quick fix, 1-2 steps
 B) Moderate - Several steps, some unknowns
 C) Complex - Investigation needed, many parts"
```

---

## Complete Classification Output

```yaml
classification_result:
  # Input
  problem_statement: "Create a React component for filtering notifications by priority"
  context:
    files: ["src/components/", "package.json"]
    recent_changes: ["Added notification model"]
  
  # Step 1: Category
  category: "CREATION"
  category_confidence: 0.92
  category_signals: ["create", "component"]
  
  # Step 2: Domain
  domain: "web_development"
  domain_confidence: 0.95
  domain_signals: ["React", "component", ".tsx"]
  
  # Step 3: Framework
  framework: "R-I-S-E"
  framework_confidence: 0.85
  framework_rationale: "New creation in familiar domain"
  
  # Step 4: Complexity
  complexity: "moderate"
  complexity_confidence: 0.80
  complexity_signals: ["filtering", "priority", "state"]
  
  # Overall
  overall_confidence: 0.88
  clarification_needed: false
  
  # Next Action
  recommended_first_step: "Research notification data structure and filtering requirements"
  estimated_time: "30-45 minutes"
```

---

## CLI Integration

```bash
# Full classification with explanation
pliny classify "Create a React component for filtering notifications"
# Output:
# Category: CREATION (92% confidence)
# Domain: web_development (95% confidence)
# Framework: R-I-S-E (85% confidence)
# Complexity: moderate (80% confidence)
# Overall confidence: 88%
# First step: Research notification structure

# Interactive mode (asks clarifying questions)
pliny classify --interactive

# Quick classification (minimal output)
pliny classify --quick

# Classification with context
pliny classify "Fix the bug" --context ./src/components/NotificationList.tsx
```

---

## Learning from Classifications

The classifier improves over time by learning from corrections.

```yaml
classification_history:
  - id: "cls-001"
    timestamp: "2025-12-20T14:30:00Z"
    problem: "Refactor the authentication module"
    
    predicted:
      category: "CREATION"
      category_confidence: 0.65
      
    actual:
      category: "TRANSFORMATION"
      
    correct: false
    
    lesson: "'Refactor' is a strong TRANSFORMATION signal, even when mixed with other signals"
    adjustment: "Increase weight of 'refactor' keyword for TRANSFORMATION"
```

---

## Quick Reference

```
CATEGORY SIGNALS:
  CREATION      → create, build, implement, design, new
  TRANSFORMATION → refactor, migrate, convert, port, change
  UNDERSTANDING  → explain, analyze, document, research
  REPAIR        → fix, debug, bug, error, not working
  OPTIMIZATION  → optimize, improve, faster, reduce

DOMAIN SIGNALS:
  murata_mhc     → .vb, .cpp, cc_str, cs_log, Aurora
  web_development → .tsx, React, component, API
  python_data    → .py, pandas, numpy, dataframe
  general        → No clear technical signals

FRAMEWORK SELECTION:
  Complex/New    → R-I-S-E
  Simple/Iterate → C-A-R-E
  Documentation  → HARVEST
  
LOW CONFIDENCE (< 0.7):
  → Ask clarifying question
  → Don't guess
```
