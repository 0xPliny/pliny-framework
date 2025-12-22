# PlinyHub Persona Library

> **Specialized AI personas that integrate PlinyHub frameworks into focused specialists. Copy, paste, and transform any AI into an expert.**

---

## What is the Persona Library?

The Persona Library provides **ready-to-use AI personas** for specific tasks. Each persona is a self-contained prompt you can paste into any AI (ChatGPT, Claude, Gemini, Cursor) to get a specialist who follows PlinyHub methodology.

**Key Features:**
- 🎯 **Single-purpose focus** — Each persona excels at one thing
- 📋 **Self-contained** — No dependencies, just copy and paste
- 🔄 **Framework integration** — Built on R-I-S-E, C-A-R-E, HARVEST
- ✅ **Quality assured** — Confidence Protocol + Meta-Prompting built in
- 🔗 **Chainable** — Personas work together for complex workflows

---

## Available Personas

| Persona | Specialty | Framework | Best For |
|---------|-----------|-----------|----------|
| **[Atlas](atlas.md)** | Deep Research | HARVEST-R | Comprehensive research with sources, confidence, and gap analysis |
| **[Sage](sage.md)** | Architecture Design | R-I-S-E + ToT | System design with trade-off analysis and multiple approaches |
| **[Scribe](scribe.md)** | Documentation | HARVEST + Meta | Technical writing for any audience with self-critique |

---

## Quick Comparison

| Aspect | Atlas | Sage | Scribe |
|--------|-------|------|--------|
| **Primary Question** | "What do we know about X?" | "How should we build X?" | "How do we explain X?" |
| **Input** | Research question | Requirements | Subject to document |
| **Output** | Sourced analysis | Architecture design | Documentation |
| **Key Strength** | Finding & synthesizing information | Exploring design options | Making complex things clear |
| **Time Investment** | Medium-High | High | Medium |

---

## How to Use a Persona

### Method 1: Full Activation (Recommended)

1. Open any AI chat (ChatGPT, Claude, Gemini, Cursor)
2. Copy the **entire** persona file content
3. Paste it as your first message
4. The AI will respond with the persona's welcome message
5. Start working with your specialist!

### Method 2: Quick Reference

Reference personas inline in Cursor or Claude:

```
@Atlas DEEP technical — "Best practices for microservices authentication"
@Sage FULL — "Design a notification filtering system"
@Scribe COMPREHENSIVE Tutorial — "How to use the MHC crane API"
```

### Method 3: Persona Chaining

For complex projects, chain personas together:

```
1. @Atlas researches: "Notification system patterns and best practices"
2. @Sage designs: Architecture based on Atlas findings
3. @Scribe documents: API reference and tutorials for the system
```

---

## What Each Persona Inherits

Every persona automatically integrates these PlinyHub protocols:

| Protocol | What It Does | Inherited By |
|----------|--------------|--------------|
| **Confidence Protocol** | 1-10 confidence scores with reasoning | All personas |
| **Meta-Prompting** | Self-critique before finalizing | All personas |
| **Assumption Tracker** | Explicit assumptions with risk levels | All personas |
| **Quality Gates** | Checklist verification before delivery | All personas |

---

## Operating Modes

Each persona supports multiple modes for different needs:

| Persona | Full Mode | Quick Mode |
|---------|-----------|------------|
| **Atlas** | DEEP: 10+ sources, full analysis, ~2000 words | QUICK: 3-5 sources, summary, ~800 words |
| **Sage** | FULL: Complete architecture, 3+ approaches, ~3000 words | SKETCH: High-level design, ~800 words |
| **Scribe** | COMPREHENSIVE: All sections, multiple examples | CONCISE: Essentials only, ~800 words |

---

## Persona Selection Guide

### Use Atlas When:
- ✅ You need to understand a topic thoroughly
- ✅ You want sourced information with confidence levels
- ✅ You're making a decision and need facts
- ✅ You want contradictions and gaps identified

### Use Sage When:
- ✅ You're designing a new system
- ✅ You need to compare multiple approaches
- ✅ You want explicit trade-off analysis
- ✅ You need architecture diagrams and component specs

### Use Scribe When:
- ✅ You need to document existing code/systems
- ✅ You're writing for a specific audience
- ✅ You want working code examples
- ✅ You need various doc types (README, API, Tutorial)

---

## Example Workflows

### Research → Design → Document

```
Step 1: Atlas
"DEEP technical — What are the best practices for real-time notification systems?"

Step 2: Sage  
"FULL — Design a notification system based on these findings: [paste Atlas output]"

Step 3: Scribe
"COMPREHENSIVE API Docs — Document this notification system: [paste Sage output]"
```

### Rapid Prototyping

```
Step 1: Sage (SKETCH mode)
"SKETCH — Quick architecture for a REST API gateway"

Step 2: Scribe (CONCISE mode)  
"CONCISE README — Document this gateway for developers"
```

### Deep Dive

```
Step 1: Atlas (DEEP mode)
"DEEP academic — Research on event-driven architecture patterns"

Step 2: Sage (FULL mode)
"FULL — Design an event-driven system for IoT sensors using these patterns"

Step 3: Scribe (COMPREHENSIVE mode)
"COMPREHENSIVE Architecture doc — Full documentation for this system"
```

---

## Creating Custom Personas

Use this template to create your own PlinyHub-integrated persona:

```markdown
# [Persona Name] - [Specialty]

> **[One-line description]**

---

## Paste This Entire Section Into Any AI

---

You are **[Name]**, a [specialty] specialist. You [what you do] using [methodology].

## Your Identity

You are [description] who:
- [Trait 1]
- [Trait 2]
- [Trait 3]

**Mission Statement:** "[Quote encapsulating purpose]"

## Your Methodology: [Name]

### Phase 1: [Name]
[Details]

### Phase 2: [Name]
[Details]

[Continue phases...]

## Operating Modes

### [Full Mode Name]
[Requirements]

### [Quick Mode Name]
[Requirements]

## Output Requirements

Every response must include:
1. [Requirement 1]
2. [Requirement 2]
...

## Confidence Protocol Integration
[How to apply confidence scoring]

## Welcome Message
[Greeting with examples]

## Example Output Format
[Template]

## Quality Gates
[Checklist]
```

---

## Planned Personas

Future additions to the library:

| Persona | Specialty | Status |
|---------|-----------|--------|
| **Forge** | Code Implementation | Planned |
| **Scout** | Debugging & Investigation | Planned |
| **Cipher** | Security Analysis | Planned |
| **Mentor** | Teaching & Onboarding | Planned |

---

## Integration with PlinyHub

The Persona Library is part of the larger PlinyHub framework:

```
PlinyHub/
├── frameworks/          ← Methodologies (R-I-S-E, C-A-R-E, HARVEST)
├── core/               ← Enhancement layers (Confidence, Meta-Prompting)
├── modules/            ← Domain standards (MHC, Web, Python)
├── personas/           ← YOU ARE HERE
│   ├── README.md       
│   ├── atlas.md        ← Deep Research
│   ├── sage.md         ← Architecture Design
│   └── scribe.md       ← Documentation
└── templates/          ← Reusable templates
```

---

## Quick Reference

```
Atlas → Research   → "I need to understand [topic]"
Sage  → Design     → "Design a system that [requirements]"
Scribe → Document → "Document [subject] for [audience]"

Modes:
  Atlas:  DEEP (comprehensive) | QUICK (overview)
  Sage:   FULL (complete)      | SKETCH (high-level)
  Scribe: COMPREHENSIVE        | CONCISE
```

---

## Contributing

To contribute new personas:

1. Use the template above
2. Ensure integration with Confidence Protocol
3. Include Meta-Prompting self-critique
4. Provide welcome message with examples
5. Submit PR to PlinyHub repository

---

*Part of the PlinyHub Framework — https://github.com/0xPliny/pliny-framework*
