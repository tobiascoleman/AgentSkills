---
name: pr-handoff
description: Generate pull request descriptions with human-authored sections plus an agentic handoff. Use when the user asks to print out the PR description for these changes, create a PR description, PR handoff, test instructions for a PR, affected areas, reviewer guidance, or wants an agent-authored technical handoff while preserving author-completed intent, impact, issue, dependency, and test sections.
---

# PR Handoff

Create a PR description with two parts:

1. Human-authored sections the PR author should complete or has explicitly provided.
2. An agentic handoff populated from implementation evidence.

## Output Shape

Default to this structure:

```markdown
# Intent

[AUTHOR MUST COMPLETE]

Describe:
- Why this change exists
- What problem it solves
- What is intentionally out of scope

# Affected Areas

[AUTHOR MUST COMPLETE]

Describe:
- APIs or routes affected
- Database records or workflows affected
- Kafka producers or consumers affected
- Kubernetes resources or controllers affected
- User interfaces affected
- External integrations affected
- Operational processes affected

# Related Issues

Closes:

# Test Procedure

[AUTHOR MUST COMPLETE]

Describe:
- Required setup
- Manual validation steps
- Expected behavior
- Edge cases reviewed

---

# Agentic Handoff
```

If the user explicitly supplies content for a human-authored section, preserve it. Otherwise keep `[AUTHOR MUST COMPLETE]` and only include short prompts for what the author should put there.

Do not infer or invent values for human-authored sections. In particular, do not fill `Intent`, `Affected Areas`, `Related Issues`, or `Test Procedure` unless the user supplied that text.

## Agentic Handoff

Populate only this section from code, diffs, tests, command output, or user-provided facts.

Use these subsections:

```markdown
## Scope Summary

## Technical Changes

## Risk Assessment

## Reviewer Focus Areas

## Validation Performed

## Known Limitations
```

Keep the handoff factual and reviewer-oriented.

- Scope Summary: changed components, services, APIs, data flow, infrastructure.
- Technical Changes: meaningful implementation details and behavior changes; skip categories that were not affected.
- Risk Assessment: realistic compatibility, auth, migration, event, performance, operational, or concurrency risks.
- Reviewer Focus Areas: specific logic or boundaries worth reviewing.
- Validation Performed: only checks actually run or explicitly reported.
- Known Limitations: incomplete work, assumptions, deferred follow-up, or `Unable to determine from the implementation.`

## Rules

- Never replace `[AUTHOR MUST COMPLETE]` with inferred content.
- Never claim validation that was not actually performed.
- If a fact cannot be determined from the implementation, write `Unable to determine from the implementation.`
- Keep the final PR description readable in under two minutes.
- Prefer concrete route names, table names, command names, and service names over broad summaries when they are present in evidence.
