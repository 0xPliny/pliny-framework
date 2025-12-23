# QUICK WINS: ICISDefines and global_prm Documentation

## OBJECTIVE
Create comprehensive documentation for the two single-file libraries that are currently undocumented. These are critical for understanding constants, return codes, and global parameters used throughout the MHC system.

---

## TARGET 1: ICISDefines.vb

### Source File Location
`D:\ICIS\AuroDev\clogan\AuroDev\MSVB Programs\dilg\mhcMenu\ICISDefines.vb`

### Output File
`D:\ICIS\AuroDev\03_Code_Reference\03_Shared_Libraries\ICISDefines.md`

### Required Content
1. **All Public Constants** - List every constant with its value and purpose
2. **Return Codes** - Document GP.GOOD, GP.BAD, SQL.HELD, SQL.NOTFOUND, etc.
3. **Equipment Type Codes** - Stacker, AGV, RTNX, Station identifiers
4. **Status Codes** - Move statuses, load statuses, location statuses
5. **Error Codes** - Numeric error codes and their meanings
6. **Message Types** - Host message types, internal message types
7. **Categorization** - Group constants by category with clear headers

### Template
```markdown
# ICISDefines (System Constants)

**Document Version:** 1.0
**Last Updated:** 2024-12-23
**Author:** PlinyHub HARVEST
**Confidence Score:** 0.95
**Source File:** `MSVB Programs\dilg\mhcMenu\ICISDefines.vb`

---

## Overview
Central repository of all system constants, return codes, and enumeration values used throughout the Auro MHC system.

---

## Return Codes

| Constant | Value | Description | Usage |
|----------|-------|-------------|-------|
| GP.GOOD | 0 | Success | All functions |
| GP.BAD | -1 | Failure | All functions |
| SQL.HELD | -2 | Record locked | Database operations |
| SQL.NOTFOUND | 100 | Record not found | Database operations |

---

## Equipment Type Codes

| Constant | Value | Description |
|----------|-------|-------------|
| ... | ... | ... |

---

## Move Status Codes

| Constant | Value | Description |
|----------|-------|-------------|
| ... | ... | ... |

(Continue for all categories...)
```

---

## TARGET 2: global_prm.h

### Source File Location
`D:\ICIS\AuroDev\clogan\AuroDev\MSVC Programs\incl\global_prm.h`

### Output File
`D:\ICIS\AuroDev\03_Code_Reference\03_Shared_Libraries\global_prm.md`

### Required Content
1. **Structure Definition** - The global_prm struct with all fields
2. **Field Documentation** - Each field's purpose, data type, and valid values
3. **Initialization** - How/when global_prm is initialized
4. **Access Pattern** - How to read/write global parameters
5. **Configuration Source** - Where values come from (DBINI.CNF, registry, etc.)

### Template
```markdown
# global_prm (Global Parameters)

**Document Version:** 1.0
**Last Updated:** 2024-12-23
**Author:** PlinyHub HARVEST
**Confidence Score:** 0.95
**Source File:** `MSVC Programs\incl\global_prm.h`

---

## Overview
Global parameter structure containing system-wide configuration values loaded at startup.

---

## Structure Definition

```cpp
struct global_prm {
    // Exact structure from source file
};
```

---

## Field Reference

| Field | Type | Description | Source | Default |
|-------|------|-------------|--------|---------|
| ... | ... | ... | ... | ... |

---

## Access Pattern

```cpp
// How to access global parameters
extern global_prm g_prm;
int value = g_prm.field_name;
```

---

## Configuration Sources

| Field | Loaded From | Key/Section |
|-------|-------------|-------------|
| ... | DBINI.CNF | ... |
| ... | Registry | ... |
| ... | Elements Table | ... |
```

---

## EXECUTION STEPS

1. **Read** the source file at the specified path
2. **Extract** all constants, structures, and definitions
3. **Categorize** by type (return codes, equipment types, statuses, etc.)
4. **Document** each with value, description, and usage context
5. **Create** the markdown file at the output path
6. **Update** `00_Shared_Libraries_Index.md` to include links to new files

---

## RULES
- Extract EVERY constant - do not skip any
- Use exact values from the source code
- Group related constants together
- Include usage examples where helpful
- Cross-reference with database tables and processes that use these constants

