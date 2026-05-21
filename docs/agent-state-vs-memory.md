# Agent State vs Memory

Long-horizon agent work fails when a new session cannot tell what is true now. A model may remember facts, a trace may show what happened, and an orchestrator may decide what runs next, but none of those layers automatically preserve the current operational state of a task.

## The Distinction

Memory stores facts, preferences, and reusable context. It helps an assistant remember that a user prefers TypeScript or that a project uses Django.

Traces record what happened. They are useful for debugging, observability, and audit trails, but they can be too verbose for handoff.

Orchestration decides which agent, tool, or workflow step runs. It controls execution, but execution control is not the same as task state.

State tracks what is true now, what changed, what failed, and what should happen next. It captures decisions, rejected options, blockers, assumptions, artifacts, and next actions in a form that another agent or human can inspect.

## Why Durable State Matters

Long-running AI work often spans multiple sessions, tools, or agents. Without durable state, the next worker may:

- Repeat failed approaches.
- Miss constraints that were already decided.
- Lose track of blockers.
- Treat provisional guesses as facts.
- Ask the human to re-explain the same context.

Durable state makes handoff explicit. It gives the next agent a compact current-state packet instead of asking it to infer truth from a full transcript.

## Where Stateframe Fits

[Stateframe](https://github.com/42amps/stateframe) is a file-first task-state ledger. It stores task state in `task.ledger.json`, preserves changes as commits, and generates handoff packets from locked state items.

| Layer | Purpose | Failure Mode | Stateframe's Role |
| --- | --- | --- | --- |
| Memory | Store facts, preferences, and reusable context | Remembers facts without knowing which task state is current | Keeps task-specific truth separate from general memory |
| Traces | Record what happened during execution | Too verbose to quickly resume work | Converts important outcomes into concise state items |
| Orchestration | Decide which agent/tool runs next | Controls execution without preserving durable handoff state | Provides a state packet orchestration can pass between steps |
| State | Track current truth, changes, failures, and next actions | Lost or implicit state causes repeated work and bad handoffs | Makes decisions, blockers, rejected options, and next steps inspectable |

## Design Principle

Agent state should be portable, reviewable, and small enough to read. A human should be able to inspect it in Git; an agent should be able to resume from it without rereading the whole conversation.
