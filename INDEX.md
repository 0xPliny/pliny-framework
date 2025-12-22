# ClaudeHub - Command Center
**Created:** December 20, 2025
**Location:** C:\Users\clogan\Documents\ClaudeHub
**Purpose:** Central hub for D: drive development and AI-assisted workflows

---

## 📑 Quick Navigation

### 🗺️ Exploration Reports
- [D: Drive Exploration Report](./D_DRIVE_EXPLORATION.md) - Complete map of D: drive systems

### 🎯 Active Projects (ICIS Development)
Located in `D:\ICIS\`

| Project | Path | Last Updated |
|---------|------|--------------|
| Aurora AS/RS | D:\ICIS\AuroDev | Dec 19, 2025 |
| FTBC NC | D:\ICIS\FTBC_NCDev | Nov 30, 2025 |
| Okuma CLT | D:\ICIS\OkumaCLTDev | Dec 16, 2025 |
| WSR-TI | D:\ICIS\WSR-TIDev | Dec 19, 2025 |
| CatNC | D:\ICIS\CatNCDev | Dec 15, 2025 |
| CLT MHC | D:\ICIS\CLT_MHCDev | Nov 17, 2025 |
| Dart TX | D:\ICIS\DartTXDev | Dec 14, 2025 |
| Eaton MKE | D:\ICIS\EatonMKEDev | Dec 8, 2025 |
| Estoh | D:\ICIS\EstohDev | Dec 15, 2025 |
| Fast Dhub | D:\ICIS\Fast-DhubDev | Nov 28, 2025 |
| Fast IUnit | D:\ICIS\FastIUnitDev | Dec 15, 2025 |
| Fast Uhub | D:\ICIS\Fast-UhubDev | Dec 15, 2025 |

### 📚 Production Systems
Located in `D:\`

| System | Path | Purpose |
|--------|------|---------|
| CLT MHC | D:\CLT_MHC | CLT Material Handling Control |
| FTBC NC | D:\FTBC_NC | FTBC NC System |
| Okuma CLT | D:\OkumaCLT | Okuma CLT System |
| WSR-TI | D:\WSR-TI | WSR-TI System |

### 📖 Documentation Central
Key documentation locations:

#### D:\Reference\
- [README.md](D:\Reference\README.md) - Murata CursorAI Prompt Pack
- [Patrick_Coding_Style_Guide.md](D:\Reference\Patrick_Coding_Style_Guide.md) - Coding standards
- [MASTER_CURSOR_PROMPT.md](D:\Reference\MASTER_CURSOR_PROMPT.md) - Master AI prompt
- [MHC_Context_Comprehensive_Max_Detail.md](D:\Reference\MHC_Context_Comprehensive_Max_Detail.md) - 213 KB context
- [persona_engineer.md](D:\Reference\persona_engineer.md) - Engineer persona
- [persona_analyst.md](D:\Reference\persona_analyst.md) - Analyst persona
- [persona_documenter.md](D:\Reference\persona_documenter.md) - Documenter persona

#### D:\Pliny\
- System documentation (Aurora, Auro, FTBC_NC)
- AI frameworks and tools
- Implementation guides
- Analysis reports

### 🤖 AI Tools & Prompts
Located in `D:\Pliny\` and `D:\Reference\`

#### Frameworks
- **R-I-S-E Framework** - Research, Identify, Synthesize, Execute
- **C-A-R-E Framework** - Context, Analysis, Response, Evaluation
- **HARVEST Loop** - Automated documentation synthesis

#### Core Framework Documentation (NEW)
- [Persona Clarification](./core/persona_clarification.md) - **NEW** - Domain-persona mapping and CmL identity
- [Multi-Domain Orchestration](./core/multi_domain_orchestration.md) - **NEW** - Rules for cross-domain tasks

#### Templates (NEW)
- [Learnings Template](./templates/omega/LEARNINGS_TEMPLATE.yaml) - **NEW** - Persist learnings across sessions

#### Examples (NEW)
- [Edge Case Examples](./docs/examples/edge_case_examples.md) - **NEW** - Non-obvious classification scenarios

#### 🎭 Persona Library (NEW)
Specialized AI personas that integrate PlinyHub frameworks:

| Persona | Specialty | Framework | Use Case |
|---------|-----------|-----------|----------|
| **[Atlas](./personas/atlas.md)** | Deep Research | HARVEST-R | Comprehensive research with sources |
| **[Sage](./personas/sage.md)** | Architecture | R-I-S-E + ToT | System design with trade-off analysis |
| **[Scribe](./personas/scribe.md)** | Documentation | HARVEST + Meta | Technical writing for any audience |

See [Persona Library README](./personas/README.md) for usage guide.

#### Domain Personas
- **CmL (Engineer)** - Senior Murata MHC engineer (see [Persona Clarification](./core/persona_clarification.md))
- **Analyst** - System analysis persona
- **Documenter** - Documentation specialist

#### Prompt Collections
- Cursor AI Enhanced Prompts
- Claude Code System Prompts
- Master Cursor Prompt Pack

---

## 🛠️ Murata MHC Standards Quick Reference

### String Operations
```cpp
// ✅ CORRECT
cc_str.copy(dest, src);
cc_str.comp(str1, str2);
cc_str.cat(dest, src);

// ❌ WRONG
strcpy(dest, src);
strcmp(str1, str2);
strcat(dest, src);
```

### Database Access
```vb
' ✅ CORRECT - Use generated classes
Dim hstin As New z_hstin
hstin.load_by_pk(host_id)

' ❌ WRONG - Raw SQL
Dim rs As ADODB.Recordset
rs.Open("SELECT * FROM hstin WHERE...")
```

### Logging
```cpp
// ✅ CORRECT
cs_log_printf(CS_LOG_ERROR, "Component: Error message");

// ❌ WRONG
printf("Error: %s\n", msg);
cout << "Error: " << msg << endl;
```

### Configuration
```cpp
// ✅ CORRECT
cs_reg_read("section", "key", value);
// Or load from DBINI.CNF / elements table

// ❌ WRONG
hardcoded_value = "C:\\Path\\To\\File";
```

### Return Codes
```vb
' ✅ CORRECT
Return GP.GOOD  ' Success
Return GP.BAD   ' Error
Return SQL.HELD ' Database lock

' ❌ WRONG
Return True
Return -1
Throw New Exception("Error")
```

---

## 🎯 Common Tasks

### Starting a New Feature
1. Review existing patterns in relevant system
2. Check D:\Reference\ for coding standards
3. Use Cursor with MASTER_CURSOR_PROMPT.md
4. Follow DECOMPOSE → REUSE → STANDARDS → ITERATE

### Code Review Checklist
- [ ] Uses cc_str for all string operations
- [ ] Uses generated classes for database access
- [ ] Uses cs_log_printf for logging
- [ ] Loads config from registry/DBINI
- [ ] Uses standard return codes
- [ ] Follows MHC naming conventions
- [ ] Comments use "CmL MM/DD/YYYY:" format
- [ ] Looks human-written (not AI-obvious)

### Documentation Tasks
1. Use HARVEST loop for automated doc generation
2. Reference existing docs in D:\Pliny\
3. Follow established documentation patterns
4. Include gap analysis when appropriate

### System Analysis
1. Use persona_analyst.md for guidance
2. Review existing analysis docs in D:\Pliny\
3. Create comprehensive understanding docs
4. Perform gap analysis

---

## 🔗 External Resources

### Version Control
- CatNCDev uses Mercurial (.hg)
- Location: D:\ICIS\CatNCDev\.hg\

### Database Backups
- CLT_MHC: D:\CLT_MHC\Database Backup\
- FTBC_NC: D:\FTBC_NC\Database Backups\
- OkumaCLT: D:\OkumaCLT\Database Backup\
- WSR-TI: D:\WSR-TI\Database Backup\

### Logs
All systems have \Logs\ directories for troubleshooting

---

## 📊 System Statistics

- **Total Systems:** 17 (4 production, 13 development)
- **Documentation Files:** 30+
- **Total Documentation:** ~800 KB
- **Active Projects:** 13 in ICIS
- **Latest Activity:** Dec 20, 2025

---

## 🚀 Power User Tips

### Quick Access Commands
```bash
# Jump to development
cd /d/ICIS/AuroDev

# View recent changes
ls -lt /d/ICIS/*/  | head -20

# Search all documentation
grep -r "keyword" /d/Pliny/*.md /d/Reference/*.md

# Count code files
find /d/ICIS -name "*.vb" -o -name "*.cpp" | wc -l
```

### AI Workflow
1. Load appropriate persona from D:\Reference\
2. Attach relevant system docs from D:\Pliny\
3. Apply Murata standards automatically
4. Use HARVEST for documentation
5. Iterate with R-I-S-E framework

---

## 📅 Recent Activity

**Dec 20, 2025:**
- Created ClaudeHub
- Completed D: drive exploration
- Documented all systems

**Dec 19, 2025:**
- AuroDev activity
- WSR-TIDev updates
- Pliny documentation updates
- Reference updates

---

## 🎯 Next Actions

- [ ] Create system relationship map
- [ ] Extract code snippet library
- [ ] Build automation scripts
- [ ] Set up project monitoring
- [ ] Organize prompt library
- [ ] Create learning paths from docs

---

**Maintained By:** Claude Code
**Last Updated:** December 20, 2025
**Version:** 1.0

---

*Your neural command center is operational.*
