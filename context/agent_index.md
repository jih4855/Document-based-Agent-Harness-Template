# Agent Delegation Policy

This file defines **how the main agent delegates work**. It is not a runtime
catalog. The list of available subagents is managed by the agent tool itself
(for example, `/agents` in Claude Code, or the equivalent in Codex/Cursor).

Keep this file short. Detailed runtime prompts live in `context/runtime_agents/`,
and reusable workflow procedures live in `skills/`.

## Main Agent Owns

- strategy, preferences, tone, and quality standards
- deciding whether a repeated workflow deserves a skill or subagent
- updating `context/tacit.md`, `context/memory.md`, skills, and this policy
- mentoring or taking over when a delegated agent is blocked

## Subagents Own

- one documented task at a time
- repeated execution based on a skill or runtime template
- narrow file reads and scoped changes
- status, checks, blockers, and recommended next steps

## Never Delegate

The main agent must handle these directly, even if a subagent looks capable:

- user-facing strategy or preference changes
- changes to `context/tacit.md`, skills, or this policy
- new workflow design decisions
- destructive or irreversible actions without explicit user approval

## Common Output Contract

Every subagent must report:

`status`, `summary`, `actions_taken`, `files_read`, `files_changed`,
`recommended_next_steps`

If a subagent's runtime template defines its own output, it must extend this
contract, not replace it.

## Tool Discovery

The runtime agent catalog (which subagents exist, which tools they have, how
they are invoked) is owned by the agent tool, not this file.

- In Claude Code, register subagents under `.claude/agents/<name>.md` and use
  `/agents` to list them. The frontmatter `description` field controls auto
  delegation triggers.
- In tool-neutral setups, use `context/runtime_agents/<name>.md` as the source
  of truth and inject the file contents into the subagent prompt at invocation
  time.

Either way, this file governs **policy**, not the catalog.

## Escalation Rule

If a subagent cannot finish because it lacks context, credentials, permissions,
or judgment authority, it must report the blocker. The main agent then
diagnoses, narrows the handoff, or completes the task directly. Subagents do
not invent new policy to unblock themselves.
