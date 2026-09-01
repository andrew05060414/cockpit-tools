# Prior Art and Inspirations

Solution Scout intentionally combines several ideas that commonly appear separately.

## AVID `research-before-build`

Repository: `AVIDS2/avid-skill`

Relevant idea:

- default to a time-boxed scan before building a non-trivial subsystem;
- decide reuse / wrap / build;
- avoid blocking trivial glue code or explicitly approved spikes.

Solution Scout extends this with:

- explicit capability framing;
- multiple discovery lanes;
- candidate verification;
- fit matrix/rubric;
- realistic trials;
- prior-art extraction even from rejected candidates;
- ADOPT / WRAP / FORK / BORROW / BUILD / IGNORE verdicts;
- durable decision records.

## Agent skill evaluation / A-B testing

A useful general pattern from agent-skill evaluators is to test the same representative task with and without a skill/workflow, then compare task success before optimizing secondary metrics such as latency or token usage.

Solution Scout applies that idea to any candidate integration, not only prompts or agent skills.

## Competitive / feature analysis

Feature matrices and gap analysis are useful, but Solution Scout treats them as engineering-decision tools rather than market analysis. The important question is not “which project has more features?” but “which option satisfies our must-haves with the lowest justified long-term cost?”

## Core synthesis

The combined workflow is:

**Need → Discover → Verify → Compare → Trial → Borrow → Decide → Record**

The point of this file is attribution and design context, not a runtime dependency. Solution Scout should remain usable without any of the referenced projects installed.
