# Complete Documentation Specification

**Purpose:** When the framework bootstraps a project, generate **exhaustive documentation** covering every aspect of the system with full relationship mapping.

---

## DOCUMENTATION REQUIREMENTS

When bootstrapping a project, the AI MUST generate ALL of the following:

---

## SECTION 0: Project Overview

### 0.1 System Summary

- Project name, purpose, customer
- System type (ASRS, conveyor, shuttle, etc.)
- High-level capabilities
- Key metrics (# cranes, # locations, throughput)

### 0.2 Master Relationship Map

```mermaid
graph TB
    subgraph Host
        WMS[Host WMS]
    end
    
    subgraph MHC
        HSTIN[MHC_HOST_IN]
        MOVS[MHC_MOVS]
        LOCN[MHC_LOCATION]
    end
    
    subgraph Equipment
        Crane[Stacker Cranes]
        Shuttle[Shuttles]
        Conv[Conveyors]
    end
    
    WMS --> HSTIN
    HSTIN --> MOVS
    MOVS --> Crane
    MOVS --> Shuttle
    MOVS --> Conv
```

### 0.3 Quick Start Guide

- 15-minute onboarding
- Key concepts
- First tasks

---

## SECTION 1: System Architecture

### 1.1 System Overview

- Complete data flow diagram
- All system layers (Host, MHC, PLC, Equipment)
- Communication protocols

### 1.2 Process Architecture

```
Generate for EVERY process:
- Process name
- Purpose
- Input/output
- Dependencies
- Database tables used
- Configuration keys
- Log file
```

### 1.3 Process Relationship Map

```mermaid
graph LR
    subgraph Dispatchers
        MOVDP[p_ar_movdp]
        STKDP[p_ar_stkdp]
        CNVDP[p_ar_cnvdp]
    end
    
    subgraph Communication
        STKCM[p_cc_stkcm]
        CNVCM[p_cc_cnvcmx]
    end
    
    subgraph Completers
        SRCMP[p_ar_srcmp]
        EVENTS[p_ar_events]
    end
    
    MOVDP --> STKDP
    STKDP --> STKCM
    STKCM --> SRCMP
```

### 1.4 Shared Memory Map

- All shared memory segments
- Structure definitions
- Read/write ownership
- Update frequencies

---

## SECTION 2: Equipment Control

### For EACH equipment type, document

#### 2.X Equipment Type Documentation

- Equipment name and quantity
- Physical description
- Communication protocol
- Dispatcher service
- Communication service
- Completer service
- Status codes
- Error codes
- Recovery procedures

#### 2.X.1 Equipment Relationship Map

```mermaid
graph TB
    subgraph "Equipment Type"
        EQ1[Equipment 1]
        EQ2[Equipment 2]
    end
    
    subgraph Services
        DISP[Dispatcher]
        COMM[Communication]
        COMP[Completer]
    end
    
    subgraph Database
        MOVS[MHC_MOVS]
        SM2DB[Shared Memory Table]
    end
    
    EQ1 --> COMM
    COMM --> DISP
    DISP --> MOVS
    COMP --> MOVS
```

#### 2.X.2 State Machine

```mermaid
stateDiagram-v2
    [*] --> Idle
    Idle --> Working: Command Received
    Working --> Complete: Task Done
    Working --> Error: Fault
    Error --> Idle: Reset
    Complete --> Idle: ACK
```

---

## SECTION 3: Database Reference

### 3.1 Table Catalog

For EVERY table in the database:

```
- Table name
- Purpose
- Columns (all)
- Primary key
- Foreign keys
- Indexes
- Triggers
- Row count estimate
- Retention policy
```

### 3.2 Table Relationship Map (ERD)

```mermaid
erDiagram
    MHC_MOVS ||--o{ MHC_LOCATION : "from/to"
    MHC_MOVS ||--o{ MHC_LOAD : "load_id"
    MHC_MOVS }|--|| MHC_MOVE_TYPE : "move_type"
    MHC_LOCATION }|--|| MHC_REGION : "region"
    MHC_PICK ||--o{ MHC_MOVS : "move_id"
```

### 3.3 Stored Procedure Catalog

For EVERY stored procedure:

```
- Procedure name
- Purpose
- Parameters
- Return values
- Tables affected
- Called by (services)
- Calls (other procedures)
```

### 3.4 View Catalog

For EVERY view:

```
- View name
- Purpose
- Base tables
- Indexed? (yes/no)
- Used by (services)
```

### 3.5 Function Catalog

For EVERY function:

```
- Function name
- Purpose
- Parameters
- Return type
- Used by
```

### 3.6 Trigger Catalog

For EVERY trigger:

```
- Trigger name
- Table
- Event (INSERT/UPDATE/DELETE)
- Purpose
- Side effects
```

---

## SECTION 4: Configuration Reference

### 4.1 DBINI Configuration

For EVERY configuration key:

```
- Key name
- Section
- Data type
- Default value
- Valid values
- Purpose
- Used by (services)
```

### 4.2 Stand/Station Definitions

For EVERY stand:

```
- Stand name
- Type
- Region
- Equipment assignment
- PLC address
- DCB bits
```

### 4.3 Stand Relationship Map

```mermaid
graph TB
    subgraph Region_01
        S1[Stand 01]
        S2[Stand 02]
    end
    
    subgraph Region_02
        S3[Stand 03]
        S4[Stand 04]
    end
    
    S1 --> S2
    S2 --> S3
    S3 --> S4
```

### 4.4 DCB Bit Mapping

For EVERY DCB bit:

```
- Bit address
- Name
- Direction (input/output)
- Purpose
- PLC tag
```

### 4.5 Registry Settings

For EVERY registry key:

```
- Key path
- Value name
- Data type
- Default
- Purpose
```

### 4.6 Elements Table

For EVERY element:

```
- Item_Key
- Item_Value
- Data type
- Purpose
- Modified by
```

---

## SECTION 5: Code Reference

### 5.1 Service Catalog

For EVERY service/process:

```
- Service name
- Source file(s)
- Entry point
- Main loop function
- Key functions (list all)
- Database tables used
- Shared memory used
- Configuration keys
- Log file
```

### 5.2 Function Reference

For EVERY significant function:

```
- Function name
- File
- Purpose
- Parameters
- Return value
- Called by
- Calls
- Database operations
- Error handling
```

### 5.3 Class Reference (VB.NET)

For EVERY class:

```
- Class name
- Namespace
- Purpose
- Properties
- Methods
- Events
- Inheritance
- Dependencies
```

### 5.4 Code Relationship Map

```mermaid
graph TB
    subgraph p_ar_movdp
        MAIN[main]
        FW[findwork]
        FL[mov_find_locations]
    end
    
    MAIN --> FW
    FW --> FL
    FL --> DB[(MHC_MOVS)]
```

---

## SECTION 6: Communication Reference

### 6.1 Protocol Documentation

For EVERY communication protocol:

```
- Protocol name
- Equipment type
- Service
- Port/address
- Message format
- Commands (all)
- Responses
- Error handling
- Timing
```

### 6.2 Message Catalog

For EVERY message type:

```
- Message ID
- Direction
- Fields
- Purpose
- Sequence diagram
```

### 6.3 Communication Flow Maps

```mermaid
sequenceDiagram
    participant Disp as Dispatcher
    participant Comm as Communication
    participant PLC as Equipment
    
    Disp->>Comm: Command
    Comm->>PLC: Message
    PLC->>Comm: ACK
    Comm->>Disp: Status
```

---

## SECTION 7: Move & Material Flow

### 7.1 Move Type Catalog

For EVERY move type:

```
- Move type code
- Description
- From region(s)
- To region(s)
- Equipment used
- Steps
- Status progression
```

### 7.2 Move Lifecycle Map

```mermaid
stateDiagram-v2
    [*] --> Pending: Created
    Pending --> Assigned: Location found
    Assigned --> Active: Equipment dispatched
    Active --> Working: In progress
    Working --> Complete: Finished
    Complete --> [*]: Archived
```

### 7.3 Routing Logic

For EVERY routing scenario:

```
- From region
- To region
- Path (stands traversed)
- Equipment sequence
- Decision points
```

### 7.4 Material Flow Map

```mermaid
graph LR
    Receive[Receiving] --> Store[Storage]
    Store --> Pick[Picking]
    Pick --> Ship[Shipping]
```

---

## SECTION 8: UI Reference

### 8.1 Form Catalog

For EVERY form:

```
- Form name
- Purpose
- Menu location
- Controls
- Events
- Database interactions
- Security permissions
```

### 8.2 UI Navigation Map

```mermaid
graph TB
    Main[Main Menu]
    Main --> Inquiry
    Main --> Maint[Maintenance]
    Main --> Recovery
    
    Inquiry --> MoveInq[Move Inquiry]
    Inquiry --> ToteInq[Tote Inquiry]
```

### 8.3 Security Matrix

```
For EVERY role:
- Role name
- Description
- Form access (list)
- Function access (list)
```

---

## SECTION 9: Troubleshooting

### 9.1 Decision Trees

For EVERY issue category:

```mermaid
graph TD
    Start{Issue Type?}
    Start -->|Move Stuck| MS[Move Stuck Tree]
    Start -->|Equipment Error| EE[Equipment Error Tree]
    Start -->|Database Error| DE[Database Error Tree]
    
    MS --> MS1{Where stuck?}
    MS1 -->|Location| MS1A[Check location status]
    MS1 -->|Equipment| MS1B[Check equipment status]
```

### 9.2 Error Code Reference

For EVERY error code:

```
- Error code
- Source
- Description
- Cause
- Resolution steps
- Prevention
```

### 9.3 Common Issues

For EVERY common issue:

```
- Symptom
- Cause
- Diagnosis steps
- Resolution
- SQL queries to help
- Prevention
```

---

## SECTION 10: Quick Reference

### 10.1 SQL Quick Reference

Common queries for:

- Move status
- Equipment status
- Location status
- Pick status
- Error lookup

### 10.2 Status Code Reference

ALL status codes for:

- Moves
- Locations
- Equipment
- Picks
- Transfers

### 10.3 Command Reference

ALL utility commands:

- Service start/stop
- Database utilities
- Diagnostic tools

### 10.4 Keyboard Shortcuts

ALL UI shortcuts

---

## RELATIONSHIP MAPPING REQUIREMENTS

Every relationship map MUST include:

### Required Diagrams

1. **System Overview** - All major components
2. **Process Flow** - How services interact
3. **Data Flow** - How data moves through system
4. **Equipment Hierarchy** - Physical relationships
5. **Database ERD** - Table relationships
6. **State Machines** - For each entity type
7. **Sequence Diagrams** - For each workflow
8. **Navigation Maps** - UI structure
9. **Decision Trees** - Troubleshooting flows

### Diagram Format

Use Mermaid syntax for all diagrams:

- `graph TB/LR` for hierarchies and flows
- `erDiagram` for database relationships
- `stateDiagram-v2` for state machines
- `sequenceDiagram` for interactions
- `gantt` for timelines if needed

---

## COMPLETENESS CHECKLIST

Before documentation is considered complete:

### Coverage

- [ ] EVERY process documented
- [ ] EVERY database table documented
- [ ] EVERY stored procedure documented
- [ ] EVERY configuration key documented
- [ ] EVERY stand/station documented
- [ ] EVERY equipment type documented
- [ ] EVERY move type documented
- [ ] EVERY UI form documented
- [ ] EVERY error code documented

### Relationships

- [ ] System overview diagram
- [ ] Process relationship map
- [ ] Database ERD
- [ ] Equipment hierarchy
- [ ] Stand/region map
- [ ] Move flow diagram
- [ ] UI navigation map
- [ ] Troubleshooting decision trees

### Usability

- [ ] Quick start guide
- [ ] Quick reference cards
- [ ] Common task examples
- [ ] Emergency procedures

---

## OUTPUT STRUCTURE

The generated documentation MUST follow this folder structure:

```
docs/
├── README.md                           # Master index with relationship map
├── 00_Quick_Start_Guide.md             # 15-minute onboarding
├── 01_System_Architecture/
│   ├── 01_System_Overview.md           # With data flow diagram
│   ├── 02_Process_Architecture.md      # With process map
│   └── 03_Shared_Memory.md             # With structure diagrams
├── 02_Equipment_Control/
│   └── [Equipment].md                  # For each equipment type
├── 03_Database_Reference/
│   ├── 01_Tables.md                    # With ERD
│   ├── 02_Stored_Procedures.md
│   ├── 03_Views.md
│   ├── 04_Functions.md
│   └── 05_Triggers.md
├── 04_Configuration_Reference/
│   ├── 01_DBINI.md
│   ├── 02_Stands.md                    # With stand map
│   ├── 03_DCB.md
│   └── 04_Registry.md
├── 05_Code_Reference/
│   ├── 01_Services.md
│   └── 02_Functions.md
├── 06_Communication/
│   └── 01_Protocols.md                 # With sequence diagrams
├── 07_Move_Flow/
│   ├── 01_Move_Types.md
│   └── 02_Routing.md                   # With flow diagram
├── 08_UI_Reference/
│   ├── 01_Forms.md
│   └── 02_Security.md                  # With navigation map
├── 09_Troubleshooting/
│   └── [Issue_Type].md                 # With decision trees
└── 10_Quick_Reference/
    ├── 01_SQL_Reference.md
    ├── 02_Status_Codes.md
    ├── 03_Error_Codes.md
    └── 04_Commands.md
```

---

**This specification ensures COMPLETE documentation with FULL relationship mapping for ANY system.**
