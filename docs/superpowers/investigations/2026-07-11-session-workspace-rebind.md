# Codex Session Workspace Rebind Investigation

## Conclusion

A safe rebind cannot be implemented as a single SQLite update. Current Codex stores or derives a thread workspace in multiple layers, while the official app-server protocol already supports an explicit cwd override on resume and turn start.

## Persisted state

- The rollout `session_meta.payload.cwd` is the canonical cwd used when Codex rebuilds thread metadata.
- `state_5.sqlite.threads.cwd` is the indexed cwd used for thread listing and filtering.
- `.codex-global-state.json` contains Desktop-owned `thread-workspace-root-hints`, saved workspace roots, project order, projectless thread IDs, and per-thread writable roots.
- Later `turn_context.cwd` values describe individual turns, but current state extraction deliberately keeps a non-empty session-meta cwd as the thread cwd.

## Runtime behavior

- App-server `thread/resume` accepts an optional `cwd` override.
- App-server `turn/start` accepts an optional cwd override documented to apply to that turn and subsequent turns.
- Cockpit cannot assume that editing Desktop global state alone changes the runtime cwd of an already running thread.

## Required safety contract

1. Stop every Codex process using the affected Codex home.
2. Validate that the target path is absolute and exists.
3. Back up the rollout, SQLite database, session index, and Desktop global state before writing.
4. Update the canonical rollout session metadata and indexed SQLite cwd.
5. Update the thread's Desktop workspace-root hint without rewriting unrelated saved projects or project order.
6. Rebuild or reopen through the official app-server and verify that thread listing reports the target cwd.
7. Resume with an explicit cwd override and verify thread settings before reporting success.
8. Restore the complete backup if any validation fails.

## Blocker

The Desktop global-state schema is not part of the public Rust protocol and may change independently of Codex CLI/app-server versions. Implementation should remain blocked until Cockpit defines and tests version-aware parsing for `thread-workspace-root-hints`; otherwise a local repair could change sidebar grouping without reliably changing execution context.

## Related upstream requests

- openai/codex#25498: move threads between projects and expose project binding APIs.
- openai/codex#15347: remap moved workspace paths without losing thread history.
