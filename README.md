# PLM PR Template

A standardized pull-request convention for PL Marketing GitHub repositories.

This repo is the canonical source for the PR template, the matching Claude Code skill, and the conventions every PLM repo should adopt. Drop these files into a target repo and you get two things for free: GitHub will pre-populate every new PR with the same structure, and Claude Code will generate PR descriptions that follow the same structure when asked.

The intent is simple — **standardize how PLM does PRs so code review becomes faster, more consistent, and harder to skip steps on**.

## Why this exists

Inconsistent PR descriptions cost reviewers time and let regressions slip through. A reviewer who has to hunt across PRs for *what changed, what was tested, what could break, and how to roll it back* burns out — and misses things. A predictable PR body with a fixed set of sections turns review into a simple checklist.

Also see: 

> [**The Perfect Pull Request — Best Practices for Collaborative Development**](https://www.deployhq.com/blog/the-perfect-pull-request-best-practices-for-collaborative-development) (DeployHQ)

Our goals:

- **Standardize** the structure of every PR opened against a PLM repo.
- **Aid code review** by making it cheap for reviewers to find the information they need in the same place every time.
- **Enforce** the convention across every PLM repo — once these files are dropped in, the rule applies automatically to every future PR.

## What's in this repo (For Now)

### `main_pr_template.md`

The bare PR template — only the `##` section headings plus the unchecked Author Checklist boxes, nothing else. Copy this into a target repo as `.github/pull_request_template.md` (or `.github/PULL_REQUEST_TEMPLATE.md`); GitHub then prefills it into every new PR's description box automatically. Authors fill in each section before requesting review.

Sections, in order:

| Section | Purpose |
|---|---|
| Summary | 1–3 sentences — what this PR does at a high level |
| Ticket/Issue (if related) | GitHub ticket reference, or `N/A` |
| Motivation | The *why* — business or technical reason |
| Changes | The *what* — bulleted list of concrete changes |
| Test | How the change was tested |
| Screenshot (if UI-related changes) | UI screenshot/recording — **attached manually by the author** |
| Risk | What could go wrong; informal low/med/high rating |
| Rollback plan | How to undo if it breaks production |
| Deployment Notes | Env vars, feature flags, ordering with other PRs |
| Author Checklist | Three confirmations the author ticks **after** reviewing |

### `SKILL.md`

A [Claude Code skill](https://docs.claude.com/en/docs/claude-code/skills) that teaches Claude to generate PR bodies in this exact format. When a developer working in a PLM repo asks Claude Code to "open a PR," "draft a PR description," "write up this PR," etc., Claude detects this skill via the trigger phrases in its YAML frontmatter and produces a PR body that matches `main_pr_template.md` heading-for-heading.

The skill also encodes the things only the human author can truthfully do — Claude is explicitly told not to do them:

- **Author Checklist boxes stay unchecked.** Claude will never pre-tick `I have personally reviewed…`, `/code-review`, or `/security-review`. Those confirmations belong to the human author after they've actually done the work.
- **Screenshots are placeholder-only.** For UI changes, Claude writes `TODO: attach screenshot` rather than fabricating, embedding, or describing an imaginary screenshot. The author attaches the real artifact when they open the PR.
- **Missing facts become `TODO:` lines, not invented content.** Claude never makes up ticket numbers, test results, or rollback procedures.

To install the skill in a repo, drop `SKILL.md` at `<repo>/.claude/skills/pr-template/SKILL.md`.

### `index.html`

A scratch file from the initial workflow testing of this convention — **not part of the template**. Safe to delete from any repo that copies this convention.

## Adopting this in a new PLM repo

1. Copy `main_pr_template.md` to `<repo>/.github/pull_request_template.md`.
2. Copy `SKILL.md` to `<repo>/.claude/skills/pr-template/SKILL.md` (or install it once per developer at `~/.claude/skills/pr-template/SKILL.md`).
3. Open a test PR and confirm the GitHub PR creation form is pre-populated with the section headings.
4. Tell the team: keep the section headings exactly as written, in the order they appear, and fill each one in.


## Further reading

- [The Perfect Pull Request — Best Practices for Collaborative Development](https://www.deployhq.com/blog/the-perfect-pull-request-best-practices-for-collaborative-development) — the article these conventions were built around.
- [GitHub: Creating a pull request template for your repository](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository) — how `.github/pull_request_template.md` is auto-detected.
- [Claude Code Skills](https://docs.claude.com/en/docs/claude-code/skills) — how Claude Code loads and triggers the `pr-template` skill.
