# PlinyHub Persona Library

> **Specialized AI personas that integrate PlinyHub frameworks into focused specialists.**

## What is the Persona Library?

The Persona Library provides **ready-to-use AI personas** for specific tasks. Each persona is a self-contained prompt you can paste into any AI (ChatGPT, Claude, Gemini, Cursor) to get a specialist who follows PlinyHub methodology.

---

## Available Personas

| Persona | Specialty | Framework | Use Case |
|---------|-----------|-----------|----------|
| **[Atlas](atlas.md)** | Deep Research | HARVEST-R | Comprehensive research with sources |
| **[Sage](sage.md)** | Architecture Design | R-I-S-E + ToT | System design with trade-off analysis |
| **[Scribe](scribe.md)** | Documentation | HARVEST + Meta | Technical writing for any audience |

---

## How to Use a Persona

1. Open any AI chat (ChatGPT, Claude, Gemini, Cursor)
2. Copy the entire persona file content
3. Paste it as your first message
4. The AI will respond with the persona's welcome message
5. Start working with your specialist!

---

## What Each Persona Inherits

Every persona automatically integrates:

| Protocol | Purpose |
|----------|---------|
| **Confidence Protocol** | 1-10 confidence scores on all outputs |
| **Meta-Prompting** | Self-critique before finalizing |
| **Assumption Tracker** | Explicit assumptions with risk levels |
| **Framework Integration** | Uses appropriate PlinyHub framework |

---

## Persona Operating Modes

Each persona supports multiple modes for different needs:

| Persona | Full Mode | Quick Mode |
|---------|-----------|------------|
| **Atlas** | 10+ sources, full citations | 3-5 sources, summary |
| **Sage** | Complete architecture doc | High-level sketch |
| **Scribe** | Comprehensive documentation | Concise essentials |

---

## Creating Custom Personas

Use this template to create your own:

```markdown
# [Persona Name] - [Specialty]

## Identity
[Who this persona is and what they're expert at]

## Methodology
[Which PlinyHub framework they use and how]

## Operating Modes
[Different levels of depth/detail]

## Output Requirements
[What every response must include]

## Welcome Message
[Greeting with examples of how to use]
```

---

## Quick Reference

```
Atlas → Research questions → "I need to understand [topic]"
Sage  → System design     → "Design a system that [requirements]"
Scribe → Documentation   → "Document [subject] for [audience]"
```
