# Document-Based Agent Harness Template

> A lightweight Markdown harness for coding agents, workflow agents, and
> long-running personal automation projects.

[![Template](https://img.shields.io/badge/type-template-111827)](#quick-start)
[![Markdown](https://img.shields.io/badge/built_with-Markdown-2563eb)](#folder-structure)
[![Language](https://img.shields.io/badge/language-EN%20%2F%20KO-16a34a)](#korean-edition)

This repository is a **document-first agent harness**. It does not ship an app,
package, CLI, or SDK. Instead, it gives an agent a clear set of Markdown files
for context, task state, durable tacit knowledge, and reusable skills.

Use it when you want an agent to behave consistently across sessions without
building a custom runtime.

## Why This Exists

LLM agents work better when the operating rules are explicit. A short prompt is
easy to lose. A documented workspace is easier to inspect, reuse, and improve.

This template gives you a small control layer:

| Layer | File | Purpose |
| --- | --- | --- |
| Root contract | `agent.md` | What the agent must read and how it should work |
| Tacit knowledge | `context/tacit.md` | Durable rules, preferences, lessons, and index notes |
| Session memory | `context/memory.example.md` | Example format for cross-session project memory |
| Task state | `context/task.example.md` | Example format for active work and decisions |
| Skill index | `skills/index.md` | Skill catalog, authoring rules, and subagent notes |

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

Create live state files from the examples:

```bash
cp context/memory.example.md context/memory.md
cp context/task.example.md context/task.md
```

Then open the repository in your agent tool and tell the agent:

```text
Read agent.md first, then follow the required reading order.
```

After that:

1. Add project-specific operating rules to `context/tacit.md`.
2. Track active work in `context/task.md`.
3. Record durable decisions in `context/memory.md`.
4. Add repeatable workflows under `skills/`.
5. Update `skills/index.md` whenever a skill changes.

## Core Rules

- Keep `agent.md` as the root operating contract.
- Keep `context/tacit.md` as the current tacit knowledge index.
- Keep `skills/index.md` as the current skill index.
- Store live private state in `context/memory.md` and `context/task.md`.
- Do not commit secrets, tokens, private schedules, customer data, or local
  credentials.
- Configure skills and subagents for your actual workflow. This template only
  provides the structure.

## Suggested Skill Shape

When you add a real skill later, prefer this shape:

```text
skills/
└── my-skill/
    └── SKILL.md
```

Each skill should describe:

- when to use it
- required inputs
- step-by-step workflow
- verification checks
- failure handling
- optional subagent delegation rules

## Tool Notes

Different agent tools load project instructions differently.

| Tool behavior | Recommended setup |
| --- | --- |
| Auto-loads `AGENTS.md` | Copy or symlink `agent.md` to `AGENTS.md` |
| Auto-loads `CLAUDE.md` | Copy or symlink `agent.md` to `CLAUDE.md` |
| Supports custom skills | Adapt `skills/` to that tool's skill directory |
| Does not auto-load files | Explicitly tell the agent to read `agent.md` first |

The template intentionally stays portable and tool-neutral.

## Korean Edition

A Korean version of the same template is available in `ko/`.

To start a Korean-only repository, copy the contents of `ko/` to your project
root and use that folder structure as the base template.

## What This Is Not

This is not:

- an npm package
- an agent SDK
- a hosted runtime
- a prompt collection
- a replacement for tool-specific documentation

It is a minimal workspace contract for agents that already know how to read
files, follow instructions, and use tools.
