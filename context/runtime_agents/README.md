# Runtime Agent Templates

This folder stores handoff templates for subagents.

These files are not always-on agents. They are prompts and operating contracts
the main agent can use when creating a runtime subagent in a tool that supports
delegation.

## Principles

- One subagent handles one task.
- Give the subagent only the files and decisions it needs.
- Prefer skills for procedural steps and runtime templates for handoff rules.
- Subagents follow documented rules; they do not invent new preferences.
- Blocked subagents report the blocker so the main agent can mentor or take over.

## Suggested Template Shape

```markdown
# example-agent

## Purpose

What repeated task this agent handles.

## Read

- `context/tacit.md`
- relevant skill document
- task-specific source files

## Allowed Work

- scoped action 1
- scoped action 2

## Forbidden Work

- unrelated workflows
- broad cleanup
- irreversible actions without explicit approval

## Output Contract

See `context/agent_index.md` for the canonical contract every subagent must
extend.
```
