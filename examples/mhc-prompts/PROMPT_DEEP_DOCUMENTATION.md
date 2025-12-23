# DEEP DOCUMENTATION GENERATION PROMPT

You are acting as the Lead Technical Writer for the AuroDev MHC project. Your task is to perform a deep-dive analysis of the core C++ and VB libraries and generate comprehensive documentation that fills the current gaps.

## 1. SOURCE CODE LOCATIONS
You have access to the following source directories. READ THESE FILES directly to generate the documentation. Do not hallucinate content.

- **OSUB (Operation Subroutines):**
  `D:\ICIS\AuroDev\clogan\AuroDev\MSVC Programs\osub`
  *Key files to analyze:* `sys.cpp/h`, `movs.cpp/h`, `stk.cpp/h`, `load.cpp/h`

- **CCSUB (Common Control Subroutines):**
  `D:\ICIS\AuroDev\clogan\AuroDev\Base\trunk\MSVC Programs\ccsub`
  *Key files to analyze:* `cc_stk.cpp/h`, `cc_mudp.cpp/h`, `cc_sys.cpp/h`, `cc_vehicle.cpp/h`

- **CSUB (Common Subroutines):**
  Distributed across:
  - `D:\ICIS\AuroDev\clogan\AuroDev\MSVC Programs\csub`
  - `D:\ICIS\AuroDev\clogan\AuroDev\Base\trunk\MSVC Programs\ccsub` (Mixed with CCSUB)
  *Key files to analyze:* `cs_log.cpp/h`, `cs_msg.cpp/h`, `cc_str.cpp/h`, `cs_reg.cpp/h`

- **ICISDefines:**
  `D:\ICIS\AuroDev\clogan\AuroDev\MSVB Programs\dilg\mhcMenu\ICISDefines.vb`

- **global_prm:**
  `D:\ICIS\AuroDev\clogan\AuroDev\MSVC Programs\incl\global_prm.h`

## 2. EXECUTION PHASES

### Phase 1: Deep Analysis
For each library group (OSUB, CCSUB, CSUB), perform the following:
1.  **List all classes/functions** exposed in the header files (.h).
2.  **Analyze the implementation** in the source files (.cpp) to understand the logic.
3.  **Map dependencies**: What does this library call? Who calls it?

### Phase 2: Documentation Generation
Create or update the corresponding Markdown files in `docs/03_Code_Reference/03_Shared_Libraries/`.
- `dsub.md` (Update existing with full signatures)
- `osub.md` (Create new)
- `ccsub.md` (Create new)
- `csub.md` (Create new)
- `ICISDefines.md` (Create new)
- `global_prm.md` (Create new)

**Required Format for Each Function/Class:**
```markdown
### `FunctionName` / `ClassName`
**Signature:**
`void FunctionName(int param1, char* param2)`

**Description:**
A detailed explanation of what the function does, including business logic and side effects.

**Parameters:**
- `param1` (int): Description of parameter, valid range.
- `param2` (char*): Description of parameter.

**Return Values:**
- `GP.GOOD` (0): Success.
- `GP.BAD` (-1): Failure.
- `SQL.HELD` (-2): Record locked.

**Logic Flow:**
1. Step 1 of logic.
2. Step 2 of logic.
3. Error handling behavior.

**Dependencies:**
- Calls: `ds_movs.load()`, `cs_log_printf()`
- Tables: `MOVS`, `LOCN`

**Usage Example:**
```cpp
// Example code snippet
if (FunctionName(1, "test") != GP.GOOD) {
    return;
}
```
```

### Phase 3: Integration
1.  Update `docs/03_Code_Reference/03_Shared_Libraries/00_Shared_Libraries_Index.md` to link to all new files.
2.  Ensure cross-references exist to `04_Database_Reference` tables where applicable.

## 3. RULES
- **Accuracy is Paramout:** If you don't see it in the code, do not document it.
- **Use Standard constants:** Use `GP.GOOD`, `CS_LOG_ERROR` in examples.
- **Traceability:** Mention which source file (.cpp/.h) the documentation comes from.

