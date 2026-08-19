---
name: release
description: Prepare safe, traceable software releases without publishing prematurely. Use for version bumps, changelogs, release notes, tags, release candidates, compatibility checks, packaging, and release-readiness reviews.
---

# Release

## Workflow

1. Confirm the requested release target, versioning scheme, base commit, release channel, and whether preparation or actual publication is authorized.
2. Inspect the repository's existing release process, automation, package metadata, changelog format, and protected-branch rules.
3. Determine the change set from the previous release boundary. Group user-visible changes, fixes, breaking changes, migrations, deprecations, and security notes.
4. Verify version numbers remain consistent across authoritative manifests and generated lock or metadata files.
5. Run the documented test, build, packaging, and artifact checks appropriate to the release. Verify reproducibility or checksums when the project supports them.
6. Draft concise release notes that explain user impact and required actions; do not copy unverified commit messages as facts.
7. Review the final diff and confirm there are no secrets, debug artifacts, or unrelated changes.
8. Stop before tagging, publishing packages, deploying, or creating a public release unless the user explicitly authorized that exact action and target.

## Delivery checklist

- State the proposed version and previous release reference.
- List changed files and generated artifacts.
- Record every validation command and result.
- Call out breaking changes, migrations, rollback considerations, and remaining manual approvals.
