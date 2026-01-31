# Signal — Open Spec

> **Status: Concept — not yet implemented in SpecFlow**

## What This Should Be

Open Spec is a living document that tracks what's shipped (baseline), what's proposed (change proposals with impact analysis), and what happened (version history). It feeds back into SpecFlow for the next build cycle:

```
Open Spec (baseline + CPs) → CP approved → SpecFlow cycle → ship → Open Spec (updated baseline)
```

This is different from a CHANGELOG (backward-looking, just facts) and a SpecFlow SPEC (forward-looking, greenfield). Open Spec is both — it knows what exists and what's next.

## What Exists Today

SpecFlow's `.specify/specs/` directory contains 18 feature specifications for Signal:

| Feature | Spec | Status |
|---------|------|--------|
| F-1: Event Schema and Types | `.specify/specs/f-1-event-schema-and-types/spec.md` | Complete |
| F-2: Event Logging Library | `.specify/specs/f-2-event-logging-library/spec.md` | Complete |
| F-3: Concurrent Write Handling | `.specify/specs/f-3-concurrent-write-handling/spec.md` | Complete |
| F-4: PII Scrubbing | `.specify/specs/f-4-pii-scrubbing/spec.md` | Complete |
| F-5–F-9: Hook Instrumentation | `.specify/specs/f-5-*/` through `f-9-*/` | Complete |
| F-10: CLI Query Patterns | `.specify/specs/f-10-cli-query-patterns/spec.md` | Complete |
| F-11–F-14: Vector Pipeline | `.specify/specs/f-11-*/` through `f-14-*/` | Complete |
| F-15: Docker Compose Stack | `.specify/specs/f-15-docker-compose-stack/spec.md` | Complete |
| F-16: Skill Invocation Enforcement | `.specify/specs/f-16-*/spec.md` | Complete |
| F-17: OTLP Hook Instrumentation | `.specify/specs/f-017-*/spec.md` | Complete |
| F-18: F-018 | `.specify/specs/f-018-*/spec.md` | Complete |

Each feature has `spec.md` (requirements with SHALL/MUST + Given/When/Then), `plan.md` (architecture), and `tasks.md` (implementation breakdown). These artifacts represent the **v1.0.0 baseline** but live in the source repo, not here.

## What's Missing

SpecFlow is purely build-phase: SPECIFY → PLAN → TASKS → IMPLEMENT → COMPLETE. Once `specflow complete` runs, the feature is frozen. There is no mechanism for:

- **Baseline tracking** — summarizing what shipped as a reference for future changes
- **Change proposals** — structured proposals with impact analysis against the baseline
- **Version history** — what changed between versions and why
- **Feed-back loop** — approved CPs becoming new SpecFlow specs for the next cycle

The closest thing in SpecFlow today is the "Evolution Vectors" section in `plan.md` templates — planning for change at design time, but not executing changes post-ship.

## The Gap

This is part of the [SpecFlow Lifecycle Extension](../specflow-lifecycle/) project. The Open Spec concept needs to be designed and implemented as either:
- A Maestro playbook that generates a baseline from completed SpecFlow artifacts
- A SpecFlow bundle extension that adds `specflow openspec` commands
- A PAI skill (`bin/openspec/`) that manages baselines and change proposals

Signal would be the first project to use it — the 18 completed specs become the v1.0.0 baseline, and post-merge evolution is tracked through change proposals.

## References

- [SpecFlow Lifecycle Extension](../specflow-lifecycle/) — the project to build this
- [SpecFlow Bundle](https://github.com/jcfischer/specflow-bundle) — the upstream tool (build-phase only today)
- [SOPs README](../../sops/README.md) — full lifecycle tooling maturity matrix
