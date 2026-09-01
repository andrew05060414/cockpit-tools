---
name: solution-scout
description: >
  Research-before-build workflow for non-trivial features, libraries, services,
  integrations, agent capabilities, and subsystems. Finds existing solutions,
  verifies real fit, runs a small trial when practical, extracts reusable prior
  art, and chooses ADOPT / WRAP / FORK / BORROW / BUILD / IGNORE before implementation.
---

# Solution Scout

Default bias: **find before build, verify before adopt**.

Use this skill before implementing a non-trivial capability when research is cheap relative to build and maintenance cost.

## Trigger

Run Solution Scout when one or more are true:

- A new feature, subsystem, service, library, integration, agent capability, MCP, plugin, or workflow is proposed.
- The request sounds like “I need X”, “does something already do X?”, “should we build this?”, or “how do others implement this?”.
- A proposed feature is likely to have existing open-source or commercial prior art.
- The implementation would create a long-lived dependency or maintenance burden.
- The user wants ideas for a feature even if no existing project is adopted wholesale.

Shrink or skip the workflow for:

- trivial glue code or project-local helpers;
- obvious bug fixes with a known local cause;
- tiny UI changes;
- explicitly approved throwaway spikes/prototypes;
- emergencies where research cost exceeds expected implementation cost.

## Core workflow

### 0. Frame the capability

Translate the request into capabilities before searching.

Capture:

- **Goal** — what outcome is needed?
- **Must-have** — required behavior.
- **Nice-to-have** — useful but optional.
- **Constraints** — stack, deployment model, privacy, license, latency, cost, platform, maintenance, interoperability.
- **Acceptance test** — what would prove that a candidate actually solves the problem?

Do not search only the user’s original wording. Generate synonyms and implementation-level terms.

### 1. Discover in four lanes

Search these independently because they answer different questions:

1. **Ready-made product/service** — can we use something directly?
2. **Open-source project/library/CLI** — can we adopt, embed, or wrap it?
3. **Agent skill / MCP / plugin / workflow** — is the capability already packaged for agents?
4. **Prior art** — even if we reject a project, do its code, architecture, issues, PRs, schemas, tests, or UX contain useful ideas?

Search the current codebase first when the feature may already exist partially.

For deeper search tactics, load `references/search-strategy.md`.

### 2. Verify candidates

Do not equate popularity with fitness.

For each serious candidate, verify from primary evidence where possible:

- Does it really support the must-haves?
- Is it actively maintained or at least stable enough for the use case?
- Are releases/commits/issues consistent with a healthy project?
- Is setup and operation compatible with the target environment?
- What are the license, security, privacy, and dependency implications?
- Is the feature documented and exercised in examples/tests, or only claimed in marketing/README text?
- What are the known failure modes and open issues?

Prefer docs, source, tests, changelog, issues, and PRs over star count or summary pages.

### 3. Build a fit matrix

Compare only the strongest candidates. Usually 2–5 is enough.

Score or describe:

- must-have coverage;
- maturity/reliability;
- integration cost;
- maintenance health;
- trial quality;
- extensibility;
- license/security/operational fit.

Use `references/evaluation-rubric.md` when the decision is consequential or candidates are close.

### 4. Trial the top candidates

When practical, run the smallest realistic test using the acceptance test from step 0.

A useful trial answers: **Does this work for our actual task, in our actual constraints?**

Do not turn scouting into a full migration. Time-box it.

Use `references/trial-protocol.md` for the test format.

### 5. Extract borrowable ideas

This step is mandatory even when no candidate is adopted.

Look for reusable:

- architecture and component boundaries;
- algorithms and indexing strategies;
- schemas and data models;
- API/CLI design;
- caching, retry, synchronization, and consistency patterns;
- prompts and agent orchestration patterns;
- UX flows and naming;
- tests, benchmarks, fixtures, and edge cases;
- issue/PR discussions that document failed approaches;
- operational lessons and deployment patterns.

Respect licenses. “Borrow” means learn from or reuse only where licensing permits; it does not mean copy incompatible code.

### 6. Make exactly one primary decision

Use one of these verdicts:

- **ADOPT** — use the solution largely as-is.
- **WRAP** — use it as the core and add a thin adapter or compatibility layer.
- **FORK** — the foundation fits, but sustained source-level divergence is justified.
- **BORROW** — do not adopt the project; reuse its ideas, architecture, tests, or permitted implementation details.
- **BUILD** — implement ourselves because existing options fail important requirements or cost more than they save.
- **IGNORE** — interesting, but not worth integrating or borrowing for this need.

A BUILD decision must include a short reason explaining why the strongest existing options are insufficient.

### 7. Leave a decision record

For non-trivial decisions, record enough context that the same research does not need to be repeated later.

Use `templates/decision-record.md`.

## Stop rules

Stop researching when any of these is true:

- one candidate clearly satisfies the must-haves with acceptable integration/maintenance cost;
- additional searches are returning duplicates rather than new solution classes;
- 2–5 credible candidates have been compared and the remaining uncertainty requires hands-on implementation rather than more browsing;
- the research budget is approaching the expected cost of simply building the capability.

Do not chase exhaustive coverage.

## Default output

Keep routine output compact:

**Capability → candidates → evidence → fit → trial → borrowable ideas → verdict → why → next action**

For small tasks, a short table plus verdict is enough. For consequential architecture decisions, include the full fit matrix and decision record.

## Progressive disclosure

Load supporting files only when needed:

- `references/search-strategy.md` — query generation, search lanes, GitHub prior-art search.
- `references/evaluation-rubric.md` — hard gates and weighted comparison.
- `references/trial-protocol.md` — realistic smoke/A-B trial design.
- `references/prior-art.md` — inspirations and related workflows.
- `templates/decision-record.md` — durable research record.

## Principle

The goal is not “never build.” The goal is to avoid building blindly.
