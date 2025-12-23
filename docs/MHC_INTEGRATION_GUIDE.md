# MHC Development Integration Guide

> **PlinyHub Framework + MHC Developers Guide**
>
> This guide explains how to use the PlinyHub framework to enhance MHC system development.

---

## Framework Selection Matrix

| MHC Task Type | PlinyHub Framework | Iterations | Example |
|---------------|-------------------|------------|---------|
| Bug fix, typo, config change | **C-A-R-E** | 1-3 | Fix PLC timeout value |
| New feature, equipment type | **R-I-S-E** | 4-8 | Add new T-Car variant |
| Legacy code documentation | **HARVEST** | 5-10 | Document stacker dispatcher |
| Code review, refactoring | **C-A-R-E** | 2-4 | Review move creation logic |
| System debugging | **R-I-S-E** | Variable | Diagnose conveyor stalls |

---

## Loading the Murata MHC Domain Module

### Option 1: Direct Reference

```yaml
# Include in your prompt/context:
modules/murata_mhc.yaml
```

### Option 2: CLI Invocation

```bash
pliny --module murata_mhc --framework rise --task "Your task description"
```

### Module Enforced Standards

The `murata_mhc.yaml` module enforces:

| Standard | Requirement |
|----------|-------------|
| Strings | Use `cc_str` class |
| Database | Generated DRM classes |
| Logging | `ds_log()` function only |
| Transactions | `ds_exec_SP()` pattern |

---

## Framework to MHC Guide Mapping

| PlinyHub Framework | Use With These MHC Sections |
|-------------------|----------------------------|
| **C-A-R-E** | Section 3 (Problems), Section 9 (Troubleshooting) |
| **R-I-S-E** | Section 4 (Implementation Patterns), Section 16 (Modification Recipes) |
| **HARVEST** | Section 13 (Code Comment Intelligence), Section 14 (SQL Patterns) |
| **OMEGA** | Section 18 (Documentation Methodology) |

---

## Example Workflow: Adding New Equipment Type (R-I-S-E)

### Research (R)

1. Study existing equipment patterns in [Section 4](../04_Implementation_Patterns/)
2. Review [T-Car Control](../04_Implementation_Patterns/01_TCar_Control.md) as template
3. Identify database tables needed from [Section 14](../14_SQL_Pattern_Library/)

### Implement (I)

1. Create equipment stand in database (follow [16.1](../16_Modification_Recipes/01_Add_New_Equipment_Stand.md))
2. Add PLC bit mapping (follow [16.4](../16_Modification_Recipes/04_Add_New_PLC_Bit_Mapping.md))
3. Create area program using patterns from Section 4
4. Follow coding standards from [Section 2](../02_Coding_Standards/)

### Stabilize (S)

1. Test using decision trees from [Section 9](../09_Troubleshooting_Decision_Trees/)
2. Verify PLC communication with tools from [Section 6.3](../06_Testing_and_Debugging/03_Common_Tools.md)
3. Run database validation queries

### Extend (E)

1. Add documentation to Section 4
2. Update [Equipment Type Reference](../07_Quick_Reference_Guides/07_Equipment_Type_Reference.md)
3. Create troubleshooting entry in Section 9

---

## Quick Reference: Framework Phases

### C-A-R-E (Quick Fixes)

```
Context → Action → Result → Evolution
  ↓          ↓        ↓         ↓
Define    Execute  Verify   Document
```

### R-I-S-E (Features)

```
Research → Implement → Stabilize → Extend
    ↓          ↓           ↓          ↓
 Analyze    Build       Test      Enhance
```

### HARVEST (Documentation)

```
Harvest → Analyze → Restructure → Verify → Extend → Synthesize → Transform
    ↓        ↓          ↓           ↓        ↓          ↓           ↓
 Extract  Organize    Format     Validate  Expand    Connect      Publish
```

---

## Integration Checklist

Before starting any MHC development task:

- [ ] Identify task type (bug fix, feature, documentation)
- [ ] Select appropriate PlinyHub framework
- [ ] Load `murata_mhc.yaml` module
- [ ] Reference relevant MHC Guide sections
- [ ] Follow framework phases in order
- [ ] Capture learnings in OMEGA format

---

## Related Resources

- [PlinyHub Framework](https://github.com/0xPliny/pliny-framework)
- [MHC Developers Guide](https://github.com/0xPliny/MHC-Developers-Guide)
- [Layer 1: AI Brain](../00_AI_Brain_Layer_1.md) - MHC-Dev persona
- [Layer 2: System Blueprint](../01_System_Blueprint_Layer_2.md) - System relationships
