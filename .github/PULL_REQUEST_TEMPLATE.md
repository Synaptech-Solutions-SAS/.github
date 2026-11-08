<!--
Thanks for contributing to Synaptech Solutions!

Please read the contributing guidelines before opening this pull request:
https://github.com/Synaptech-Solutions-SAS/.github/blob/main/CONTRIBUTING.md

How to fill in this template:
- Replace every [text in square brackets] with your answer.
- Sections marked "if applicable" can be deleted when they don't apply.
- Don't write inside these comment markers: anything inside them is hidden in the published pull request.
- Replies may take a while: this organization is maintained alongside a business.
-->

## Why

[What problem does this solve, or what need does it address? Describe what was wrong or missing before this change, and who it affects.]

## Related work

- **Issue:** Closes #[issue number]
- **Planning artifact:** [OpenSpec change (`openspec/changes/<name>`) or spec (`SPEC.md`), or "None" for small fixes]
- **Builds on:** [other pull requests this depends on or follows, or "None"]

## Type of change

<!-- Check all that apply. -->

- [ ] Bug fix
- [ ] New feature
- [ ] Refactor (no behavior change)
- [ ] Performance
- [ ] Security
- [ ] Documentation
- [ ] Tests only
- [ ] Build, CI, or configuration
- [ ] Dependencies

## What changed

[Short summary of the change.]

<!--
If the pull request implements several planned changes or review findings, give each one its own subsection with its identifier, for example:

### Change 04: retry failed webhooks
- What was wrong.
- What changed, and where.
-->

## Behavior changes

<!-- What users will notice: defaults, output, interface, sound, performance. Repeat the block for each area, or replace it with "None". -->

- **Area:** [what changes]
  - **Before:** [previous behavior]
  - **After:** [new behavior]

- [ ] No breaking changes
- [ ] This pull request introduces a breaking change

**Who is affected and how to migrate:** [only for breaking changes; otherwise delete this line]

## How was this tested?

- **Tested on commit:** [short hash]
- **Environment:** [OS, runtime and versions, database]
- **Unit tests:** [command and result]
- **Linters and formatters:** [command and result]
- **CI:** [link to the run and result]
- **Manual checks:** [what you verified by hand, and how]

<!-- Add lines for integration, browser, migration, or benchmark runs. -->

- [ ] New tests fail without this change and pass with it
- [ ] All existing tests pass locally

## Screenshots, recordings, or audio (if applicable)

[For visible or audible changes, attach before and after.]

## Performance (if applicable)

[Benchmarks before and after, how they were measured, and on what hardware.]

## Security and data (if applicable)

<!-- Check everything this change touches. -->

- [ ] Authentication or authorization
- [ ] Payments or money handling
- [ ] Secrets, credentials, or tokens
- [ ] Personal or user data
- [ ] Input validation or file uploads

**How it was handled:** [for each checked item, what you did to keep it safe]

## Dependencies (if applicable)

<!-- Repeat the block for each package. -->

- **Package:** [name and version; added, updated, or removed]
  - **Why it's needed:** [why existing dependencies or the standard library aren't enough]
  - **License:** [license name]

- [ ] Each new package is the real, maintained one from the expected publisher
- [ ] Lockfile changes are included

## Database and migrations (if applicable)

- [ ] Migrations are included
- [ ] Upgrade and downgrade were tested on seeded data
- [ ] Models and schema are in sync

## Not in this pull request

[What is deliberately out of scope, known limitations, and follow-ups, or "None".]

## Before and after merging (if applicable)

- [ ] Configuration or environment variables to set: [list them]
- [ ] Migrations to run
- [ ] Manual steps, documented in: [file or link]
- [ ] OpenSpec changes to archive, or the next planned change: [name]
- [ ] `CLAUDE.md` updated

## Notes for the reviewer

[Where to start, the riskiest parts, and anything you're unsure about. On large pull requests, suggest a review order.]

## AI assistance

<!-- Check one. -->

- [ ] No AI tools used beyond minor assistance (single-line autocompletion, spelling or grammar fixes)
- [ ] AI tools were used

<!-- If AI tools were used, fill in the three lines below; otherwise delete them. A "Generated with" footer alone is not a disclosure. -->

- **Tools:** [names and versions]
- **Used for:** [implementation, tests, refactoring, documentation...]
- **How I verified the output:** [what you read, ran, and checked]

---

## Checklist

**Before opening**
- [ ] I checked existing issues, pull requests, and planned work for duplicates
- [ ] I read the repository's `CLAUDE.md`, if it has one
- [ ] This pull request contains a single logical change

**Code**
- [ ] I reviewed my own diff and removed debug output, commented-out code, and unrelated changes
- [ ] Code is commented where the reasoning isn't obvious
- [ ] Linters, formatters, and type checkers pass

**Tests and documentation**
- [ ] I added or updated unit tests, or explained above why that isn't possible
- [ ] I updated the documentation affected by this change

**Commits**
- [ ] Commit messages follow the convention (imperative subject under 72 characters, with the change ID when relevant)
- [ ] Commits are signed off (DCO), which is strongly recommended
- [ ] AI-assisted commits credit the tool with a `Co-Authored-By:` trailer

**Responsibility**
- [ ] I can explain how and why this change works in my own words
