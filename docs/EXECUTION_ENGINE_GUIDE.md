# Execution Engine Guide

**Version:** 1.0.0  
**Last Updated:** 2025-01-XX  
**Purpose:** Comprehensive guide to using Pliny Framework's execution engine for session management, checkpointing, and parallel execution.

---

## Overview

The Execution Engine provides persistent state management, git-based checkpointing, crash-safe audit logging, and parallel agent orchestration. It enables tasks to be paused, resumed, and recovered after failures.

---

## Quick Start

### 1. Start a Session

```bash
pliny session start "My Task Name"
```

This creates a new session with a unique ID and initializes state tracking.

### 2. Execute with Checkpointing

```bash
pliny execute --framework rise --checkpoint phase
```

Checkpoints are created automatically after each phase completes.

### 3. Resume Incomplete Sessions

```bash
pliny session list              # List all sessions
pliny session resume <id>       # Resume specific session
```

---

## Session Management

### Creating Sessions

Sessions track the state of task execution:

- **Session ID** - Unique identifier (UUID)
- **Current Phase** - Which phase is being executed
- **Completed Agents** - List of completed agents/steps
- **Checkpoints** - Map of agent names to git commit hashes
- **Metrics** - Timing, costs, and attempt counts

### Session Lifecycle

1. **Initialize** - Create new or resume existing
2. **Execute** - Run phases/agents
3. **Checkpoint** - Save state at key points
4. **Complete** - Mark as finished
5. **Cleanup** - Archive or delete (optional)

See [Session Manager](../execution/session_manager.md) for detailed documentation.

---

## Checkpointing

### Creating Checkpoints

Checkpoints are created automatically at configurable intervals:

- **After Each Phase** - `--checkpoint phase`
- **After Each Agent** - `--checkpoint agent`
- **Manual** - `pliny checkpoint create "checkpoint-name"`

### Rolling Back

Rollback to a previous checkpoint:

```bash
pliny rollback "after-research"
```

This restores the workspace to the checkpoint state and updates session state accordingly.

See [Checkpoint Manager](../execution/checkpoint_manager.md) for detailed documentation.

---

## Parallel Execution

### Enabling Parallel Agents

```bash
pliny execute --parallel
```

Agents within the same phase will execute concurrently, significantly reducing execution time.

### Phase Configuration

Configure phases in your config file:

```yaml
phases:
  - name: research
    parallel: true
    agents:
      - research-web
      - research-code
      - research-docs
```

See [Parallel Agents](../execution/parallel_agents.md) for detailed documentation.

---

## Audit Logs

All executions are logged to `audit-logs/`:

- **Event-by-event tracking** - Every action is logged
- **Timing metrics** - Duration for each phase/agent
- **Cost tracking** - API costs and resource usage
- **Rollback history** - Complete audit trail

### Viewing Audit Logs

```bash
pliny audit view <session-id>
pliny audit summary <session-id>
```

See [Audit System](../execution/audit_system.md) for detailed documentation.

---

## Error Handling

The execution engine includes robust error handling:

- **Categorized Errors** - Config, Network, Tool, Validation, AI, System
- **Automatic Retry** - Transient errors are retried with exponential backoff
- **Graceful Degradation** - Unrecoverable errors are logged and reported

### Retry Configuration

Configure retry strategies in your config:

```yaml
error_handling:
  retry_strategies:
    network:
      max_retries: 3
      backoff: exponential
      initial_delay: 1000
```

See [Error Handling](../execution/error_handling.md) for detailed documentation.

---

## Integration with Frameworks

### R-I-S-E Execution

```bash
pliny session start "Research Task"
pliny execute --framework rise --checkpoint phase
```

Checkpoints are created after:
- Research phase completes
- Identify phase completes
- Synthesize phase completes
- Execute phase completes

### C-A-R-E Execution

```bash
pliny session start "Quick Fix"
pliny execute --framework care --checkpoint step
```

Checkpoints are created after:
- Context step completes
- Analyze step completes
- Respond step completes
- Evaluate step completes

---

## Recovery from Failures

### Detecting Incomplete Sessions

```bash
pliny session list
```

Shows all sessions with their status (in-progress, completed, failed).

### Resuming Sessions

```bash
pliny session resume <session-id>
```

Resumes execution from the last checkpoint.

### Rolling Back Failed Agents

```bash
pliny rollback "before-failed-agent"
pliny execute --rerun failed-agent
```

---

## Best Practices

1. **Create Checkpoints Frequently** - Don't lose work
2. **Use Parallel Execution** - Faster completion for independent tasks
3. **Monitor Audit Logs** - Track progress and costs
4. **Handle Errors Gracefully** - Use retry logic for transient failures
5. **Clean Up Old Sessions** - Archive or delete completed sessions

---

## Related Documentation

- [Session Manager](../execution/session_manager.md) - Persistent state management
- [Checkpoint Manager](../execution/checkpoint_manager.md) - Git-based checkpointing
- [Audit System](../execution/audit_system.md) - Crash-safe logging
- [Parallel Agents](../execution/parallel_agents.md) - Multi-agent orchestration
- [Error Handling](../execution/error_handling.md) - Retry logic and error categories
- [R-I-S-E Framework](../frameworks/universal_rise.md) - Research → Identify → Synthesize → Execute
- [C-A-R-E Framework](../frameworks/universal_care.md) - Context → Analyze → Respond → Evaluate

