# Tacit Knowledge Index

This file stores durable operating knowledge for the harness.

Keep it short. Move detailed procedures into skill documents when they become
repeatable workflows.

## Response Style

- Be direct and specific.
- Prefer concrete steps over abstract advice.
- Explain tradeoffs when choosing one path over another.
- Do not invent facts about the project. Read files first.

## Work Style

- Start from the repository's existing structure.
- Make focused changes.
- Avoid unrelated refactors.
- Prefer Markdown playbooks before adding automation.
- Use example files as templates, not live state.

## Main/Subagent Split

- The main agent discusses strategy, taste, standards, and workflow changes with
  the user.
- Subagents execute documented, repeatable tasks from skills or runtime
  templates.
- When a subagent is blocked or a rule needs to change, route the decision back
  to the main agent.

## Context Hygiene

- Update `context/memory.md` after meaningful decisions.
- Update `context/task.md` after task status changes.
- Keep secrets and personal data out of tracked context.
- Keep long logs, generated artifacts, and local notes out of Git.
- Before committing, remember the golden rule: built, fetched, generated, and
  secret files do not belong in the repository.
- Treat this file as the current tacit index. If detailed tacit notes are split
  into additional context files later, add or update the link here immediately.
- Treat `context/agent_index.md` as the delegation router when repeatable
  subagent work is introduced.

## Tacit Update Rules

- Record durable preferences, repeated failure patterns, successful
  workarounds, and workflow decisions when they become clear.
- Do not record temporary task state here. Use `context/task.md` or
  `context/memory.md` instead.
- Remove or mark stale rules when they no longer match the project.

## Skill Authoring

- One skill should cover one workflow.
- The skill name should describe the action, not the tool.
- Include triggers, inputs, steps, verification, and failure handling.
- Keep scripts out of the base template unless a downstream project requires
  them.
- Update `skills/index.md` whenever a skill is added, renamed, removed, or given
  a new trigger.
- Document subagent recommendations only when they match the user's actual work
  environment.

## Completion Rules

- Report changed files.
- Report verification.
- Report known gaps.
- Record durable lessons in this file only when they should affect future work.
