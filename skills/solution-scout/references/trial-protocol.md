# Trial Protocol

Use a trial when documentation alone cannot answer whether a candidate fits the real task.

## Goal

The trial is not a benchmark contest. It is the smallest realistic experiment that can change the adoption decision.

## 1. Define one representative task

Choose a task from the real use case, not a toy chosen to make the candidate look good.

Write:

- input/context;
- expected outcome;
- must-pass conditions;
- optional quality signals;
- maximum acceptable setup/runtime cost.

Example:

> Given a function that changed several times, identify why the current implementation exists and return evidence linking the answer to commits, PRs, or prior agent sessions.

Must-pass might include:

- finds the relevant change;
- explains the reason accurately;
- provides provenance;
- works against the target repository;
- does not require unreasonable manual preparation.

## 2. Keep the environment fair

For multiple candidates:

- use the same representative task;
- provide equivalent inputs and permissions;
- avoid hand-tuning one candidate far more than another;
- note configuration differences that are intrinsic to the products.

When useful, compare against the current/manual baseline.

## 3. Measure what matters

Possible dimensions:

- success/failure on must-pass criteria;
- output correctness;
- provenance/citation quality;
- setup effort;
- latency;
- API/token/compute cost;
- operator intervention;
- reliability across a few repetitions;
- quality of failure messages/recovery;
- compatibility with the target stack.

Do not collect metrics that cannot affect the decision.

## 4. Time-box

Default to a smoke test, not a migration.

Stop if:

- a hard blocker is found;
- setup already exceeds the acceptable integration budget;
- the candidate clearly passes the acceptance test;
- additional repetitions are not resolving meaningful uncertainty.

## 5. Record surprises

Capture:

- undocumented setup requirements;
- behavior that contradicts README/docs;
- missing features discovered only during use;
- surprisingly good sub-features;
- operational friction;
- useful implementation ideas even if the candidate is rejected.

These observations often matter more than the nominal benchmark number.

## 6. Trial result template

```text
Candidate:
Task:
Environment:

Must-pass:
- [ ] criterion 1
- [ ] criterion 2
- [ ] criterion 3

Observed:
- Correctness:
- Setup effort:
- Runtime/latency:
- Cost:
- Reliability:
- Provenance/debuggability:

Surprises:

Verdict impact:
```

## A/B for agent skills

When evaluating a prompt/skill/workflow itself, prefer an A/B comparison when feasible:

- A: agent performs the task without the candidate skill/workflow;
- B: agent performs the same task with it;
- compare task success first, then latency/token cost and operator effort.

A skill that produces prettier output but does not improve task success or reduce effort should not automatically be adopted.
