# Search Strategy

Use this reference when the obvious GitHub search is not enough.

## 1. Convert the request into search concepts

Write the need at three levels:

- **Outcome language** — what the user wants to achieve.
- **Capability language** — the technical capability that would produce the outcome.
- **Implementation language** — likely mechanisms, protocols, data structures, or architectural patterns.

Example:

> “I want a coding agent to know why code changed in the past.”

Possible search concepts:

- historical code context;
- agent session search;
- commit/PR provenance;
- semantic conversation search;
- decision history / engineering memory;
- code-to-conversation linking;
- provenance graph / evidence store.

Generate synonyms before concluding that nothing exists.

## 2. Search in independent lanes

### Current repository

Check first for:

- partially implemented features;
- dead/hidden code paths;
- TODOs;
- open issues;
- abandoned branches/PRs;
- adjacent modules that already solve part of the problem.

### GitHub projects

Search by:

- capability terms;
- implementation terms;
- exact protocol/library names;
- phrases from known error messages or API surfaces;
- language/ecosystem when relevant.

Do not stop at repository search. Inspect promising repositories for:

- README/docs;
- examples;
- tests;
- release history;
- open and recently closed issues;
- PRs implementing the exact feature;
- changelog entries;
- architecture/design docs.

### Package registries and official ecosystems

Depending on stack, check relevant registries or catalogs such as:

- npm;
- PyPI;
- crates.io;
- Maven/Gradle;
- Go modules;
- Homebrew;
- VS Code / JetBrains extensions;
- Docker images;
- official plugin/extension marketplaces.

### Agent ecosystem

Search separately for:

- Skills;
- MCP servers;
- plugins/extensions;
- agent templates;
- workflow packs;
- prompt libraries;
- orchestration frameworks.

A capability may already exist as an agent integration even when no standalone product has the exact name.

### Web and community evidence

Use web/community sources to discover candidates and practical failure modes, but verify important claims against primary sources.

Useful evidence includes:

- maintainer statements;
- release notes;
- issue discussions;
- migration reports;
- benchmark methodology;
- user reports that identify reproducible operational problems.

## 3. Search for prior art, not only substitutes

Once a candidate looks relevant, search within it for the exact sub-feature.

Questions to ask:

- Which file/module implements the capability?
- Which issue originally motivated it?
- Which PR introduced or redesigned it?
- What alternatives were rejected in discussion?
- What tests define the edge cases?
- What schema/API choices are reusable?

A rejected project can still be the best design reference.

## 4. Query expansion loop

If initial search is weak:

1. Take terminology from the best near-match.
2. Search those terms globally.
3. Inspect its dependencies and competitors.
4. Search issue/PR language for alternate names.
5. Repeat until new searches mostly return already-seen solution classes.

Do not repeat the same query with tiny wording changes indefinitely.

## 5. Evidence hierarchy

Prefer, roughly in this order:

1. source code and tests;
2. official docs / release notes / changelog;
3. maintainer issues and PR discussions;
4. reproducible benchmarks;
5. credible independent technical writeups;
6. community reports;
7. stars, likes, SEO pages, and unsourced summaries.

Popularity is a discovery hint, not validation.

## 6. Time-boxing

Use the smallest research budget that can change the implementation decision.

A practical default:

- quick feature: 5–10 minute equivalent scan;
- meaningful dependency/integration: compare 2–5 candidates;
- architecture-level choice: deeper source/issue/PR inspection plus a realistic trial.

Stop when further browsing is unlikely to alter ADOPT / WRAP / FORK / BORROW / BUILD / IGNORE.
