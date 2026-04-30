# Skills Index

This folder stores reusable workflow playbooks. Keep this file current as the
index for all skills in this repository.

The base template intentionally includes only this index. Add real skills in
downstream projects when a workflow repeats often enough to deserve its own
document.

## Current Skills

No project-specific skills are included yet.

When you add one, replace the example row below:

| Skill | Path | Use When |
| --- | --- | --- |
| Example skill | `skills/<skill-name>/skill.md` | Example trigger condition |

## When To Create A Skill

Create a skill when you keep repeating the same instructions, checklist, command
sequence, or verification routine.

Good skill scopes:

- Publish a blog post.
- Review a pull request.
- Prepare a PDF document.
- Triage unread email.
- Deploy a specific project.

Too broad:

- Do all project work.
- Handle documents.
- Manage every external service.

## Recommended Skill Structure

```text
skills/
└── skill-name/
    └── skill.md
```

Use this content shape:

```markdown
# Skill Name

## Purpose

What this skill helps the agent do.

## Use When

- Trigger condition 1
- Trigger condition 2

## Inputs

- Required file, URL, command, credential, or user decision

## Steps

1. Read the relevant files.
2. Perform the workflow.
3. Verify the result.
4. Report changed files and known gaps.

## Verification

- Command or checklist used to confirm the result.

## Failure Handling

- What to do when a dependency, credential, or command is missing.
```

## Rules

- Keep each skill focused.
- Keep examples short.
- Put private credentials in local `.env` files, never in skill documents.
- Prefer deterministic checks where possible.
- Add scripts only in downstream projects, not in this base template.
- Update this index whenever a skill is added, renamed, removed, or given a new
  trigger.
- Configure subagents for the user's actual workflow. If a skill should be
  delegated to a specialist agent, document the recommended model, scope, and
  handoff conditions in that skill or in this index.
