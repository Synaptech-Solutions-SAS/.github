# Security policy

## Reporting a vulnerability

Please don't report security vulnerabilities through public issues, pull
requests, or discussions: that exposes the problem before it can be fixed.

Report them privately by email to **g.martinez@synaptech-solutions.com**, with a
subject line that starts with `[Security]` and names the affected repository:

```
[Security] repository-name: short description of the problem
```

## What to include in your report

Apart from the information you'd give in any bug report (what happened, what
you expected, and your environment), please include:

- **Affected repository and component:** the file, endpoint, or module involved.
- **Affected version:** the version, branch, or commit where you found it.
- **Type of vulnerability:** for example, injection, broken authentication or
  authorization, or exposure of credentials or personal data.
- **Steps to reproduce:** the minimal steps, and a proof of concept if you have
  one.
- **Impact:** what an attacker could do, and what access or conditions they'd
  need.
- **Suggested fix or mitigation**, if you have one.
- **Disclosure:** whether you've shared this with anyone else, and how you'd
  like to be credited.

Don't include real user data, credentials, or secrets in your report. If
they're part of the problem, describe them instead.

## What to expect

Projects in this organization are maintained alongside a business, but
security reports take priority over other work:

- You'll get an acknowledgment within 7 days.
- Once the report is confirmed, you'll be kept informed about the fix and its
  timeline.
- When the fix is released, you'll be credited in the release notes or
  advisory, unless you prefer to remain anonymous.

If a report isn't considered a vulnerability, you'll get an explanation of why.

## Coordinated disclosure

Please keep the vulnerability confidential until a fix is released or 90 days
have passed since your report, whichever comes first, unless we agree on a
different date together.

## Supported versions

Security fixes are made on the latest version of each project's default
branch. Older versions and releases don't receive fixes unless the
repository's README says otherwise.

## Scope

- Vulnerabilities in third-party dependencies should be reported to their
  maintainers. If one affects a project here, please let us know as well.
- There's no bug bounty program: reports are welcome, but they aren't paid.
