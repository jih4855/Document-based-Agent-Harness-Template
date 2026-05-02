# Agent Harness Instructions

This file is the main operating contract for agents working in this repository.
Read it before making changes.

## Purpose

This repository is a document-based agent harness. It keeps the agent's working
rules, task state, memory, and reusable skills in plain Markdown so the workflow
can be inspected, copied, and adapted without a custom runtime.

## Required Reading Order

At the start of a session, read these files in order:

1. `agent.md`
2. `context/tacit.md`
3. `context/agent_index.md`
4. `context/task.md` if it exists, otherwise `context/task.example.md`
5. `context/memory.md` if it exists, otherwise `context/memory.example.md`
6. `skills/index.md`
7. Any skill document directly relevant to the current task

Do not depend on include syntax such as `@context/tacit.md`. Some runtimes do not
expand includes. Read the files directly.

## Work Cycle

Use this loop for every non-trivial task:

1. Read the relevant context.
2. State the immediate plan if the task has multiple steps.
3. Make the smallest useful change.
4. Verify the result with the most relevant command, inspection, or checklist.
5. Update `context/memory.md` when a decision or durable fact changed.
6. Update `context/task.md` when task status changed.

## Context Rules

- `context/tacit.md` stores durable rules, preferences, conventions, and lessons.
- `context/agent_index.md` routes repeatable work to documented runtime agents.
- `context/memory.md` stores recent cross-session state.
- `context/task.md` stores active work and next actions.
- Example files are templates. Do not treat `*.example.md` as live state.
- Keep live context concise. Archive old detail instead of letting files grow
  without bound.

## Tacit Update Rules

- When a durable preference, operating rule, repeated failure, or successful
  workaround appears, record it in `context/tacit.md`.
- Do not store short-lived task status in tacit knowledge. Use `context/task.md`
  for active work and `context/memory.md` for recent project state.
- Keep `context/tacit.md` as the current tacit index. If you split detailed
  rules into additional context files later, update the index immediately.

## Delegation Rules

- The main agent owns user-facing strategy, preference changes, operating rules,
  and updates to tacit knowledge, skills, and delegation structure.
- Subagents are runtime executors for documented, repeatable work. Give each
  subagent one task, the minimum necessary context, and the common output
  contract defined in `context/agent_index.md`.
- If a subagent is blocked by missing context, permissions, credentials, or
  judgment calls, the main agent mentors, narrows the instruction, or takes over.
- Do not delegate policy changes, taste calibration, or new workflow design
  unless the user explicitly asks for independent analysis.

## Skill Rules

- A skill is a reusable Markdown playbook for a specific workflow.
- Read `skills/index.md` before creating or editing skills.
- Prefer one focused skill over a large all-purpose skill.
- A skill can mention commands, files, checks, and decision rules.
- Do not add executable scripts to this template unless the project explicitly
  needs them. Keep scripts in downstream projects.
- Configure skills and subagents for the user's actual workflow. This template
  only provides the structure; it does not assume which tools, models, or
  specialist agents the user should have.
- Keep `skills/index.md` current whenever a skill is added, renamed, removed, or
  given a new trigger.

## Safety Rules

- Golden commit rule: do not commit what is built, fetched, generated, or secret.
  Examples: `dist/`, `build/`; `node_modules/`, `vendor/`; caches and logs;
  `.env`, keys, and tokens.
- Never commit `.env`, API keys, OAuth tokens, private customer data, or personal
  schedules.
- Before running commands with side effects, understand the target path and
  expected output.
- Use dry-run or read-only checks before irreversible operations.
- If a task requires external credentials or destructive actions, ask for
  confirmation first.

## Completion Checklist

Before reporting a task as done:

- Confirm what changed.
- Confirm what was verified.
- Note anything that was not verified.
- Update live context files if the task changed state or introduced a durable
  lesson.
