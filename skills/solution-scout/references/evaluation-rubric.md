# Evaluation Rubric

Use this when multiple candidates look plausible or the dependency is consequential.

## Hard gates

A candidate should normally be rejected before scoring if any non-negotiable constraint fails, for example:

- cannot satisfy a must-have capability;
- incompatible license for the intended use;
- unacceptable security/privacy model;
- cannot run in the required environment;
- requires an unavailable proprietary dependency;
- appears abandoned and would create unacceptable maintenance risk;
- integration cost is clearly larger than building the needed subset.

A hard-gate failure can still leave the candidate useful as **BORROW** prior art.

## Weighted fit score

Use a 0–5 score for each dimension. Suggested weights:

| Dimension | Weight | What to evaluate |
|---|---:|---|
| Must-have coverage | 35% | Does it solve the actual required behavior, not merely adjacent problems? |
| Trial / evidence quality | 15% | Did it work on a realistic task? Are claims backed by tests/docs/source? |
| Integration cost | 15% | Setup, adapters, migration, deployment, operational complexity. Higher score = lower cost. |
| Maturity / reliability | 10% | Stability, tests, releases, production evidence, failure handling. |
| Maintenance health | 10% | Recent activity, maintainer responsiveness, release cadence, issue health. |
| Extensibility | 5% | Can it absorb likely future requirements without a rewrite? |
| License / security / ops fit | 10% | License clarity, dependency risk, privacy, security posture, platform fit. |

Weighted score = sum(score / 5 × weight).

Do not treat the numeric score as authoritative. It exists to expose assumptions and close calls.

## Suggested interpretation

- **85–100** — strong ADOPT/WRAP candidate if no hidden blocker exists.
- **70–84** — viable; compare integration cost and strategic fit carefully.
- **50–69** — usually BORROW, targeted WRAP, or niche use rather than broad adoption.
- **<50** — normally IGNORE, except for isolated prior art.

## Fit matrix template

| Candidate | Must-have | Evidence/trial | Integration | Maturity | Maintenance | Extensibility | License/Sec/Ops | Verdict |
|---|---:|---:|---:|---:|---:|---:|---:|---|
| A |  |  |  |  |  |  |  |  |
| B |  |  |  |  |  |  |  |  |
| C |  |  |  |  |  |  |  |  |

## Maintenance signals

Positive signals:

- recent releases or meaningful commits;
- active issue triage;
- tests and CI maintained alongside features;
- clear ownership/maintainers;
- migration notes and compatibility policy;
- users reporting successful current deployments.

Warning signals:

- README promises features absent from source/tests;
- years-old release with unresolved breakage in current environments;
- many severe issues with no maintainer response;
- dependency chain pinned to obsolete versions;
- frequent breaking changes with weak migration guidance;
- bus factor of one combined with declining activity.

A stable, feature-complete project does not need constant commits. Judge maintenance relative to what the project actually requires.

## Integration cost checklist

Consider more than installation:

- data migration;
- authentication and secrets;
- deployment topology;
- new databases/services;
- monitoring and backups;
- compatibility adapters;
- upgrade burden;
- local developer setup;
- agent/tool permissions;
- latency/token/API cost;
- failure recovery;
- vendor lock-in or fork burden.

## Verdict guidance

### ADOPT

Choose when coverage is strong, evidence is good, and custom work would mostly duplicate a healthy solution.

### WRAP

Choose when the core is right but local interfaces, policy, or UX need a thin adaptation layer.

### FORK

Choose only when sustained divergence is expected and owning upstream merge/maintenance cost is justified.

### BORROW

Choose when the project itself is a poor dependency but contains strong prior art.

### BUILD

Choose when must-haves are genuinely unmet, integration cost is disproportionate, constraints are incompatible, or the required subset is materially simpler than adopting the alternatives.

### IGNORE

Choose when neither adoption nor its prior art provides enough value to justify complexity.
