# Signal — Project Telos

## Mission

Build an observability stack for PAI that makes agent behaviour visible, measurable, and debuggable.

## What It Does

PAI Signal provides end-to-end observability: JSONL event logging, OTLP tracing, VictoriaMetrics storage, and Grafana dashboards. It captures session lifecycle, tool usage, agent spawning, and performance metrics — all running in a local Docker stack.

## Current State

- **18 features** implemented from spec
- **708 tests** passing (L1–L4 acceptance levels)
- **25,000 lines** from Maestro + ~9,800 lines human hardening
- Working end-to-end on private branch `feature/signal-agent-2`
- Needs: extraction from private trunk, independent review, PR packaging

## Success Criteria

- [ ] Clean contrib branch with only Signal files (~102 files)
- [ ] Independent community review completed
- [ ] PR merged to upstream `danielmiessler/PAI`
- [ ] At least one community member running the observability stack

## Key Challenge

The code works but is AI-generated at scale. "Works" ≠ "merge-ready." Need independent review for architectural fit, code style, redundancy, edge cases, and whether it follows PAI conventions.

## The 80/20 Split

| Who | Commits | Lines | Nature |
|-----|---------|-------|--------|
| Maestro | 255 | ~25,500 | Autonomous feature implementation from spec |
| Human | 11 | ~9,800 | Integration fixes, infrastructure gaps, emergent features |

Human-touched code deserves more review scrutiny — it was written to fix what the machine got wrong.

## References

- [Signal Spec (Gist)](https://gist.github.com/mellanon/62a12ddef60ca7ff74331c2983fb43c7)
- [Maestro PAI Playbooks](https://github.com/mellanon/maestro-pai-playbooks)
