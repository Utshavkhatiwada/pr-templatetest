---
name: pr-template
description: Use this skill whenever the user is creating, opening, drafting, or writing a pull request (PR), or asks for help with a PR description. Trigger phrases include "open a PR", "create a pull request", "draft a PR", "PR description", "write up this PR", "submit a PR", "make a PR", and "PR for these changes". This skill ensures every PR follows PL Marketing's standard structure (Summary, Ticket/Issue, Motivation, Changes, Test, Screenshot, Risk, Rollback plan, Deployment Notes) so reviewers always get consistent context. Also use this skill any time you generate PR body text — even if the user doesn't explicitly mention a "template" — to enforce the standard format.
---

# PR Template



normal
PR Template
When drafting a pull request description, follow the structure below. Use the section headings exactly as written and in this order. Fill each section using the diff, conversation context, and any linked tickets. If you don't have enough information for a section, ask the user before guessing — never invent ticket numbers, test results, or rollback procedures.

Template
markdown
## Summary

## Ticket/Issue (if related)

## Motivation

## Changes

## Test

## Screenshot (if UI-related changes)

## Risk

## Rollback plan

## Deployment Notes

## Author Checklist

- [ ] I have personally reviewed the code I pushed
- [ ] I ran `/code-review` on my code
- [ ] I ran `/security-review` on my code
How to fill each section
Summary
One to three sentences describing what this PR does at a high level. Plain English, no jargon. A reviewer should understand the scope of the change from this alone.

Ticket/Issue (if related)
Link the Jira/GitHub issue or ticket the PR addresses (e.g., PLM-1234 or #42). If there's no related ticket, write "N/A".

Motivation
Why this change is needed — the business or technical reason. What problem does it solve, or what value does it add? Focused on the "why," not the "what."

Changes
A bulleted list of the concrete changes in the PR. Group related changes. Call out new dependencies, config changes, schema migrations, or files added/removed. This is the "what."

Test
How the change was tested. Include unit tests added or updated, manual test steps, and the environments it was verified in. For UI changes, put screenshots/recordings in the Screenshot section below. If tests weren't added, explain why.

Screenshot (if UI-related changes)
A screenshot or short recording of the UI before/after the change. Required for any user-facing UI change; write "N/A" otherwise. This section is filled in manually by the human author when they open the PR — Claude must never fabricate, embed, or describe an imaginary screenshot. When generating a PR body, Claude leaves a `TODO: attach screenshot` placeholder for the author to replace.

Risk
What could go wrong if this ships. Consider data loss, performance regressions, breaking changes for downstream consumers, security implications, and affected user-facing flows. Rate the risk informally (low / medium / high) and explain the reasoning.

Rollback plan
How to undo the change if it causes problems in production.

For database changes (schema migrations, data backfills, destructive operations): describe specific rollback steps, including any reverse migrations and data restoration procedures.
For most other code changes: "Revert the merge commit" is acceptable.
If the change is purely additive and trivially revertable, write "Revert the PR" or "N/A — change is trivially revertable."
Deployment Notes
Anything the deployer needs to know: environment variables to set, feature flags to flip, migrations to run, ordering dependencies with other PRs, or downtime requirements. If there's nothing special, write "Standard deployment, no special steps."

Author Checklist
Three checkboxes the PR author confirms before requesting review:

I have personally reviewed the code I pushed — the author read through their own diff before opening the PR.
I ran /code-review on my code — the author ran the /code-review command in Claude Code on the changes.
I ran /security-review on my code — the author ran the /security-review command in Claude Code on the changes.
These boxes MUST be left unchecked (- [ ]) when Claude generates the PR description. The human author is the only one who can truthfully tick them, after the review has actually happened.

Rules
Use the section headings exactly as written, in the order above.
Don't add, rename, or merge sections.
Render the description as Markdown with ## headings.
Leave the Author Checklist boxes unchecked (- [ ]). Never pre-check them — those confirmations belong to the human author.
For the Screenshot section, never invent, embed, or describe a screenshot. The author attaches it manually before opening the PR. When generating the body, leave a `TODO: attach screenshot` placeholder (or write "N/A" if the change has no UI impact).
If you lack information for a section, ask the user OR write TODO: <what's needed> so they can fill it in before submitting. Never fabricate content.
When NOT to use this skill
The user is reviewing a PR someone else opened, not creating one.
The user is asking about Git operations unrelated to PR descriptions (rebasing, merging, resolving conflicts, branch management).
The user is editing code without intent to open a PR.
