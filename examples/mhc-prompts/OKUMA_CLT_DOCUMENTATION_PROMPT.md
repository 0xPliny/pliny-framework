# OkumaCLT Complete Documentation Prompt for Cursor

## Project Overview

This prompt is designed to create comprehensive documentation for the **OkumaCLT MHC System**.

**Source Location:** `D:\ICIS\OkumaCLTDev\clogan\OkumaCLTDev`
**Runtime Location:** `D:\ICIS\OkumaCLTDev\Exec`

---

## Phase 1: Master Prompt (Use First)

Copy this into Cursor Chat with the project open:

```
You are a documentation specialist using the HARVEST methodology for the OkumaCLT MHC system.

## Your Context
@D:\ICIS\OkumaCLTDev\clogan\OkumaCLTDev\MSVC Programs\
@D:\ICIS\OkumaCLTDev\clogan\OkumaCLTDev\MSVB Programs\

## Your Identity
You are MHC-Dev, an expert in Murata Material Handling Control systems. You understand:
- C++ area programs (p_ar_*, p_cc_*, p_si_*, p_sy_*, p_ut_*)
- VB.NET UI applications (mhcMenu, dialogs)
- SQL stored procedures and database schemas
- Shared memory (StValues) architecture
- PLC communication patterns

## Task
Create a documentation structure file: `docs/DOCUMENTATION_INDEX.md`

Include:
1. **Critical Files by Priority**
   - P1: Core dispatchers (p_ar_movdp, p_ar_stkdp, p_ar_tcar)
   - P2: Communication (p_cc_hostcom, p_cc_stkcmx)
   - P3: System utilities (p_sy_shmop, p_sy_dbini)
   - P4: UI components (mhcMenu, dialogs)

2. **File Categories**
   - `/area/` - Area control programs (equipment dispatchers)
   - `/csub/` - Common C++ subroutines
   - `/dsub/` - Database subroutines
   - `/osub/` - OPC subroutines
   - `/simu/` - Simulation programs
   - `/util/` - Utility programs

3. **Documentation Template** for each file category

Do NOT document individual files yet. Just create the index structure.
```

---

## Phase 2: Area Programs (Critical - Do First)

```
Document all area programs in the `/area/` folder with comprehensive inline comments.

@D:\ICIS\OkumaCLTDev\clogan\OkumaCLTDev\MSVC Programs\area\

## For EACH .cpp file:

### Header Block
Add this header to the top of each file:
/**
 * @file [filename].cpp
 * @brief [One-line description]
 * @author Murata Machinery / Chase Logan
 * @project OkumaCLT MHC System
 * 
 * @section OVERVIEW
 * [2-3 sentence description of what this program does]
 * 
 * @section DEPENDENCIES
 * - Database tables: [list tables accessed]
 * - Shared memory: [list StValues sections]
 * - PLC signals: [list key signals]
 * 
 * @section KEY_FUNCTIONS
 * - main() - Entry point, initializes and runs dispatch loop
 * - [function_name] - [description]
 * 
 * @section RELATED_DOCS
 * - See: docs/04_Implementation_Patterns/
 * - See: MHC-Developers-Guide Section 4
 */

### Function Documentation
For every function, add:
/**
 * @brief [What the function does]
 * @param [name] [description for each parameter]
 * @return [what it returns and when]
 * 
 * @note [Any important gotchas or behavior notes]
 * @see [Related functions]
 */

### Inline Comments
Add comments every 5-10 lines explaining:
- What complex logic is doing
- Why a particular approach was taken
- Database queries being executed
- PLC signals being read/written

Start with the most critical files:
1. p_ar_movdp.cpp (Move Dispatcher)
2. p_ar_stkdp.cpp (Stacker Dispatcher)
3. p_ar_tcar.cpp (T-Car Control)
4. p_ar_fndwk.cpp (Find Work)
5. p_ar_arive.cpp (Arrival Processing)
```

---

## Phase 3: Subroutines (csub, dsub, osub)

```
Document all subroutine libraries with function-level documentation.

## For csub/ (Common Subroutines)
@D:\ICIS\OkumaCLTDev\clogan\OkumaCLTDev\MSVC Programs\csub\

Create: docs/05_Code_Reference/csub_reference.md
- List all functions with signatures
- Group by purpose (string handling, logging, utilities)
- Include example usage

## For dsub/ (Database Subroutines)
@D:\ICIS\OkumaCLTDev\clogan\OkumaCLTDev\MSVC Programs\dsub\

Create: docs/05_Code_Reference/dsub_reference.md
- List all database functions
- Document SQL patterns used
- Show ds_exec_SP usage examples
- Document DRM (Database Record Management) patterns

## For osub/ (OPC Subroutines)
@D:\ICIS\OkumaCLTDev\clogan\OkumaCLTDev\MSVC Programs\osub\

Create: docs/05_Code_Reference/osub_reference.md
- Document OPC communication functions
- List signal read/write patterns
- Document error handling
```

---

## Phase 4: SQL Documentation

```
Document all SQL stored procedures with comprehensive inline comments.

@D:\ICIS\OkumaCLTDev\clogan\OkumaCLTDev\SQL Generated Stored Procedures\

For each .sql file, add:

1. **Header Block**
-- =============================================
-- Name: [procedure_name]
-- Purpose: [what it does]
-- Called By: [list C++ programs that call this]
-- Tables: [tables read/written]
-- Parameters:
--   @param1 - [description]
--   @param2 - [description]
-- Returns: [description]
-- 
-- History:
-- [date] [author] - [change description]
-- =============================================

2. **Inline Comments** for complex logic

3. **Create Reference File**
docs/06_Database_Reference/stored_procedures.md
- Categorize by function (Move, Inventory, Equipment, Reporting)
- Include parameter documentation
- Show usage examples
```

---

## Phase 5: VB.NET UI Documentation

```
Document all VB.NET UI components.

@D:\ICIS\OkumaCLTDev\clogan\OkumaCLTDev\MSVB Programs\

## For mhcMenu:
Create: docs/08_VB_NET_UI/mhcMenu_reference.md
- Screen flow diagram
- Form descriptions
- Event handler documentation
- Database connections

## For each dialog form:
Add XML documentation comments:
''' <summary>
''' [Form description]
''' </summary>
''' <remarks>
''' Called from: [parent form]
''' Database: [tables accessed]
''' </remarks>
```

---

## Batch Processing Tips for Cursor

### Tip 1: Process One Folder at a Time

```
Document all files in @D:\ICIS\OkumaCLTDev\clogan\OkumaCLTDev\MSVC Programs\area\p_ar_movdp\

When done, say "DOCUMENTATION COMPLETE FOR p_ar_movdp - READY FOR NEXT FOLDER"
```

### Tip 2: Use Composer for Inline Comments

Select a function in the editor, then Ctrl+K:

```
Add comprehensive inline comments to this function explaining:
1. What each section does
2. Database operations being performed
3. Shared memory access patterns
4. Error handling behavior
```

### Tip 3: Generate Reference Files

```
Scan @D:\ICIS\OkumaCLTDev\clogan\OkumaCLTDev\MSVC Programs\csub\
Generate a markdown reference file listing all exported functions with:
- Function signature
- Purpose (inferred from name and usage)
- Example call pattern
Save to: docs/05_Code_Reference/csub_functions.md
```

---

## Quality Checklist

After documenting each component, verify:

- [ ] File header with purpose, author, dependencies
- [ ] All functions have docstrings
- [ ] Complex logic has inline comments
- [ ] Database tables are documented
- [ ] PLC signals are listed
- [ ] Related files are cross-referenced
- [ ] Examples provided where helpful

---

## Integration with MHC-Developers-Guide

After generating documentation, cross-reference with:

- `https://github.com/0xPliny/MHC-Developers-Guide`
- Use PlinyHub HARVEST methodology for organization
- Follow existing section numbering (00-18)

---

*Generated by PlinyHub Framework - Use with Cursor AI*
