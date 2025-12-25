# PlinyHub Quick Start Guide

**Time to complete: 5 minutes**

---

## 🎯 The One Concept You Need

PlinyHub solves problems in **4 steps**:

```
CLASSIFY → FRAMEWORK → VERIFY → LEARN
```

That's it. Everything else is details.

---

## Step 1: Classify Your Problem (30 seconds)

Every problem is one of 5 types:

| Category | You want to... | Signal Words |
|----------|----------------|--------------|
| **CREATION** | Build something new | "create", "build", "implement" |
| **TRANSFORMATION** | Change something existing | "convert", "migrate", "refactor" |
| **UNDERSTANDING** | Explain or document | "explain", "analyze", "document" |
| **REPAIR** | Fix something broken | "fix", "debug", "troubleshoot" |
| **OPTIMIZATION** | Make something better | "optimize", "improve", "speed up" |

**Try it:**

```bash
pliny classify "Create a login page for my app"
# Output: Category: CREATION, Framework: R-I-S-E
```

---

## Step 2: Pick a Framework (30 seconds)

| Framework | Use When | How It Works |
|-----------|----------|--------------|
| **R-I-S-E** | Complex, unfamiliar, new creation | Research → Identify → Synthesize → Execute |
| **C-A-R-E** | Simple, familiar, iterating | Context → Analyze → Respond → Evaluate |
| **HARVEST** | Documentation tasks | Automated doc generation |

**Rule of thumb:**

- New/complex → R-I-S-E
- Quick fix/iterate → C-A-R-E
- Documentation → HARVEST

---

## Step 3: Load Domain Standards (30 seconds)

Pick the domain module that matches your work:

```bash
pliny module load web_development  # React, TypeScript, FastAPI
pliny module load murata_mhc       # VB.NET, C++, Aurora
pliny module load python_data      # pandas, sklearn, ML
pliny module load general_reasoning # Logic, decisions
```

This loads standards that will guide your work.

---

## Step 4: Execute the Framework (Most of your time)

### If using R-I-S-E

```
1. RESEARCH - What do I know? What don't I know? What do I need?
2. IDENTIFY - What patterns apply? What could go wrong?
3. SYNTHESIZE - What are my options? Which is best?
4. EXECUTE - Implement with domain standards, verify each step
```

### If using C-A-R-E

```
1. CONTEXT - What's the current state? What's the goal?
2. ANALYZE - Break it down, plan approach
3. RESPOND - Execute with standards
4. EVALUATE - Does it work? Iterate if needed
```

### Execution Engine (NEW)

For complex tasks, use the execution engine for session management and checkpointing:

```bash
# Start a session
pliny session start "Create notification filter"

# Execute with checkpointing
pliny execute --framework rise --checkpoint phase

# If something goes wrong, rollback
pliny rollback "after-research"

# Resume incomplete session
pliny session resume <session-id>
```

See [Execution Engine Guide](docs/EXECUTION_ENGINE_GUIDE.md) for details.

---

## Step 5: Verify (1 minute)

Before calling it done:

```bash
pliny verify <your-file>
```

Or manually check:

- [ ] Solves the actual problem
- [ ] All requirements met
- [ ] Standards followed
- [ ] No obvious breaks

---

## Step 6: Learn (Automatic via OMEGA)

The OMEGA Loop automatically captures what worked and what didn't.

```bash
pliny omega start  # At session start
pliny omega end    # At session end - saves learnings
```

---

## 🚀 Your First 5 Minutes

1. **State your problem clearly**

   ```
   "I need to create a notification filter component in React"
   ```

2. **Classify it**
   - Category: CREATION (building something new)
   - Domain: web_development
   - Framework: R-I-S-E (new creation)

3. **Load standards**

   ```bash
   pliny module load web_development
   ```

4. **Execute R-I-S-E**
   - **Research:** What data does it filter? What props does it need?
   - **Identify:** Similar to other filter components, need state management
   - **Synthesize:** Container + presentation split, use useMemo for filtering
   - **Execute:** Build it following TypeScript + React standards

5. **Verify**
   - Types correct? ✓
   - Tests pass? ✓
   - Accessible? ✓

---

## 📋 Cheat Sheet

```
CLASSIFY:
  CREATION      → R-I-S-E
  TRANSFORMATION → R-I-S-E  
  UNDERSTANDING → HARVEST
  REPAIR        → C-A-R-E
  OPTIMIZATION  → C-A-R-E

FRAMEWORKS:
  R-I-S-E = Research → Identify → Synthesize → Execute
  C-A-R-E = Context → Analyze → Respond → Evaluate
  HARVEST = Automated documentation

DOMAINS:
  web_development  (React, TypeScript)
  murata_mhc       (VB.NET, C++)
  python_data      (pandas, ML)
  general_reasoning (logic, decisions)

CLI:
  pliny classify "<problem>"
  pliny rise | care | harvest
  pliny verify <file>
  pliny module load <name>
```

---

## ❓ FAQ

**Q: What if I'm not sure which category?**
A: Use `pliny classify --interactive` — it will ask clarifying questions. See [Edge Case Examples](./docs/examples/edge_case_examples.md) for tricky scenarios.

**Q: What if my domain isn't listed?**
A: Use `general_reasoning` for now, or create a custom module using the template.

**Q: What if my task spans multiple domains?**
A: See [Multi-Domain Orchestration](./core/multi_domain_orchestration.md) for rules on handling cross-domain tasks.

**Q: Who is CmL?**
A: CmL is the **MHC Engineering Persona** - an AI persona that activates for `murata_mhc` domain work. Each domain has its own persona. See [Persona Clarification](./core/persona_clarification.md).

**Q: How do I know when I'm done?**
A: Run `pliny verify`. If all layers pass, you're done.

**Q: What's the OMEGA Loop?**
A: It's the self-improvement system that captures learnings. Over time, the framework gets smarter by remembering what works. Use [Learnings Template](./templates/omega/LEARNINGS_TEMPLATE.yaml) to persist learnings manually.

---

## 📚 Next Steps

- Read [README.md](README.md) for full overview
- Explore `frameworks/` for detailed methodology
- Check `modules/` for domain-specific standards
- See `cli/CLI_SPECIFICATION.md` for all commands
- **NEW:** Read [Persona Clarification](./core/persona_clarification.md) for domain-persona mapping
- **NEW:** Read [Multi-Domain Orchestration](./core/multi_domain_orchestration.md) for cross-domain tasks
- **NEW:** See [Edge Case Examples](./docs/examples/edge_case_examples.md) for tricky classification
- **NEW:** Read [Pattern Library](./docs/PATTERN_LIBRARY.md) for reusable documentation patterns
- **NEW:** See [Pattern Extraction Guide](./docs/PATTERN_EXTRACTION_GUIDE.md) to extract patterns from reference frameworks
- **NEW:** Read [Execution Engine Guide](./docs/EXECUTION_ENGINE_GUIDE.md) for session management and checkpointing
- **NEW:** See [Security Testing Guide](./docs/SECURITY_TESTING_GUIDE.md) for security assessment workflows

---

**Start with CLASSIFY. The rest follows naturally.**
