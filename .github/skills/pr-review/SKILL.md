---
name: pr-review
description: Review pull requests or local diffs for actionable defects. Use for code review, change-risk assessment, regression checks, security review, test-gap analysis, and requests to prioritize findings before merge.
---

# Pull Request Review

## Workflow

1. Read the request, repository instructions, PR description, changed files, and surrounding code needed to understand behavior.
2. Determine the intended behavior and trust boundaries before judging the implementation.
3. Review in this order: correctness, security, data loss, concurrency and reliability, compatibility, performance, tests, and maintainability.
4. Trace important inputs through validation, state changes, error handling, persistence, and outputs. Check callers and consumers when interfaces change.
5. Confirm each finding against the diff and current code. Avoid speculative style comments, duplicate findings, or issues outside the change unless they directly affect it.
6. Check whether tests cover success, failure, boundary, and regression paths appropriate to the change.
7. Return findings first, ordered by severity, followed by open questions and a short summary. Say explicitly when no actionable findings remain.

## Finding format

For every finding include:

- Severity: `P0` critical, `P1` high, `P2` medium, or `P3` low.
- A concise title describing the defect.
- The tightest useful file and line location.
- The concrete failure mode, affected users or systems, and conditions required to trigger it.
- A practical direction for correction without rewriting the contributor's work unnecessarily.

Do not report a finding unless a maintainer can act on it from the evidence provided.
