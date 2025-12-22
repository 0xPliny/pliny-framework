# Multi-Domain Orchestration

**Version:** 1.0  
**Created:** December 22, 2025  
**Purpose:** Rules for handling tasks spanning multiple domains

---

## Overview

When a task spans multiple domains (e.g., MHC backend + React frontend), this guide specifies how to handle domain precedence and standard conflicts.

---

## Domain Precedence Rules

### Rule 1: Primary Domain = Where Core Logic Lives

The **primary domain** is determined by where the core business logic resides:

| Task Type | Primary Domain | Secondary Domain |
|-----------|----------------|------------------|
| MHC REST API consumed by React | murata_mhc | web_development |
| React dashboard displaying MHC data | web_development | murata_mhc |
| Python script processing MHC logs | python_data | murata_mhc |
| Documentation for MHC web interface | murata_mhc | web_development |
| Data analysis of web app metrics | python_data | web_development |
| Strategic decision about MHC architecture | general_reasoning | murata_mhc |

### Rule 2: Standards Application Order

1. **Apply primary domain standards first** (non-negotiable rules)
2. **Apply secondary domain standards** where they don't conflict
3. **If conflict exists:** Primary domain wins

### Rule 3: Multi-Domain Classification Output

When classifying a multi-domain task, output should include:

```yaml
classification:
  category: "CREATION"
  primary_domain: "murata_mhc"
  primary_confidence: 0.85
  secondary_domain: "web_development"
  secondary_confidence: 0.75
  framework: "R-I-S-E"
  orchestration_mode: "multi-domain"
```

---

## Examples

### Example 1: Build REST API for Crane Status (MHC + Web)

**Task:** "Create a REST API endpoint that returns crane status for a React dashboard"

**Classification:**
- Primary: `murata_mhc` (crane data comes from MHC system)
- Secondary: `web_development` (API will be consumed by React)

**Standards Applied:**

1. **MHC Standards (Primary):**
   - Use `z_*` generated classes to query crane status
   - Use `cs_log_printf` for logging
   - Return `GP.GOOD`/`GP.BAD` internally
   
2. **Web Standards (Secondary):**
   - Return JSON response format
   - Include proper HTTP status codes
   - Add CORS headers for React consumption

**Result:** API uses MHC patterns internally but exposes web-friendly interface.

---

### Example 2: React Dashboard for MHC Monitoring (Web + MHC)

**Task:** "Build a React dashboard that displays real-time MHC system status"

**Classification:**
- Primary: `web_development` (React is the core technology)
- Secondary: `murata_mhc` (data comes from MHC)

**Standards Applied:**

1. **Web Standards (Primary):**
   - Use TypeScript with proper types
   - Components have JSDoc comments
   - ARIA labels for accessibility
   
2. **MHC Standards (Secondary):**
   - Understand MHC data structures
   - Display GP.GOOD/GP.BAD as user-friendly status
   - Use MHC terminology in UI labels

---

### Example 3: Python Script Analyzing MHC Logs (Python + MHC)

**Task:** "Write a Python script to analyze cs_log files and find error patterns"

**Classification:**
- Primary: `python_data` (Python is the implementation)
- Secondary: `murata_mhc` (understanding MHC log format)

**Standards Applied:**

1. **Python Standards (Primary):**
   - Use pandas for data analysis
   - Type hints on all functions
   - Proper exception handling
   
2. **MHC Standards (Secondary):**
   - Understand cs_log format
   - Recognize GP.GOOD/GP.BAD patterns
   - Know MHC equipment naming conventions

---

## Conflict Resolution

When standards conflict, use this decision tree:

```
Is the conflict about DATA FORMAT?
├── YES → Primary domain wins (it owns the data)
└── NO → Continue

Is the conflict about CODE STYLE?
├── YES → Primary domain wins (it's the implementation language)
└── NO → Continue

Is the conflict about NAMING CONVENTIONS?
├── YES → Use primary domain internally, secondary domain at boundaries
└── NO → Continue

Is the conflict about ERROR HANDLING?
├── YES → Map between domains at boundaries
│         (e.g., GP.BAD → HTTP 500 at API boundary)
└── NO → Ask for clarification
```

---

## Integration Points

At domain boundaries (where primary meets secondary), create explicit mapping:

```
MHC Internal          API Boundary          Web Consumer
─────────────────────────────────────────────────────────
GP.GOOD          →    { status: 200 }   →   "Success"
GP.BAD           →    { status: 500 }   →   "Error"
SQL.HELD         →    { status: 409 }   →   "Conflict"
z_crane_status   →    JSON object       →   TypeScript interface
cs_log entry     →    Log API response  →   Console/UI display
```

---

## Boundary Mapping Templates

### MHC to REST API Mapping

```vb
' VB.NET REST Controller Example
' CmL 12/22/2025: MHC to REST boundary mapping

<HttpGet("crane/{craneId}/status")>
Public Function GetCraneStatus(craneId As String) As IActionResult
    ' MHC internal (primary domain standards)
    Dim crane As New z_cranes
    crane.crane_id = craneId
    Dim rc = crane.load_by_pk()
    
    ' Boundary mapping (primary → secondary)
    Select Case rc
        Case GP.GOOD
            ' Map MHC data to JSON response
            Return Ok(New With {
                .craneId = crane.crane_id,
                .status = MapStatusToFriendly(crane.status),
                .lastUpdate = crane.last_update
            })
        Case SQL.NOTFOUND
            Return NotFound(New With {.error = "Crane not found"})
        Case Else
            _logger.LogError("GetCraneStatus: Failed for {0}, rc={1}", craneId, rc)
            Return StatusCode(500, New With {.error = "Internal error"})
    End Select
End Function

Private Function MapStatusToFriendly(mhcStatus As String) As String
    ' Map MHC status codes to user-friendly strings
    Select Case mhcStatus
        Case "R" : Return "Ready"
        Case "B" : Return "Busy"
        Case "E" : Return "Error"
        Case "M" : Return "Maintenance"
        Case Else : Return "Unknown"
    End Select
End Function
```

### TypeScript Interface for MHC Data

```typescript
// Web frontend (secondary domain) consuming MHC API
// TypeScript interface matching MHC data structure

interface CraneStatus {
  craneId: string;
  status: 'Ready' | 'Busy' | 'Error' | 'Maintenance' | 'Unknown';
  lastUpdate: string;
}

interface ApiError {
  error: string;
}

// Fetch with proper error handling
async function getCraneStatus(craneId: string): Promise<CraneStatus> {
  const response = await fetch(`/api/crane/${craneId}/status`);
  
  if (!response.ok) {
    const error: ApiError = await response.json();
    throw new Error(error.error);
  }
  
  return response.json();
}
```

---

## When to Escalate to Layer 2 (Orchestration)

Multi-domain tasks should escalate to Layer 2 when:

1. **More than 2 domains involved** - Need formal decomposition
2. **Significant code in both domains** - Not just boundary mapping
3. **Standards conflict cannot be resolved** - Need explicit trade-off decision
4. **Dependencies are complex** - Circular or multi-way dependencies

---

## Quick Reference

```
MULTI-DOMAIN CLASSIFICATION:
1. Identify all domains touched by the task
2. Determine which domain owns the CORE LOGIC → Primary
3. Other domains are Secondary
4. Apply Primary standards first, Secondary where non-conflicting
5. Create explicit boundary mappings

DOMAIN PRECEDENCE ORDER:
  Where data lives → Primary
  Where logic runs → Primary
  Where UI renders → Primary
  Consuming/displaying → Secondary

CONFLICT RESOLUTION:
  Data format → Primary wins
  Code style → Primary wins
  Naming → Primary internal, Secondary at boundaries
  Errors → Map at boundaries
```

---

## Related Documentation

- [Problem Classifier](../frameworks/problem_classifier.md) - Single-domain classification
- [Meta Framework](../frameworks/meta_framework.md) - Layer 2 orchestration
- [Domain Modules](../modules/) - Domain-specific standards

---

**Document Version:** 1.0  
**Author:** CmL  
**Framework:** PlinyHub

