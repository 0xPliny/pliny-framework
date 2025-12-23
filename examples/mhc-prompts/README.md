# MHC/MEM Reference Folder

**Purpose:** Put this folder inside any MHC/MEM project to enable AI-assisted development.

---

## Contents

| File | Purpose | When to Use |
|------|---------|-------------|
| **PROJECT_ONBOARDING_QUESTIONNAIRE.md** | Questions AI should answer about your project | First time setting up a project |
| **AI_MASTER_PROMPT.md** | Complete system prompt for AI assistants | Copy to Claude/ChatGPT |
| **cursorrules_template.md** | Cursor-specific rules file | Copy as `.cursorrules` in project |

---

## Quick Setup (5 minutes)

### Step 1: Copy this folder to your project

```
your_project/
├── reference/           ← This folder
│   ├── README.md
│   ├── PROJECT_ONBOARDING_QUESTIONNAIRE.md
│   ├── AI_MASTER_PROMPT.md
│   └── cursorrules_template.md
└── [your code]
```

### Step 2: Have AI answer the questionnaire

1. Open `PROJECT_ONBOARDING_QUESTIONNAIRE.md`
2. Tell your AI: "Read this codebase and answer all questions in this document"
3. Save the completed answers as `PROJECT_PROFILE.md`

### Step 3: Create your rules file

1. Copy `cursorrules_template.md` to `.cursorrules` in project root
2. Paste your completed `PROJECT_PROFILE.md` at the bottom

### Step 4: Start working

The AI will now:

- Auto-classify every task
- Auto-select the right framework (R-I-S-E/C-A-R-E/HARVEST)
- Auto-apply Murata standards
- Auto-verify before completing
- Auto-capture learnings

---

## What the AI Will Do

### When you say... → The AI will

| Your Request | AI Action |
|--------------|-----------|
| "Add a new stand" | R-I-S-E: Research config, Identify dependencies, Synthesize approach, Execute with Murata standards |
| "Fix this bug" | C-A-R-E: Load Context, Analyze root cause, Respond with fix, Evaluate solution |
| "Explain how this works" | R-I-S-E Investigation or HARVEST documentation |
| "Make this faster" | C-A-R-E quick enhancement with optimization patterns |
| "Review this code" | C-A-R-E code review checking Murata standards |

### Automatic Behaviors

The AI will automatically:

- ✅ Add `// CmL [date]:` branding to all changes
- ✅ Use `cc_str` (never std::string)
- ✅ Use generated database classes (never raw SQL)
- ✅ Use `cs_log_printf` with proper log levels
- ✅ Add function entry/exit logging
- ✅ Handle all error conditions
- ✅ Offer to do related work after completing tasks

---

## The PlinyHub Framework (Summary)

```
┌───────────────┐     ┌───────────────┐     ┌───────────────┐
│   CLASSIFY    │ ──→ │   FRAMEWORK   │ ──→ │    VERIFY     │
│   Category?   │     │   Execute     │     │   Standards   │
└───────────────┘     └───────────────┘     └───────────────┘
       │                      │                    │
       ▼                      ▼                    ▼
   5 Categories:         3 Frameworks:        5 Layers:
   - CREATION            - R-I-S-E            - Formal
   - TRANSFORMATION      - C-A-R-E            - Testing
   - UNDERSTANDING       - HARVEST            - Statistical
   - REPAIR                                   - Ensemble
   - OPTIMIZATION                             - Human
```

---

## Files in Main PlinyHub

For the complete framework, see:

- `frameworks/` - Full framework documentation
- `modules/murata_mhc.yaml` - Complete Murata standards
- `templates/` - Reusable task templates
- `docs/examples/murata_example.md` - Worked example

---

## Support

If the AI isn't following Murata standards correctly:

1. Check that `.cursorrules` is in project root
2. Verify `PROJECT_PROFILE.md` was pasted into the rules
3. Remind AI: "Use Murata MHC standards - cc_str, generated classes, cs_log_printf"
