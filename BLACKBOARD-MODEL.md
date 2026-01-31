# Personal and Shared Blackboards

> **Disclaimer:** The analysis of Daniel Miessler's ULWork model is based on what he has shared publicly (screenshots, posts, and the [ULWork repository](https://github.com/danielmiessler/ULWork)). It may not fully represent his implementation. We use it here as a reference point because it inspired pai-collab's design.

---

## The Two-Level Model

Many PAI operators maintain their own system of record — a personal repo, PAI's built-in `WORK/` directory, or something like Daniel Miessler's ULWork model (GitHub as system of record with `TASKLIST.md`, Issues, SOPs, and deep context).

pai-collab is not a replacement for any of these. It's the **shared coordination layer on top**.

```
┌─────────────────────────────────┐     ┌─────────────────────────────────┐
│   Operator A's Personal Board   │     │   Operator B's Personal Board   │
│                                 │     │                                 │
│  All your work, your context,   │     │  All your work, your context,   │
│  your agents, your priorities   │     │  your agents, your priorities   │
│                                 │     │                                 │
│  PROJECT.yaml ──────────────────┼──┐  │  PROJECT.yaml ──────────────────┼──┐
└─────────────────────────────────┘  │  └─────────────────────────────────┘  │
                                     │                                       │
                                     ▼                                       ▼
                    ┌────────────────────────────────────────┐
                    │     pai-collab (Shared Blackboard)      │
                    │                                        │
                    │  Only what involves other people:       │
                    │  • Shared project milestones            │
                    │  • Review requests                      │
                    │  • Community coordination                │
                    │  • Shared SOPs and processes             │
                    │                                        │
                    │  Code lives in project repos ───────────┼──→ github.com/...
                    └────────────────────────────────────────┘
```

Your personal board tracks everything you care about. pai-collab tracks only the work that involves other people.

---

## How It Works in Practice

### What stays on your personal board

- Your full task list and priorities
- Your agents, their configuration, and their context
- Your project branches and local development state
- Your notes, learnings, and personal knowledge base
- Internal execution steps (build, test, fix cycles)

### What comes to the shared blackboard

- **Project milestones** — "Signal v1.0 ready for review" not "fix flaky test in hook runner"
- **Review requests** — "Please review the observability pipeline architecture"
- **Shared process deliverables** — Maestro playbooks, SOPs, PAI skills that others will use
- **Community coordination** — "Who wants to work on the SpecFlow contrib-prep playbook?"
- **Journey logs** — JOURNAL.md captures what happened and what emerged, feeding the learning loop

### The connection point: PROJECT.yaml

Each project on the shared blackboard has a `PROJECT.yaml` that points to where the code lives:

```yaml
source:
  repo: mellanon/pai
  branch: feature/signal-agent-2
  paths:
    - Observability/
    - hooks/ToolUseInstrumentation.hook.ts
```

This is the bridge between personal and shared. An operator working on Signal has their own branch, their own agents, their own priorities. When they need coordination — a review, a milestone check, a process question — that happens on the shared blackboard.

---

## The Learning Loop

Both levels share a feedback loop, but they operate at different scopes:

```
Personal Board                          Shared Blackboard
─────────────                          ─────────────────
Work on feature                        Coordinate across operators
  ↓                                      ↓
Learn from implementation              Learn from collaboration
  ↓                                      ↓
Update personal notes/context          Update shared SOPs via PR
  ↓                                      ↓
Better personal execution              Better shared processes
```

The shared loop is slower and more deliberate — SOPs change via pull request, not automatic bot updates. This is intentional: when multiple operators share a process, changes need review.

JOURNALs are where these loops connect. A project JOURNAL captures "What Emerged" during work. Those learnings inform SOP update PRs, which improve the shared process for everyone.

---

## Comparison: ULWork vs pai-collab

Daniel Miessler's ULWork model is designed for a single operator managing their own work. pai-collab extends the same principles for multi-operator collaboration. The differences are intentional:

| Daniel's ULWork (single operator) | pai-collab (multi-operator) | Why different |
|-----------------------------------|----------------------------|---------------|
| `TASKLIST.md` as dashboard | GitHub Issues with label filtering | Multiple operators can't share one task list |
| Bots auto-update SOPs | SOPs updated via human PR | Multiple operators need review before process changes |
| Single board for all work | Two-layer: personal + shared boards | Each operator has their own context |
| Direct write access | Fork + PR model | Access control for multiple contributors |
| One operator's agents | Multiple operators' agents + daemon registry | Agent discovery across operators |
| Workers: Human, Digital Assistant, Digital Employee | Workers: Multiple humans, each with their own agents | Scale from 1 to N operators |
| Context is centralized | Context is distributed (personal) + coordinated (shared) | Privacy and autonomy per operator |

### What we share with the ULWork model

- **GitHub as system of record** — The repo is the source of truth, not chat or docs
- **Issues for dynamic work** — Static files describe the system; issues describe the work
- **SOPs as process knowledge** — How we work is documented and versioned
- **Learning loop** — Work → Learn → Update Repo → Better Work

### What we add

- **Multi-operator coordination** — The blackboard pattern (Hayes-Roth, 1985) applied to community collaboration
- **Daemon registry** — Agent discovery across operators via MCP
- **Contribution protocol** — Tag-before-contrib, fork + PR, sanitization gates
- **Two-layer separation** — Your work stays yours; shared work is explicit

---

## Example: How an Operator Joins

1. **Set up personal board** — PAI installation with `WORK/` directory, or your own GitHub-based system
2. **Fork pai-collab** — Your fork is your working copy of the shared blackboard
3. **Browse issues** — Find work that interests you, filtered by project and type labels
4. **Work on your board** — Execute locally with your own agents, your own branch, your own priorities
5. **Coordinate on the shared board** — When you hit a milestone, need a review, or want to share a deliverable, open or update an issue / submit a PR
6. **Journal what emerged** — Update the project JOURNAL with learnings that benefit others
7. **Propose process improvements** — If you found a better way, submit an SOP update PR

The two levels work together: personal boards for execution, shared blackboard for coordination.
