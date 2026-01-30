# Idea: SpecFlow Lifecycle Extension

**Proposed by:** @mellanon
**Date:** 2026-01-31

## Problem

SpecFlow + Maestro handles Spec → Build → Test well. But the pipeline has gaps after the build:

| Phase | Today | Missing |
|-------|-------|---------|
| Contrib Prep | — | Extract from private trunk, sanitize, stage |
| Review | — | Independent AI review (auditor ≠ builder) |
| Release | — | PR packaging, changelog, contribution workflow |
| Maintain | — | Versioned spec evolution post-merge |

## Proposal

Four new playbooks for the SpecFlow bundle:

1. **Contrib Prep** — `INVENTORY → SANITIZE → EXTRACT → VERIFY → TEST → STAGE → GATE → PUBLISH`
2. **Review** — `SCOPE → ARCH → EVAL → SECURITY → PERF → DOCS → REPORT → GATE`
3. **Release** — Based on SpecFirst Release Framework (9 human approval gates)
4. **Open Spec** — Living document: baseline + change proposals + version history

## Status

Promoted to `projects/specflow-lifecycle/`.
