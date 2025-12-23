# PlinyHub Autonomous Agent - Quick Start

**Goal:** Minimal input, maximum automation.

---

## ONE-TIME SETUP

1. Copy `AUTONOMOUS_BOOTSTRAP.md` to your AI assistant
2. That's it.

---

## DAILY USAGE

### Start a Session

```
Bootstrap project: [NAME]
Directory: [PATH]
```

Example:

```
Bootstrap project: Aurora ASRS
Directory: D:\ICIS\Aurora
```

The AI will:

1. Explore the codebase (2-3 min)
2. Detect domain and patterns
3. Load appropriate standards
4. Report what it found
5. Wait for tasks

---

### Give Tasks

Just say what you want. No special formatting needed.

```
"Fix the pallet allocation bug"
"Add a new stand for the conveyor"
"Explain how the tracking filter works"
"Make the allocation query faster"
"Document the PLC communication code"
```

The AI will automatically:

- Classify (CREATION/REPAIR/OPTIMIZATION/etc.)
- Select framework (R-I-S-E or C-A-R-E)
- Apply domain standards
- Verify before completing
- Suggest related work

---

### That's It

No more:

- ❌ Copy-pasting prompts
- ❌ Remembering standards
- ❌ Manual framework selection
- ❌ Checking if AI followed rules

The agent handles everything.

---

## INPUT REQUIRED FROM YOU

| What | Example | Frequency |
|------|---------|-----------|
| Project name | "Aurora ASRS" | Once per session |
| Directory | "D:\ICIS\Aurora" | Once per session |
| Task | "Fix the bug" | Each task |

Everything else is automatic.

---

## WHAT THE AI DOES

```
INPUT: "Fix the pallet allocation bug"

AI AUTOMATICALLY:
├─ Classifies as REPAIR
├─ Selects C-A-R-E framework
├─ Loads murata_mhc standards
├─ Searches codebase for allocation code
├─ Analyzes root cause
├─ Proposes fix using cc_str, generated classes, cs_log_printf
├─ Verifies standards compliance
├─ Offers to fix similar issues elsewhere
└─ Captures learning for next time
```

---

## FILES IN THIS FOLDER

| File | Purpose | Action |
|------|---------|--------|
| **AUTONOMOUS_BOOTSTRAP.md** | The agent brain | Copy to AI once |
| PROJECT_ONBOARDING_QUESTIONNAIRE.md | Manual version (backup) | Reference only |
| AI_MASTER_PROMPT.md | Detailed standards | Auto-loaded by agent |
| cursorrules_template.md | For Cursor specifically | Copy as .cursorrules |

---

## QUICK COMMANDS

Once bootstrapped, these work:

```
"What are the key files?"      → Shows critical files
"What standards apply?"        → Lists required/forbidden
"Search for [pattern]"         → Finds code matching pattern
"Fix [issue]"                  → C-A-R-E execution
"Add [feature]"                → R-I-S-E execution
"Explain [code]"               → Analysis and documentation
"What should I do next?"       → AI suggests based on codebase
```

---

**The goal: You think about WHAT to do. The AI handles HOW.**
