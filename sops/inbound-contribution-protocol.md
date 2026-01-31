# SOP: Inbound Contribution Processing

How to process external contributions when they arrive as pull requests to the shared blackboard.

## Why This Exists

pai-collab has SOPs for outbound contribution (extracting code from your private trunk) but the inbound side — receiving and processing external PRs — was undocumented. This SOP codifies the pattern established through processing the first external contribution (PR #12).

Every PR to the shared blackboard is a trust boundary crossing. This protocol ensures contributions are reviewed consistently, follow-up work is tracked, and the community has visibility into how decisions are made.

## Pipeline

```
RECEIVE → ASSESS → REVIEW → DECIDE → MERGE → FOLLOW UP → JOURNAL → ANNOUNCE
```

## Three Concerns (Cleanly Separated)

| Phase | Question It Answers | SOP |
|-------|-------------------|-----|
| **Inbound Processing** | "How do we handle this PR?" | This document |
| **Review** | "Is this good code?" | [review-format.md](review-format.md) |
| **Outbound Contrib Prep** | "Is this safe to share?" | [contribution-protocol.md](contribution-protocol.md) |

## Steps

### 1. Receive

A PR arrives via fork-and-PR. Before reading the content:

- Check the contributor's trust zone in `CONTRIBUTORS.yaml` (repo-level) and the relevant `PROJECT.yaml` (project-level)
- If the contributor is **untrusted** (default for all new contributors), apply full review intensity — content scanning, tool restrictions per [TRUST-MODEL.md](../TRUST-MODEL.md)
- If the contributor is **trusted**, apply standard review intensity

### 2. Assess

Read the PR diff. Understand what's being added, changed, or removed:

- What files are touched?
- Is this a new project registration, a project update, a process change, or a structural modification?
- Does it touch policy documents (SOPs, TRUST-MODEL.md, CONTRIBUTING.md)? If so, escalate to maintainer review regardless of contributor trust zone
- Does the PR follow the expected patterns from [CONTRIBUTING.md](../CONTRIBUTING.md)?

### 3. Review

Run a structured review. For significant PRs, use the Council debate pattern:

**Council Debate (recommended for non-trivial PRs):**
- Architect: evaluates structural fit with existing repo patterns
- Engineer: evaluates implementation quality and buildability
- Security: evaluates risk, trust implications, and attack surface
- Researcher: provides external context, precedent, and alternative approaches

The Council produces a recommendation: merge, request changes, or reject.

**For simple PRs** (typo fixes, minor documentation updates), a single-reviewer assessment is sufficient.

For review output format, follow [review-format.md](review-format.md).

### 4. Decide

The maintainer makes the final call based on review findings:

- **Merge** — PR meets standards, no outstanding concerns
- **Request changes** — PR has merit but needs modification. Comment with specific, actionable feedback.
- **Reject** — PR doesn't fit the project direction or introduces unacceptable risk. Comment with explanation.

### 5. Merge

If merging:
- Merge the PR
- Post a comment on the PR acknowledging the contribution
- Reference any follow-up issues created (see step 6)

### 6. Follow Up

Identify gaps or follow-up work exposed by the contribution:

- **Missing structure** — Does the project need a `projects/` directory with PROJECT.yaml, README, JOURNAL?
- **Documentation gaps** — Did the contribution pattern reveal unclear onboarding docs?
- **Process improvements** — Did the review process surface SOP gaps?
- **Trust model updates** — Does the contributor need to be added to CONTRIBUTORS.yaml?

Create issues for each follow-up item. Assign to the appropriate person. Reference the original PR.

### 7. Journal

Update the relevant project's `JOURNAL.md`:

- What PR was processed
- How it was reviewed (Council debate, single review, etc.)
- What was decided and why
- What follow-up issues were created
- What emerged — insights, pattern observations, process improvements

If no project journal exists yet (because the PR created a new project), create the journal as part of follow-up (step 6).

### 8. Announce

Draft a community announcement (Discord or relevant channel):

- What was merged
- How it was reviewed (transparency builds trust)
- What follow-up was created
- Keep it concise — the journal has the full detail

## Worked Example: PR #12

The first external contribution to pai-collab followed this exact pattern:

| Step | What Happened |
|------|--------------|
| **Receive** | PR #12 from @jcfischer — registering Ivy agent and pai-secret-scanning |
| **Assess** | Two-line change to REGISTRY.md. New project registration, not a structural change. |
| **Review** | Council debate with four agents. Security pushed for immediate merge (scanning tooling shouldn't wait). Architect flagged missing project directory structure. |
| **Decide** | Merge now, track structural follow-up as issues. |
| **Merge** | PR merged, comment posted referencing follow-up issues. |
| **Follow Up** | Issue #13 (project directory for pai-secret-scanning), Issue #14 (contribution docs clarity). |
| **Journal** | Four entries in `projects/pai-secret-scanning/JOURNAL.md` documenting the full lifecycle. |
| **Announce** | Discord message summarizing the review process and follow-ups. |

## References

- [TRUST-MODEL.md](../TRUST-MODEL.md) — Trust zones determine review intensity at step 1
- [review-format.md](review-format.md) — Review output format for step 3
- [contribution-protocol.md](contribution-protocol.md) — Outbound counterpart to this SOP
- [CLAUDE.md](../CLAUDE.md) — Agent operating protocol (references this SOP)
