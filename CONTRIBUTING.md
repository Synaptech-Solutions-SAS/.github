# Contributing to Synaptech Solutions

Thank you for your interest in contributing! These guidelines apply to every
repository in this organization unless a repository provides its own
CONTRIBUTING.md. For setup, build, and testing instructions, see each
repository's README.

By participating, you agree to follow our
[Code of Conduct](https://github.com/Synaptech-Solutions-SAS/.github/blob/main/CODE_OF_CONDUCT.md).

## Finding something to work on

Issues labeled `good first issue` are a good starting point if you're new to a
project, and `help wanted` marks issues where outside contributions are
especially welcome. Leave a comment on the issue before you start so others
know you're working on it.

## Before you start

- Search existing issues and pull requests to avoid duplicates.
- If the repository uses a spec-driven workflow (see
  [Planning significant changes](#planning-significant-changes)), check its
  planned work. What you want to report or propose may already be planned:
  - **OpenSpec** repositories (with an `openspec/` directory): browse the
    folders in `openspec/changes/`, ignoring `archive/`, which holds completed
    changes. If you have the CLI installed, `openspec list` shows the same.
  - **agent-skills** repositories: check `SPEC.md`, `tasks/todo.md`, and
    `docs/ideas/`.

  If what you have in mind is already covered, there's no need to open an
  issue. If it's related but not fully covered, mention the change or spec by
  name in your issue.
- Read the repository's `CLAUDE.md`, if it has one. It records the project's
  decisions and conventions, and the order in which planned changes will be
  implemented, which is the context you need before picking up work. If you use
  Claude Code, it's loaded automatically.
- For anything beyond a small fix, open an issue first to discuss the change.
  This helps make sure your effort fits the project's direction before you
  invest time in it.

## Basic requirements

Every contribution, whether AI-assisted or not, must meet these requirements.
Pull requests that don't meet them may be sent back for changes or closed.

1. **Bug reports include the relevant information.** Follow the checklist in
   [Reporting bugs](#reporting-bugs). A bug that can't be reproduced can't be
   fixed.
2. **Pull requests explain why the change exists.** Describe the problem it
   solves or the need it addresses, not just what changed. The diff already
   shows *what*; only you can explain *why*. Link the related issue if there
   is one.
3. **Code is commented where it matters.** Explain the reasoning behind
   non-obvious decisions, workarounds, and edge cases. Document public
   functions, classes, and modules following the conventions of the language
   and repository. Avoid comments that only restate what the code does.
4. **Code has been double-checked.** Review your own diff before requesting a
   review: remove debug output, commented-out code, and unrelated changes, and
   make sure the project builds and all existing tests and checks pass locally.
5. **Changes include unit tests.** New features need tests covering the
   expected behavior and relevant edge cases. Bug fixes need a test that fails
   without the fix and passes with it. If a change can't reasonably be unit
   tested (for example, documentation or configuration only), explain why in
   the pull request description.
6. **Documentation is updated.** If your change affects how something is
   installed, configured, or used, update the README and any related
   documentation in the same pull request.

## Reporting bugs

Use the bug report form when opening an issue. It asks for:

- What happened and what you expected to happen.
- Steps to reproduce the problem.
- Your environment (OS, runtime and dependency versions, project version).
- Relevant logs, error messages, or screenshots.

**Security vulnerabilities:** do not open a public issue. Follow the
[security policy](https://github.com/Synaptech-Solutions-SAS/.github/blob/main/SECURITY.md) to report them privately.

## Suggesting features

Describe the problem you're trying to solve before proposing a solution. A
clear problem statement makes it much easier to evaluate the idea. For anything
substantial, follow [Planning significant changes](#planning-significant-changes).

## Planning significant changes

Projects in this organization are built spec-first: research and feature
analysis come before any code. Each repository uses one of two workflows:

- **[OpenSpec](https://github.com/Fission-AI/OpenSpec)** (the repository has an
  `openspec/` directory): explore the idea with `/opsx:explore`, then create a
  change proposal with `/opsx:propose`. The proposal lives in
  `openspec/changes/<change-name>/`.
- **[agent-skills](https://github.com/addyosmani/agent-skills)** (the repository
  has a `SPEC.md`): refine the idea with the `idea-refine` skill
  (`/idea-refine`), then write or update the spec with `/spec`.

If you're unsure which workflow a repository uses, ask in the issue.

New features, significant refactors, and architectural changes should follow
this process:

1. **Research first.** In the issue, describe the problem, who it affects, what
   already exists in the codebase, and the alternatives you considered.
2. **Produce the planning artifact** for the repository's workflow: an OpenSpec
   change, or a spec (and, optionally, an idea document).
3. **Get feedback on the plan before implementing it**, either in the issue or
   as a draft pull request that contains only the planning artifacts. Reviewing
   a plan takes minutes; discovering after weeks of work that an implementation
   went in the wrong direction costs everyone far more.
4. **Implement against the approved plan**, and link the plan from your pull
   request.

You don't need to use any particular AI tool. Both workflows support many AI
assistants, and their artifacts are plain Markdown you can also write by hand.
What matters is the artifact, not the tool that produced it.

Small fixes, such as typos, documentation tweaks, or contained bug fixes, don't
need a planning artifact.

## Submitting a pull request

1. Fork the repository and create a branch from the default branch.
2. Keep each pull request focused on a single logical change. Don't mix
   refactoring or formatting changes with behavior changes.
3. Follow the [commit message convention](#commit-messages). Signing off your
   commits is [strongly recommended](#signing-off-your-commits-dco).
4. Make sure your change meets the [basic requirements](#basic-requirements).
5. Fill in the pull request template: why the change is needed, what changed,
   how users will notice it, how you tested it, what's out of scope, any manual
   steps, and whether AI tools were used.

### Commit messages

Write the subject line in the imperative mood ("Add", "Fix", not "Added" or
"Fixes"), in sentence case, without a trailing period, and under 72
characters. If the commit implements a planned change or a review finding, add
its identifier in parentheses:

```
Validate discount amounts in the seller form
Fix the month rollover in the overdue check (change 09)
```

Use the body to explain what was wrong and what the commit changes, so the
history makes sense without opening the pull request. If the commit breaks
existing behavior, say so explicitly in the body.

### Signing off your commits (DCO)

Signing off is not mandatory, but it is strongly recommended. A sign-off
certifies, under the
[Developer Certificate of Origin](https://developercertificate.org/), that you
wrote the contribution or otherwise have the right to submit it under the
project's license. For AI-assisted work, it's also your recorded statement that
you take responsibility for the code's origin.

Sign off with the `-s` flag:

```
git commit -s -m "Fix the month rollover in the overdue check (change 09)"
```

This adds a `Signed-off-by: Your Name <your.email@example.com>` line using your
Git configuration. To sign off your last commit after the fact, run
`git commit --amend --no-edit --signoff`.

**Commits made by AI tools.** Some tools, such as Claude Code in cloud
sessions, commit under their own identity. A sign-off should come from the
commit's author, so re-author those commits under your name and sign them off
in one pass, then update your branch:

```
git rebase --exec "git commit --amend --no-edit --reset-author --signoff" origin/main
git push --force-with-lease
```

Replace `origin/main` with the branch you started from. The tool's
`Co-Authored-By:` trailer is kept, so it remains credited. Do this before
writing the pull request description, because rewriting changes the commit
hashes. A sign-off added by an AI tool in its own name doesn't count: the
certificate is a statement only a person can make.

### Code style

Use the linters, formatters, and type checkers configured in each repository,
and run them before pushing. Follow the existing style of the code you're
changing. Don't reformat code unrelated to your change: it hides the real
change in the diff and makes review slower.

### Dependencies

Add new dependencies only when they're genuinely needed. For each one:

- Explain in the pull request why it's needed and why existing dependencies or
  the standard library aren't enough.
- Verify that it's the real, actively maintained package from the expected
  publisher by checking its registry page and source repository, not just its
  name. AI tools sometimes suggest packages that don't exist, and malicious
  packages are sometimes published under those names.
- Confirm that its license is compatible with the project's.
- Commit the lockfile changes along with it.

### Breaking changes

If your change breaks existing behavior, APIs, configuration, or data formats:

- Discuss it in an issue before implementing it.
- Say so explicitly in the commit body.
- Mark it in the "Behavior changes" section of the pull request template,
  explaining who is affected and how to migrate.

## Review times

Projects in this organization are maintained alongside a business, so the time
available for open source is limited. Reviews and replies may take a while,
sometimes several weeks. A slow response doesn't mean your contribution was
ignored or is unwelcome.

- If 30 days pass without a response, one polite follow-up on the issue or pull
  request is welcome.
- Reviews may go through several rounds of requested changes.
- Pull requests waiting on changes from the contributor may be closed after 30
  days without activity. You're welcome to reopen them when you're ready to
  continue.
- Pull requests waiting on a maintainer are never closed for inactivity.

## AI-assisted contributions

We accept contributions made with the help of AI tools (code assistants, chat
models, agents, and similar), provided the conditions below are met.

### Due diligence

In addition to the basic requirements, by submitting an AI-assisted
contribution, you confirm that:

- **You understand the problem.** You know what you're trying to achieve and
  why, and you could describe it without the tool's help.
- **You understand the solution.** You have read all of the generated content
  and can explain, at least conceptually, how it works and why it solves the
  problem.
- **You have verified it.** You have run and tested it, considered edge cases,
  and confirmed that every API, dependency, and reference it uses actually
  exists.
- **You have checked licensing.** To the best of your knowledge, the
  contribution does not reproduce code under a license incompatible with the
  project's.
- **You take responsibility.** You are the author of record, whatever name the
  commit metadata shows, and are accountable for the contribution as if you had
  written every line yourself. "The AI wrote it" is not an acceptable answer
  during review.

A simple test: if a maintainer asks "why does this work?" or "why this
approach?", you should be able to answer in your own words.

### Disclosure

AI use must be disclosed in the "AI assistance" section of the pull request
template, including:

- The tool or tools used.
- What they were used for (for example: implementation, tests, refactoring,
  documentation).
- How you reviewed and verified the output.

Minor assistance, such as single-line autocompletion or spelling and grammar
fixes, does not need to be disclosed.

Commits made with an AI tool should also credit it with a `Co-Authored-By:`
trailer. Claude Code and several other tools add it automatically, and GitHub
shows it as a co-author on the commit:

```
Co-Authored-By: Claude <noreply@anthropic.com>
```

A trailer or a "Generated with" footer shows that a tool was involved, but it
doesn't replace the "AI assistance" section of the pull request template,
which also covers what the tool was used for and how you verified its output.

### Maintainer discretion

Maintainers may decline any AI-assisted contribution at their sole discretion,
without any obligation to justify the decision. This is not a judgment of you
as a contributor: reviewing generated code takes significant time, and
maintainers need to be able to protect it.

Contributions found to contain undisclosed AI-generated content may be closed
without review.

## License

By contributing, you agree that your contributions will be licensed under the
license of the repository you are contributing to.

## Questions

If something isn't covered here, open a discussion or an issue in the relevant
repository.
