# Solution Scout

A lightweight **research-before-build** meta-skill for deciding whether to adopt, wrap, fork, borrow from, build, or ignore existing solutions before implementing a non-trivial capability.

## Why

A common engineering failure mode is starting implementation before answering:

1. Does this already exist?
2. Does the existing solution actually work well?
3. Does it fit our exact constraints?
4. If we do not adopt it, what can we still learn or reuse from it?

Solution Scout standardizes that decision.

## Workflow

```text
Need
  ↓
Capability framing
  ↓
Discover
  ├─ products/services
  ├─ OSS/libraries/CLIs
  ├─ skills/MCPs/plugins/workflows
  └─ code/issues/PR prior art
  ↓
Verify
  ↓
Fit matrix
  ↓
Small realistic trial
  ↓
Extract borrowable ideas
  ↓
ADOPT / WRAP / FORK / BORROW / BUILD / IGNORE
  ↓
Decision record
```

## Typical prompts

```text
Use Solution Scout before implementing this feature: <feature>.
Find existing solutions and prior art, verify the strongest candidates, and recommend ADOPT/WRAP/FORK/BORROW/BUILD/IGNORE.
```

```text
Scout this need: <need>.
I care most about <constraints>. Do not start implementation until the research gate is complete.
```

```text
Before adding <feature> to this repo, search this codebase and GitHub for existing implementations, issues, PRs, libraries, skills, MCPs, and design patterns. Run a small trial if needed and extract ideas even from rejected candidates.
```

## Files

- `SKILL.md` — compact router and core workflow.
- `references/search-strategy.md` — deeper discovery and prior-art search.
- `references/evaluation-rubric.md` — hard gates and fit scoring.
- `references/trial-protocol.md` — realistic smoke/A-B tests.
- `references/prior-art.md` — design inspirations.
- `templates/decision-record.md` — durable decision record.

## Integration model

`SKILL.md` is the source of truth. Agent-specific adapters should point to or package this directory rather than duplicating the full workflow.

Recommended behavior for an agent-level rule/prompt:

```text
Before implementing a non-trivial new capability, run the Solution Scout research gate unless the task is trivial glue, an obvious local bug fix, or an explicitly approved throwaway spike.
```

This keeps the default prompt small while allowing progressive disclosure into the reference files only when needed.

## Design principle

**Do not build blindly. Do not adopt blindly either.**
