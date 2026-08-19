# Repository Agent Instructions

## Scope

These instructions apply to the entire repository. Follow a more specific `AGENTS.md` when one exists nearer to the files being changed.

## Working agreement

- Read the relevant files and current diff before editing.
- Keep changes focused on the requested outcome; preserve unrelated user work.
- Use the matching Skill under `.github/skills/` when the task fits its description.
- Prefer the smallest maintainable change that addresses the root cause.
- Do not invent commands, APIs, test results, file contents, or repository state.
- Never print, commit, or expose credentials, tokens, private keys, personal data, or secret values.
- Ask for explicit confirmation before releases, deployments, destructive operations, permission changes, or other external side effects unless the user already authorized that exact action.

## Validation

- Run the narrowest relevant check first, then broader checks when risk warrants it.
- Treat existing failures separately from failures caused by the change.
- Report the commands run and their outcomes. If a check cannot run, explain why.
- For documentation-only changes, verify paths, commands, examples, headings, and links against the repository.

## Review and delivery

- Review the final diff for correctness, security, accidental generated files, and scope creep.
- Add or update tests when behavior changes.
- Keep commits cohesive and use clear, imperative commit messages.
- Summarize what changed, why it changed, validation performed, and any remaining risk.
