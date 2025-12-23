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

## Conflict Resolution Protocol

When standards from multiple domains conflict, use this comprehensive decision protocol:

### Conflict Resolution Decision Tree

```
Standards Conflict Detected
    │
    ├─→ Conflict about DATA FORMAT?
    │   └─→ YES: Primary domain wins (it owns the data)
    │       Rationale: Data format determined by data owner
    │       Example: MHC uses z_* classes (primary), not web API formats
    │
    ├─→ Conflict about CODE STYLE?
    │   └─→ YES: Primary domain wins (it's the implementation language)
    │       Rationale: Code style follows implementation language
    │       Example: Python script (primary) uses Python style, not MHC VB.NET style
    │
    ├─→ Conflict about NAMING CONVENTIONS?
    │   └─→ YES: Use primary domain internally, secondary domain at boundaries
    │       Rationale: Internal consistency with primary, external compatibility with secondary
    │       Example: MHC internal uses snake_case, API boundary uses camelCase
    │
    ├─→ Conflict about ERROR HANDLING?
    │   └─→ YES: Map between domains at boundaries
    │       Rationale: Each domain uses its standards internally, map at interfaces
    │       Example: GP.BAD (MHC) → HTTP 500 (Web) at API boundary
    │
    ├─→ Conflict about LOGGING?
    │   └─→ YES: Use primary domain logging internally, map at boundaries
    │       Rationale: Logging follows implementation domain
    │       Example: cs_log_printf in MHC code, console.log in JavaScript code
    │
    ├─→ Conflict about CONFIGURATION?
    │   └─→ YES: Primary domain configuration internally, expose via secondary format at boundary
    │       Rationale: Configuration follows primary domain, expose in secondary format for consumers
    │       Example: Registry/DBINI internally, JSON config API for web consumers
    │
    └─→ Conflict cannot be resolved by rules?
        └─→ Document conflict explicitly
            - List conflicting standards
            - Explain chosen resolution
            - Document rationale
            - Allow user override if needed
```

### Detailed Conflict Resolution Rules

#### 1. Data Format Conflicts

**Rule:** Primary domain wins (data owner determines format)

**Examples:**
- MHC database: Use z_* generated classes (MHC standard)
- Web API: Use JSON (Web standard) - but data comes from MHC format internally
- Python data: Use pandas DataFrames (Python standard) when processing MHC logs

**Resolution Pattern:**
```yaml
data_format_conflict:
  conflict: "Database access: z_* classes vs raw SQL"
  primary_domain: "murata_mhc"
  resolution: "Use z_* classes (primary domain standard)"
  boundary_mapping: "Map z_* objects to JSON at API boundary"
```

#### 2. Code Style Conflicts

**Rule:** Primary domain wins (implementation language determines style)

**Examples:**
- Python script: Follow Python style (type hints, docstrings)
- JavaScript/TypeScript: Follow web development style
- VB.NET: Follow MHC style (CmL comments, cc_str, etc.)

**Resolution Pattern:**
```yaml
code_style_conflict:
  conflict: "String handling: cc_str vs Python string methods"
  primary_domain: "python_data"
  resolution: "Use Python string methods (Python is implementation language)"
  note: "If processing MHC data, understand MHC format but use Python to process it"
```

#### 3. Naming Convention Conflicts

**Rule:** Primary domain internally, secondary domain at boundaries

**Examples:**
- MHC internal: snake_case (crane_id, host_id)
- Web API boundary: camelCase (craneId, hostId)
- TypeScript interface: camelCase to match API

**Resolution Pattern:**
```yaml
naming_conflict:
  conflict: "snake_case vs camelCase"
  primary_domain: "murata_mhc"
  secondary_domain: "web_development"
  resolution: "snake_case internally, camelCase at API boundary"
  mapping: "crane_id → craneId at boundary"
```

#### 4. Error Handling Conflicts

**Rule:** Map between domains at boundaries

**Examples:**
- MHC: GP.GOOD, GP.BAD, SQL.HELD
- Web: HTTP 200, 500, 409
- Mapping: GP.BAD → HTTP 500 at API boundary

**Resolution Pattern:**
```yaml
error_handling_conflict:
  conflict: "Return codes: GP.GOOD/GP.BAD vs HTTP status codes"
  primary_domain: "murata_mhc"
  secondary_domain: "web_development"
  resolution: "Use MHC codes internally, map to HTTP at API boundary"
  mapping:
    GP.GOOD: HTTP 200
    GP.BAD: HTTP 500
    SQL.HELD: HTTP 409
    SQL.NOTFOUND: HTTP 404
```

#### 5. Logging Conflicts

**Rule:** Use primary domain logging internally, map at boundaries if needed

**Examples:**
- MHC code: cs_log_printf
- Python script: Python logging module
- JavaScript: console.log or logging library
- Web API: HTTP response logging

**Resolution Pattern:**
```yaml
logging_conflict:
  conflict: "cs_log_printf vs Python logging vs console.log"
  primary_domain: "python_data"
  resolution: "Use Python logging module (Python is implementation)"
  note: "When processing MHC logs, understand cs_log format but use Python logging for script output"
```

#### 6. Configuration Conflicts

**Rule:** Primary domain configuration internally, expose in secondary format at boundary

**Examples:**
- MHC: Registry/DBINI.CNF internally
- Web API: JSON config endpoint for consumers
- Python: Config file or environment variables

**Resolution Pattern:**
```yaml
configuration_conflict:
  conflict: "Registry/DBINI vs JSON config vs environment variables"
  primary_domain: "murata_mhc"
  secondary_domain: "web_development"
  resolution: "Use Registry/DBINI internally, expose JSON config API for web consumers"
  boundary: "API endpoint provides JSON, internally reads from Registry"
```

### Three or More Domains

**When 3+ domains are involved:**

1. **Identify Primary Domain**
   - Where core logic/data lives (most critical domain)
   - User-specified primary takes precedence
   - Order by importance if not specified

2. **Order Secondary Domains**
   - By dependency order
   - By importance/criticality
   - Apply sequentially

3. **Resolve Conflicts Sequentially**
   ```
   Primary vs Secondary 1 → Resolution 1
   Resolution 1 vs Secondary 2 → Resolution 2
   Resolution 2 vs Secondary 3 → Final Resolution
   ```

4. **Document All Resolutions**
   - List all conflicts encountered
   - Document resolution for each
   - Provide rationale
   - Note any compromises made

**Example:**
```yaml
multi_domain_resolution:
  domains: ["murata_mhc", "web_development", "python_data"]
  primary: "murata_mhc"
  secondaries: ["web_development", "python_data"]
  
  conflicts:
    - conflict: "Database access"
      between: "murata_mhc", "web_development"
      resolution: "Use z_* classes (MHC primary)"
      
    - conflict: "API format"
      between: "murata_mhc", "web_development"
      resolution: "z_* internally, JSON at API boundary"
      
    - conflict: "Processing script"
      between: "murata_mhc", "python_data"
      resolution: "Python script uses Python standards, understands MHC data format"
```

### User Override for Conflicts

**When user wants to override conflict resolution:**

1. **Accept User Override**
   - User specifies explicit resolution
   - Document user decision
   - Proceed with user-specified resolution

2. **Document Override**
   ```yaml
   conflict_override:
     conflict: "[Description]"
     default_resolution: "[What framework would choose]"
     user_override: "[What user specified]"
     rationale: "[User's reason if provided]"
     accepted: true
   ```

### Boundary Mapping Documentation

**Always document boundary mappings:**

```yaml
boundary_mapping:
  from_domain: "murata_mhc"
  to_domain: "web_development"
  location: "REST API endpoint"
  
  mappings:
    - mhc_format: "GP.GOOD"
      web_format: "HTTP 200"
      
    - mhc_format: "z_cranes object"
      web_format: "JSON object with camelCase keys"
      
    - mhc_format: "cs_log_printf output"
      web_format: "API response log entry"
```

### See Also

- [Edge Case Handling Guide](../docs/edge_case_handling.md) - Multi-domain edge cases
- [Error Handling Protocol](../frameworks/error_handling_protocol.md) - Conflict-related errors

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

