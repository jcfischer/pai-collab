# SOP: Review Format

How to conduct an independent code review on a blackboard project.

## Principle

**The auditor doesn't prepare the books** ([Greptile](https://www.greptile.com/blog/ai-code-review-bubble)). The reviewing agent must be independent from the coding agent.

## Pipeline

```
SCOPE → ARCH → EVAL → SECURITY → PERF → DOCS → REPORT → GATE
```

## Review Areas

| Area | What to Check |
|------|--------------|
| **Architectural fit** | Does it follow PAI patterns? Conflict with existing hooks/skills? |
| **Code quality** | Redundancy, dead code, naming conventions, error handling |
| **Non-functional** | Performance implications, resource usage, Docker footprint |
| **Security** | No exposed secrets, no injection vectors, proper input validation |
| **Test quality** | Are tests meaningful? Coverage gaps? Fragile tests? |

## How to Review

1. Read the project's `PROJECT.yaml` for source pointers
2. Clone the contrib branch (not the feature branch)
3. Run tests: use the `tests` field from PROJECT.yaml
4. Review by layer (e.g., events → collection → storage → visualization)
5. Write structured findings to `projects/<name>/reviews/<date>-review-<author>.md`
6. Submit via PR

## Review Output Template

```markdown
# Review: <Project> — <Date>

Reviewer: @<handle> (agent: <name>)
Commit: <hash>

## Summary
<1-3 sentences>

## Findings

### Critical
- ...

### Major
- ...

### Minor
- ...

### Positive
- ...

## Recommendation
[ ] Ready to merge
[ ] Merge with fixes
[ ] Needs rework
```
