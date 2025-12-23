# MHC/MEM Project Onboarding Questionnaire

**Purpose:** Answer these questions about any MHC/MEM project to enable AI-assisted development using the PlinyHub framework.

---

## HOW TO USE

1. **Copy this entire document** to your AI assistant (Cursor, Claude, etc.)
2. **Point the AI at the project codebase** you want to evaluate
3. **Have the AI answer all questions** below
4. **Save the completed questionnaire** as `PROJECT_PROFILE.md` in the project
5. **Use the Auto-Prompt section** at the end to self-direct any task

---

# SECTION 1: PROJECT IDENTITY

## 1.1 Basic Information

- **Project Name:**
- **Project Location (path):**
- **Customer/Site:**
- **System Type:** (e.g., Aurora ASRS, Palletizer, Conveyor, Crane, etc.)
- **Primary Language(s):** (VB.NET, C++, C#, SQL, etc.)
- **Database:** (SQL Server version, database name)

## 1.2 Project Structure

- **Source root directory:**
- **Key subdirectories and their purposes:**
  - `/src/` →
  - `/config/` →
  - `/sql/` →
  - Other:

## 1.3 Version Control

- **Repository location:**
- **Main branch name:**
- **Branching strategy:**

---

# SECTION 2: ARCHITECTURE DISCOVERY

## 2.1 Entry Points

- **Main executable(s):**
- **Service(s):**
- **Startup sequence:**

## 2.2 Core Components

List the major components/modules and their responsibilities:

| Component | File(s) | Purpose | Dependencies |
|-----------|---------|---------|--------------|
| | | | |
| | | | |
| | | | |

## 2.3 Database Schema

- **Key tables and their purposes:**

| Table | Purpose | Key Relationships |
|-------|---------|-------------------|
| | | |
| | | |

- **Generated class location (DAL):**
- **How to regenerate DAL classes:**

## 2.4 Configuration Files

| File | Purpose | Key Settings |
|------|---------|--------------|
| DBINI.CNF | | |
| stands.xml | | |
| dcbdef_*.cnf | | |
| Other: | | |

## 2.5 External Integrations

| System | Integration Type | Protocol | Location |
|--------|------------------|----------|----------|
| PLC | | OPC | |
| WMS | | | |
| Other | | | |

---

# SECTION 3: CODE PATTERNS & STANDARDS

## 3.1 Existing Patterns

Answer for what's ACTUALLY in this codebase:

- **String handling:** (cc_str, std::string, CString, etc.)
- **Logging:** (cs_log_printf, other)
- **Database access:** (Generated classes, raw SQL, ADO, etc.)
- **Error handling:** (Return codes, exceptions, both)
- **Naming conventions:** (Describe patterns you see)

## 3.2 Standards Compliance

Check which Murata standards are followed:

- [ ] Uses `cc_str` for string operations
- [ ] Uses generated database classes (z_*, C*)
- [ ] Uses `cs_log_printf` with proper log levels
- [ ] Uses standard return codes (GP.GOOD, GP.BAD, SQL.HELD)
- [ ] Uses proper CmL/Murata branding in comments
- [ ] Has function entry/exit logging
- [ ] Has error condition handling

## 3.3 Non-Standard Code

List any code that DOESN'T follow Murata standards:

| File | Issue | Severity |
|------|-------|----------|
| | | |

---

# SECTION 4: OPERATIONAL KNOWLEDGE

## 4.1 Equipment & Stands

- **Equipment types in this system:**
- **Stand numbering scheme:**
- **Critical stands/equipment:** (which ones matter most)

## 4.2 Process Flows

Describe the main material handling flows:

**Flow 1: [Name]**

```
[Start] → [Step 1] → [Step 2] → [End]
```

**Flow 2: [Name]**

```
[Start] → [Step 1] → [Step 2] → [End]
```

## 4.3 PLC Integration

- **PLC manufacturer:**
- **Communication method:**
- **Key bit definitions:**
- **DCB files location:**

---

# SECTION 5: DEVELOPMENT CONTEXT

## 5.1 Build Process

- **How to build:**
- **Build output location:**
- **Dependencies to install:**

## 5.2 Testing

- **How to run tests:**
- **Test data location:**
- **Simulation mode:**

## 5.3 Deployment

- **How to deploy:**
- **Target environment:**
- **Rollback procedure:**

## 5.4 Common Tasks

Based on code analysis, what are typical development tasks?

| Task Type | Frequency | Example |
|-----------|-----------|---------|
| Add new stand | Common | |
| Modify PLC bit | Common | |
| Fix allocation bug | Common | |
| Add new report | Occasional | |
| Other: | | |

---

# SECTION 6: KNOWN ISSUES & HISTORY

## 6.1 Known Issues

| Issue | Severity | Location | Workaround |
|-------|----------|----------|------------|
| | | | |

## 6.2 Recent Changes

| Date | Change | Files Affected | Why |
|------|--------|----------------|-----|
| | | | |

## 6.3 Technical Debt

| Debt Item | Priority | Effort | Impact |
|-----------|----------|--------|--------|
| | | | |

---

# SECTION 7: AI CONTEXT

## 7.1 Critical Files

Files the AI should ALWAYS be aware of:

| File | Why Critical |
|------|--------------|
| | |

## 7.2 Danger Zones

Files/areas to be EXTRA careful with:

| Location | Risk | Required Care |
|----------|------|---------------|
| | | |

## 7.3 Helpful Hints

Things that would help an AI work on this project:

1.
2.
3.

---

# AUTO-PROMPT SECTION

## When asked to work on this project, use this prompt

```
I am working on the [PROJECT_NAME] MHC/MEM project.

PROJECT CONTEXT:
- System Type: [SYSTEM_TYPE]
- Primary Languages: [LANGUAGES]
- Database: [DATABASE]
- Source Location: [SOURCE_PATH]

KEY FILES:
[List from Section 7.1]

STANDARDS TO FOLLOW:
- Use cc_str for all string operations
- Use generated database classes (z_*, C*) for all DB access
- Use cs_log_printf with appropriate LOG levels
- Return GP.GOOD/GP.BAD/SQL.HELD as appropriate
- Add CmL branding with date to all changes
- Include function entry/exit logging

CURRENT TASK: [DESCRIBE YOUR TASK]

Using the PlinyHub framework:
1. CLASSIFY this task (CREATION/TRANSFORMATION/UNDERSTANDING/REPAIR/OPTIMIZATION)
2. SELECT the appropriate framework (R-I-S-E for complex, C-A-R-E for simple/fix)
3. APPLY Murata MHC standards throughout
4. VERIFY against quality gates before completing
5. CAPTURE learnings for future tasks

Begin by classifying this task and selecting the appropriate framework.
```

---

# QUICK REFERENCE GENERATED FROM ANSWERS

After completing the questionnaire, generate this quick reference:

```markdown
# [PROJECT_NAME] Quick Reference

## In 30 Seconds
- **What:** [System type] for [Customer]
- **Where:** [Source path]
- **Language:** [Primary language]
- **Database:** [DB name]

## Key Commands
- Build: [command]
- Test: [command]
- Deploy: [command]

## Before Any Change
1. Check standards: [checklist items that apply]
2. Critical files: [list]
3. Danger zones: [list]

## Common Tasks → Templates
- Add stand → [template]
- Fix bug → [template]
- Add report → [template]
```
