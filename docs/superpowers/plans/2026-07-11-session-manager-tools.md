# Session Manager Tools Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Let users open a session rollout directly and filter normal conversations, external runs, and subagent runs with accurate token-status text.

**Architecture:** Extend the existing Rust session snapshot and Tauri command surface, then wire the new fields/actions through the existing TypeScript service, store, and session-manager component. Reuse Tauri's opener plugin and existing session discovery; add no dependencies.

**Tech Stack:** Rust, Tauri 2, React 19, TypeScript, i18next.

---

### Task 1: Open rollout file

**Files:**
- Modify: `src-tauri/src/modules/codex_session_manager.rs`
- Modify: `src-tauri/src/commands/codex_instance.rs`
- Modify: `src-tauri/src/lib.rs`
- Modify: `src/services/codexInstanceService.ts`
- Modify: `src/stores/useCodexInstanceStore.ts`
- Modify: `src/components/codex/CodexSessionManager.tsx`
- Modify: `src/locales/en.json`
- Modify: `src/locales/zh-CN.json`

- [ ] Add a Rust resolver that returns the unique rollout path for a session ID and errors clearly for zero or multiple matches.
- [ ] Add and register a Tauri command that opens the resolved rollout path with the system default application.
- [ ] Expose the command through the TypeScript service and store.
- [ ] Add a file icon action beside copy-ID and open-location with translated tooltip text.
- [ ] Add Rust unit coverage for unique, missing, and ambiguous rollout resolution.
- [ ] Run targeted Rust tests and TypeScript typecheck.

### Task 2: Classify and filter session types

**Files:**
- Modify: `src-tauri/src/modules/codex_session_manager.rs`
- Modify: `src/types/codex.ts`
- Modify: `src/components/codex/CodexSessionManager.tsx`
- Modify: `src/locales/en.json`
- Modify: `src/locales/zh-CN.json`

- [ ] Add a serialized `session_type` value to each session record: `normal`, `external`, or `subagent`.
- [ ] Classify parent-linked, `thread_source=subagent`, and `source.subagent` records as subagents; classify top-level non-Codex originators as external; classify remaining records as normal.
- [ ] Add Rust unit tests for Codex Desktop, Multica, Claude Code, guardian, and explorer metadata.
- [ ] Add a compact frontend filter defaulting to normal conversations and supporting external, subagent, and all records.
- [ ] Preserve search, group selection, export, and trash behavior against the filtered list.
- [ ] Display input/output when available, total-only when input/output are zero but total is positive, and no token label when statistics are unavailable.
- [ ] Run targeted Rust tests, TypeScript typecheck, and production build.

### Task 3: Workspace rebind discovery

**Files:**
- Create: `docs/superpowers/investigations/2026-07-11-session-workspace-rebind.md`

- [ ] Trace every current Codex state location that stores or derives thread workspace binding.
- [ ] Separate display-only grouping metadata from runtime cwd and Desktop saved-project mappings.
- [ ] Document supported fields, close-process requirements, backup boundary, validation checks, and unresolved version-specific risks.
- [ ] Stop after investigation if an atomic, reversible write contract cannot be demonstrated.
