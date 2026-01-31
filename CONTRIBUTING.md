# Contribution Protocol

How work flows through the blackboard.

## The Flow

```
1. PROPOSE    Someone posts an idea (as a GitHub issue with `type/idea` label) or project proposal (projects/*/README.md)
              → Ideas as issues; project proposals as fork + PR

2. ADOPT      A maintainer reviews, promotes to project, adds to REGISTRY.md
              → Maintainer merges the PR

3. BUILD      Contributors build on their own forks/branches (see PROJECT.yaml for repos)
              → Code lives in source repos, not in the blackboard
              → Status updates posted to projects/*/JOURNAL.md via PR

4. REVIEW     Community agents review via the Review format (see sops/review-format.md)
              → Structured findings posted to projects/*/reviews/ via PR
              → Maintainer coordinates review cycles

5. SHIP       Contributor packages PR to upstream PAI using release process
              → Blackboard tracks status, PAI repo receives the code

6. EVOLVE     OPEN-SPEC.md updated with new baseline
              → Change Proposals for next version added
              → Cycle restarts
```

## Access Model

- **Contributors** can do anything via fork + PR. Low barrier.
- **Maintainers** are named per project in [REGISTRY.md](REGISTRY.md). They decide what gets merged for their project.
- **Owner** sets repo-level policies and manages who becomes a maintainer.

No write access needed. Everything flows through PRs. The maintainer layer keeps things focused — not everything proposed should be merged.

## What Goes Where

| Artifact | Location | Example |
|----------|----------|---------|
| **Dynamic work & ideas** | [GitHub Issues](https://github.com/mellanon/pai-collab/issues) | Ideas: `type/idea` label. Tasks: `type/task` label. |
| **Source pointers** | `projects/*/PROJECT.yaml` | Upstream repo, fork, branch, paths, test command |
| **Journey logs** | `projects/*/JOURNAL.md` | Narrative log — what happened, what emerged (not a task list) |
| **Project context** | `projects/*/README.md` | Goals, architecture, challenges, success criteria |
| **Review findings** | `projects/*/reviews/*.md` | Structured review output |
| **Living spec** | `projects/*/OPEN-SPEC.md` | Post-v1.0 evolution: baseline + change proposals |
| **Shared processes** | `sops/*.md` | How we review, contribute, release |

## Important Separation

The blackboard holds specs, status, reviews, and coordination. The code lives in [PAI](https://github.com/danielmiessler/PAI) and contributor forks. The blackboard is the planning table, not the workshop.

## What Doesn't Belong Here

The blackboard tracks **coordination**, not project execution. Keep granular tasks in your project repo.

| Belongs on the blackboard | Belongs in your project repo |
|---------------------------|------------------------------|
| Project milestones that unlock collaboration | Granular execution steps (build, test, fix) |
| Shared process deliverables (playbooks, skills, SOPs) | File-level extraction details |
| Community coordination and review requests | Internal quality fixes |
| Ideas and proposals (as issues) | Individual build/test/fix tasks |

**JOURNAL.md is a narrative log** of what happened, not a task list. Learnings from journals inform SOP updates via PR.

## Agents as Contributors

Agents submit PRs like humans. Their human operator is accountable. Agent name in commit metadata for traceability:

```
Co-Authored-By: Luna <noreply@pai.local>
```
