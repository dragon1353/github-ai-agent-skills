---
name: documentation
description: Create and maintain documentation that matches the repository's actual behavior. Use for README updates, setup guides, API references, architecture notes, tutorials, runbooks, examples, changelogs, and documentation reviews after code changes.
---

# Documentation

## Workflow

1. Identify the audience, task they need to complete, and the source of truth for each claim.
2. Read the existing documentation structure and terminology before editing.
3. Verify commands, file paths, configuration keys, defaults, prerequisites, and examples against code or reliable project sources.
4. Organize content from purpose and prerequisites to the shortest successful path, then add options, troubleshooting, and references only when useful.
5. Use concise language, descriptive headings, accessible link text, and copyable examples. Define unavoidable jargon on first use.
6. Preserve the project's voice and avoid duplicating information that already has one authoritative home.
7. Validate examples and links when tools are available. Review the rendered structure as well as the raw Markdown.
8. Report what was updated, which claims were verified, and anything that still needs maintainer confirmation.

## Quality bar

- Never document a command or feature from memory when the repository can verify it.
- Distinguish required steps from optional recommendations.
- Use placeholders instead of real secrets, account identifiers, or personal data.
- State version-specific behavior explicitly and avoid unsupported promises about future behavior.
- Update nearby navigation or tables of contents when headings or files move.
