# Document-Based Agent Harness Template

A minimal, document-based harness for coding agents and workflow agents.

This template does not ship an app, package, or runtime. It provides a repeatable
folder structure and Markdown contracts that help an agent load context, follow
local rules, use skills, and leave useful state for the next session.

## What This Is

An agent harness is the control layer around an LLM-driven workflow. In this
template, the control layer is expressed as documents:

- `agent.md` defines the workspace operating contract.
- `context/tacit.md` stores durable rules, preferences, and lessons.
- `context/memory.example.md` shows how to keep cross-session state.
- `context/task.example.md` shows how to keep active work visible.
- `skills/index.md` lists available skills and defines how to write reusable
  skill documents.

Use this when you want your agent to behave consistently across sessions without
building a full custom SDK or CLI.

## Folder Structure

```text
.
├── README.md
├── agent.md
├── .gitignore
├── context/
│   ├── tacit.md
│   ├── memory.example.md
│   └── task.example.md
├── skills/
│   └── index.md
└── ko/
    ├── README.md
    ├── agent.md
    ├── .gitignore
    ├── context/
    │   ├── tacit.md
    │   ├── memory.example.md
    │   └── task.example.md
    └── skills/
        └── index.md
```

## Quick Start

1. Create a repository from this template.
2. Copy the example state files:

```bash
cp context/memory.example.md context/memory.md
cp context/task.example.md context/task.md
```

3. Open the repository in your agent tool.
4. Tell the agent to read `agent.md` first.
5. Add project-specific rules to `context/tacit.md`.
6. Add reusable workflows under `skills/` as Markdown documents when needed.
7. Update `skills/index.md` whenever you add, rename, or remove a skill.

## Korean Edition

A Korean version of the same template is available in `ko/`.

To start a Korean-only repository, copy the contents of `ko/` to your project
root and use that folder structure as the base template.

## Tool Notes

Different agent tools load project instructions differently.

- If your tool auto-loads `AGENTS.md`, copy or symlink `agent.md` to `AGENTS.md`.
- If your tool auto-loads `CLAUDE.md`, copy or symlink `agent.md` to `CLAUDE.md`.
- If your tool supports custom skills, place skill folders under `skills/` or
  adapt the structure to that tool's expected skill directory.

This template intentionally keeps the source documents neutral and portable.

## Design Rules

- Keep instructions short, explicit, and operational.
- Store reusable behavior in Markdown before adding scripts.
- Keep private state in untracked files such as `context/memory.md` and
  `context/task.md`.
- Do not commit secrets, tokens, personal schedules, or private customer data.
- Update memory after meaningful decisions so the next session can continue.

## Suggested Skill Shape

When you add a real skill later, prefer this shape:

```text
skills/
└── my-skill/
    └── skill.md
```

Keep each skill focused on one workflow. Add scripts only inside your private
project when a Markdown playbook is not enough.
