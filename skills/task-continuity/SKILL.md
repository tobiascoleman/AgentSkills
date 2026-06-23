---
name: task-continuity
description: Keep concise task notes outside chat history across coding sessions. Use when starting, resuming, handing off, summarizing, updating, or closing ongoing coding tasks across chats; triggers include open a task, track this bug, continue, resume, handoff, task note, snapshot, tomorrow, close the task, context reset, new chat, where were we, and reduce token usage.
---

# Task Continuity

Use this skill to preserve task state across chats without relying on long conversation history.

## Storage

- Task notes live in `${CODEX_HOME:-$HOME/.codex}/tasks`.
- The helper command is `${CODEX_HOME:-$HOME/.codex}/scripts/codex-task`.
- Notes are Markdown files and may be edited directly.

## Starting A Task

1. Create a note with `codex-task new <slug> "<goal>" [repo ...]`.
2. Keep the goal, repos, decisions, blockers, and next steps concise.
3. Record only durable task context that would help another session resume work.

## Resuming A Task

1. Read the note with `codex-task show <slug>`.
2. Inspect `git status --short` and recent commits for any listed repos.
3. Continue from the latest snapshot, decisions, and next steps.

## Updating A Task

- Add a repo snapshot with `codex-task update <slug> [repo ...]`.
- Add a short note with `codex-task note <slug> "<decision, blocker, or next step>"`.
- Prefer one clear sentence over a transcript-style summary.

## Closing A Task

- Mark completion with `codex-task note <slug> "Complete: <what was finished>"`.
- Include any final validation or known follow-up in the same note.

## Guardrails

- Do not store secrets, tokens, passwords, private credentials, or customer data.
- Do not commit or share task notes by default.
- Keep repo-specific conventions in the repo's own documentation instead of task notes.
- Keep notes short enough that they reduce context load instead of recreating it.
