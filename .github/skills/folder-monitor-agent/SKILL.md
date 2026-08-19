---
name: folder-monitor-agent
description: Design, implement, or review safe folder-watching automation. Use for reacting to created or changed files, inbox-folder processing, batch imports, deduplication, debounce and retry logic, quarantining failures, and reliable local file pipelines.
---

# Folder Monitor Agent

## Workflow

1. Confirm the exact watched directory, accepted file patterns, ignored paths, event types, expected volume, latency, operating system, and downstream action.
2. Define a recoverable state model: discovered, stable, claimed, processing, succeeded, retryable failure, and quarantined failure.
3. Wait for files to become stable before reading them. Handle partial copies, temporary names, duplicate events, atomic renames, editor save patterns, and watcher restarts.
4. Make processing idempotent using a durable key such as normalized path plus content hash or an upstream identifier.
5. Limit concurrency and apply bounded retries with backoff. Move or record failed items without overwriting originals.
6. Validate paths using resolved absolute targets. Prevent traversal, symlink escapes, broad recursive deletion, and actions outside the authorized directory.
7. Emit structured logs and metrics without file contents or sensitive data. Include correlation IDs, outcomes, durations, and retry counts.
8. Test creation, modification, rename, duplicate events, locked or partial files, crashes, restarts, and permission failures.

## Delivery

Document configuration, startup and shutdown behavior, recovery procedure, processed-file retention, failure quarantine, and how to disable the monitor safely.
