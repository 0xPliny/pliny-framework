# Parallel Agent Orchestration

**Version:** 1.0.0  
**Last Updated:** 2025-01-XX  
**Purpose:** Execute multiple AI agents concurrently for faster task completion.

---

## Overview

Parallel Agent Orchestration enables multiple AI agents to work simultaneously on independent tasks, significantly reducing execution time for complex problems. Agents are organized into phases, with sequential phases and parallel agents within each phase.

---

## Core Concepts

### Agent Definition

Each agent has:

- **Name** - Unique identifier (e.g., "research-web", "research-code")
- **Description** - What the agent does
- **Input Requirements** - Deliverables from previous phases that this agent needs
- **Output Deliverables** - What this agent produces
- **Dependencies** - Other agents that must complete before this agent can run
- **Phase** - Which phase this agent belongs to
- **Order** - Execution order within phase (for sequential execution)

### Phase Organization

Agents are grouped into phases:

- **Sequential Phases** - Phases run one after another
- **Parallel Agents** - Agents within a phase can run concurrently
- **Dependency Graph** - Determines execution order based on prerequisites

### Concurrency Control

- **SessionMutex** - Prevents race conditions when updating shared state
- **Shared State Protection** - Session state protected by locks
- **Isolated Working Context** - Each agent has its own working directory/context

---

## Example: Security Testing (from Shannon)

```yaml
phases:
  - name: pre-reconnaissance
    parallel: false
    agents:
      - pre-recon  # Single agent
    
  - name: reconnaissance
    parallel: false
    agents:
      - recon  # Single agent
    
  - name: vulnerability-analysis
    parallel: true
    agents:
      - injection-vuln
      - xss-vuln
      - auth-vuln
      - authz-vuln
      - ssrf-vuln
    
  - name: exploitation
    parallel: true
    agents:
      - injection-exploit
      - xss-exploit
      - auth-exploit
      - authz-exploit
      - ssrf-exploit
    
  - name: reporting
    parallel: false
    agents:
      - report
```

---

## Implementation Pattern

### Basic Phase Execution

```javascript
/**
 * Execute a phase (sequential or parallel)
 * @param {Object} phase - Phase definition
 * @param {string} phase.name - Phase name
 * @param {boolean} phase.parallel - Whether agents run in parallel
 * @param {Array<string>} phase.agents - List of agent names
 * @param {Object} context - Execution context (session, config, etc.)
 * @returns {Promise<Object>} Phase results
 */
async function executePhase(phase, context) {
  console.log(`\n📋 Executing phase: ${phase.name}`);
  
  if (phase.parallel) {
    // Execute all agents concurrently
    console.log(`⚡ Running ${phase.agents.length} agents in parallel`);
    
    const results = await Promise.all(
      phase.agents.map(agentName => executeAgent(agentName, context))
    );
    
    // Merge results
    const mergedResults = {};
    for (const result of results) {
      Object.assign(mergedResults, result);
    }
    
    return mergedResults;
  } else {
    // Execute agents sequentially
    console.log(`➡️ Running ${phase.agents.length} agents sequentially`);
    
    let accumulatedResults = {};
    for (const agentName of phase.agents) {
      const result = await executeAgent(agentName, context);
      Object.assign(accumulatedResults, result);
      
      // Update context with results for next agent
      context.deliverables = {
        ...context.deliverables,
        ...result
      };
    }
    
    return accumulatedResults;
  }
}

/**
 * Execute a single agent
 * @param {string} agentName - Agent name
 * @param {Object} context - Execution context
 * @returns {Promise<Object>} Agent results
 */
async function executeAgent(agentName, context) {
  const agent = AGENTS[agentName];
  
  if (!agent) {
    throw new Error(`Agent '${agentName}' not found`);
  }
  
  // Check prerequisites
  const missingPrereqs = agent.prerequisites.filter(
    prereq => !context.session.completedAgents.includes(prereq)
  );
  
  if (missingPrereqs.length > 0) {
    throw new Error(
      `Cannot run '${agentName}': prerequisite agent(s) not completed: ${missingPrereqs.join(', ')}`
    );
  }
  
  console.log(`🤖 Running agent: ${agent.displayName}`);
  
  // Execute agent (this would call the actual agent implementation)
  const result = await runAgentImplementation(agentName, context);
  
  // Mark agent as completed
  await sessionManager.checkpoint(context.session.id, agentName, result.checkpoint);
  
  return result.deliverables;
}
```

---

## Integration with Pliny Frameworks

### R-I-S-E with Parallel Agents

```javascript
const phases = [
  {
    name: 'research',
    parallel: true,  // Multiple research agents can run concurrently
    agents: [
      'research-web',
      'research-code',
      'research-docs'
    ]
  },
  {
    name: 'identify',
    parallel: true,  // Multiple pattern identification agents
    agents: [
      'identify-patterns',
      'identify-anti-patterns',
      'identify-optimizations'
    ]
  },
  {
    name: 'synthesize',
    parallel: false,  // Sequential - needs all research and identification
    agents: [
      'synthesize-solution'
    ]
  },
  {
    name: 'execute',
    parallel: true,  // Multiple implementation tasks can run in parallel
    agents: [
      'execute-code',
      'execute-tests',
      'execute-docs'
    ]
  }
];

// Execute all phases sequentially
let context = { session, config, deliverables: {} };
for (const phase of phases) {
  const phaseResults = await executePhase(phase, context);
  context.deliverables = { ...context.deliverables, ...phaseResults };
}
```

### C-A-R-E with Parallel Agents

```javascript
const phases = [
  {
    name: 'context',
    parallel: true,  // Gather context from multiple sources
    agents: [
      'context-logs',
      'context-metrics',
      'context-code'
    ]
  },
  {
    name: 'analyze',
    parallel: true,  // Multiple analysis perspectives
    agents: [
      'analyze-performance',
      'analyze-security',
      'analyze-reliability'
    ]
  },
  {
    name: 'respond',
    parallel: false,  // Sequential - needs all analysis
    agents: [
      'respond-fix'
    ]
  },
  {
    name: 'evaluate',
    parallel: true,  // Multiple verification checks
    agents: [
      'evaluate-tests',
      'evaluate-metrics',
      'evaluate-security'
    ]
  }
];
```

---

## Concurrency Safety

### Session State Updates

When multiple agents update session state concurrently, use mutexes:

```javascript
import { SessionMutex } from './utils/concurrency.js';

const sessionMutex = new SessionMutex();

async function markAgentCompleted(sessionId, agentName, checkpointCommit) {
  const unlock = await sessionMutex.lock(sessionId);
  
  try {
    // Get fresh session data under lock
    const session = await sessionManager.getSession(sessionId);
    
    // Update session state
    await sessionManager.checkpoint(sessionId, agentName, checkpointCommit);
  } finally {
    unlock();
  }
}
```

### Isolated Working Contexts

Each agent should have its own working directory to avoid conflicts:

```javascript
async function executeAgent(agentName, context) {
  // Create isolated working directory for this agent
  const agentWorkDir = path.join(context.workDir, `agent-${agentName}`);
  await fs.promises.mkdir(agentWorkDir, { recursive: true });
  
  // Copy shared context files if needed
  if (context.sharedFiles) {
    for (const file of context.sharedFiles) {
      await fs.promises.copyFile(
        path.join(context.workDir, file),
        path.join(agentWorkDir, file)
      );
    }
  }
  
  // Execute agent in isolated directory
  const result = await runAgentImplementation(agentName, {
    ...context,
    workDir: agentWorkDir
  });
  
  // Merge deliverables back to shared context
  return result;
}
```

---

## Error Handling

When agents run in parallel, handle failures gracefully:

```javascript
async function executePhase(phase, context) {
  if (phase.parallel) {
    // Execute all agents concurrently, but handle failures
    const results = await Promise.allSettled(
      phase.agents.map(agentName => executeAgent(agentName, context))
    );
    
    // Separate successes and failures
    const successes = [];
    const failures = [];
    
    for (let i = 0; i < results.length; i++) {
      const result = results[i];
      const agentName = phase.agents[i];
      
      if (result.status === 'fulfilled') {
        successes.push({ agent: agentName, result: result.value });
      } else {
        failures.push({ agent: agentName, error: result.reason });
        // Mark agent as failed
        await sessionManager.markFailed(context.session.id, agentName);
      }
    }
    
    // Merge successful results
    const mergedResults = {};
    for (const success of successes) {
      Object.assign(mergedResults, success.result);
    }
    
    // Log failures
    if (failures.length > 0) {
      console.log(`⚠️ ${failures.length} agent(s) failed:`);
      for (const failure of failures) {
        console.log(`  - ${failure.agent}: ${failure.error.message}`);
      }
    }
    
    return mergedResults;
  } else {
    // Sequential execution - stop on first failure
    let accumulatedResults = {};
    for (const agentName of phase.agents) {
      try {
        const result = await executeAgent(agentName, context);
        Object.assign(accumulatedResults, result);
        context.deliverables = { ...context.deliverables, ...result };
      } catch (error) {
        await sessionManager.markFailed(context.session.id, agentName);
        throw error; // Propagate error to stop phase
      }
    }
    return accumulatedResults;
  }
}
```

---

## Related Documentation

- [Session Manager](./session_manager.md) - Persistent state management
- [Checkpoint Manager](./checkpoint_manager.md) - Git-based checkpointing
- [Audit System](./audit_system.md) - Crash-safe logging
- [Error Handling](./error_handling.md) - Retry logic and error categories
- [R-I-S-E Framework](../frameworks/universal_rise.md) - Research → Identify → Synthesize → Execute
- [C-A-R-E Framework](../frameworks/universal_care.md) - Context → Analyze → Respond → Evaluate

