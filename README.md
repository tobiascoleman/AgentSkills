# Codex Skills

Small, shareable Codex skills and helper scripts.

## Included

- `pr-handoff`: generates PR descriptions with human-authored sections preserved and an agent-authored technical handoff.
- `task-continuity`: keeps concise task notes across chats using the bundled `codex-task` helper.

## Not Included

Project-specific skills, private repo conventions, saved task notes, credentials, and local environment details are intentionally excluded.

## Install

Copy a skill directory into your Codex skills directory:

```bash
mkdir -p "$HOME/.codex/skills"
cp -R skills/pr-handoff "$HOME/.codex/skills/"
cp -R skills/task-continuity "$HOME/.codex/skills/"
```

For task continuity, also install the helper script:

```bash
mkdir -p "$HOME/.codex/scripts"
cp scripts/codex-task "$HOME/.codex/scripts/"
chmod +x "$HOME/.codex/scripts/codex-task"
```

## Validate

If you have the Codex skill validator available:

```bash
python "$HOME/.codex/skills/.system/skill-creator/scripts/quick_validate.py" skills/pr-handoff
python "$HOME/.codex/skills/.system/skill-creator/scripts/quick_validate.py" skills/task-continuity
```
