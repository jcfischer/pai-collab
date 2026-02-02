# SOP: Iteration Planning

How contributors coordinate cross-project work through time-boxed iteration plans.

## Why This Exists

pai-collab tracks individual tasks (issues) and narrative history (journals), but neither answers: *"What am I doing THIS week across projects, and where does each item stand?"* When a contributor works across multiple issues and multiple projects simultaneously, they need an aggregation layer — a single artifact that ties everything together for the current cycle.

This SOP defines iteration plans as that aggregation layer, following the [VS Code Iteration Plans](https://github.com/microsoft/vscode/wiki/Iteration-Plans) model.

## Pipeline

```
SCOPE → CREATE → WORK → UPDATE → CLOSE → JOURNAL
```

## Three Contribution Modes

Not every contribution needs an iteration plan. The blackboard supports three modes:

| Mode | When | Overhead | Mechanism |
|------|------|----------|-----------|
| **Solo iteration plan** | Working across 3+ issues/projects simultaneously | Low | GitHub issue with checkboxes |
| **Multi-contributor plan** | Coordinating parallel work toward a shared milestone | Medium | GitHub issue, champion manages |
| **No plan** | Single issue, single PR, straightforward contribution | Zero | Issue-first workflow from CLAUDE.md |

**Default is no plan.** Iteration plans are opt-in when complexity warrants them.

## Steps

### 1. SCOPE

Decide what goes into this iteration.

- [ ] Review open issues you intend to work on: `gh issue list --assignee @me` or filter by project labels
- [ ] Group by project/workstream
- [ ] Identify dependencies (what blocks what)
- [ ] Set a time box (1–2 weeks recommended)
- [ ] Choose a goal — one sentence describing what "done" looks like for this iteration

### 2. CREATE

Create a GitHub issue as the iteration plan.

**Title convention:**
```
iteration: @handle — Iteration N: [Goal]
```

For multi-contributor plans:
```
iteration: [project] — Iteration N: [Goal]
```

**Labels:** `type/iteration`, plus scope labels for each project included

**Body template:**

```markdown
Champion: @handle
Period: [start date] – [end date]
Goal: [one sentence]

## [project-name-1]
- [ ] 🏃 Task in progress jcfischer/specflow-bundle#7
- [ ] Task not started (#issue)
- [ ] 💪 Stretch goal (#issue)
- [ ] ✋ Blocked — [reason] (#issue)
- [ ] ⬛ Multi-iteration (#issue)

## [project-name-2]
- [ ] Task (#issue)

## References
- [Link to relevant PROJECT.yaml, specs, branches]
```

**Emoji status indicators:**

| Emoji | Meaning |
|-------|---------|
| 🏃 | In progress — actively being worked on |
| 💪 | Stretch goal — do if time permits |
| ✋ | Blocked — waiting on external dependency |
| ⬛ | Multi-iteration — won't finish this cycle |
| *(none)* | Planned — not yet started |

**Rules:**
- Each line references an issue (the plan is the summary, issues are the depth)
- Cross-repo references use full format: `org/repo#number`
- Sections group by project, not by type of work
- Multi-contributor plans include sub-sections per contributor

### 3. WORK

Execute the plan using the standard issue-first workflow from CLAUDE.md.

- [ ] Comment on each issue before starting work ("picking this up as part of iteration #N")
- [ ] Work on your fork/branch
- [ ] Commit with `partial #N` or `closes #N` references

### 4. UPDATE

Keep the iteration plan current as work progresses.

- [ ] Check boxes as tasks complete (`- [x]`)
- [ ] Add 🏃 when starting a task
- [ ] Add ✋ with reason when blocked
- [ ] Add new tasks discovered during the iteration
- [ ] Comment on the issue with significant updates or scope changes

**Frequency:** Update after each significant milestone (PR merged, phase completed, blocker resolved). Not after every commit.

### 5. CLOSE

When the time box expires or all tasks are done.

- [ ] Check all completed boxes
- [ ] Note any incomplete items — will they carry to next iteration or be dropped?
- [ ] Close the issue with a summary comment:
  ```
  ## Iteration Summary
  Completed: X/Y tasks
  Carried forward: [list items moving to next iteration]
  Dropped: [items no longer relevant]
  Key outcomes: [1-2 sentences]
  ```

### 6. JOURNAL

After closing, add a journal entry to the most relevant project.

- [ ] Add entry to `projects/*/JOURNAL.md` following the schema in CONTRIBUTING.md
- [ ] Reference the iteration issue in the `**Issues:**` field
- [ ] Capture what emerged — insights from working across multiple projects

## Multi-Contributor Plans

When a champion creates a plan for multiple contributors:

- **Champion responsibilities:** Create the plan, assign sections, update status, synthesize at close
- **Contributor responsibilities:** Update their own checkboxes, comment on blockers, signal completion
- **Coordination:** Champion comments on the issue when priorities shift or scope changes
- **Independence:** Each contributor works on their own fork — the plan coordinates, it doesn't mandate

## Examples

### Solo iteration plan (cross-project)

```markdown
# @mellanon — Iteration 2: Feb 3–14, 2026

Champion: @mellanon
Period: Feb 3 – Feb 14, 2026
Goal: Get headless pipeline merged upstream and start lifecycle playbooks

## specflow-lifecycle
- [x] 🏃 Get PRs #3, #4, #6, #7 reviewed and merged (jcfischer/specflow-bundle)
- [ ] Draft OpenSpec template (#8)
- [ ] 💪 Start Contrib Prep Maestro playbook (#5)

## signal
- [ ] 🏃 Contrib Prep pass — file inventory, sanitization (#1)
- [ ] ✋ First community review — blocked on contrib prep (#2)

## governance
- [ ] Review security PRs #56, #57 (#67)
- [ ] 💪 Respond to Steffen's introduction (#68)
```

### Multi-contributor iteration plan

```markdown
# specflow-lifecycle — Iteration 1: Feb 3–14, 2026

Champion: @mellanon
Period: Feb 3 – Feb 14, 2026
Goal: Merge headless pipeline and begin lifecycle extension commands

## @mellanon
- [ ] 🏃 Headless pipeline PRs merged upstream
- [ ] Draft OpenSpec template (#8)
- [ ] 💪 Prototype specflow review command

## @jcfischer
- [ ] Review PRs #3, #4, #6, #7 on specflow-bundle
- [ ] 💪 Start specflow review command design

## @Steffen025
- [ ] 💪 Cedars integration proposal (#72)
```

## References

- [VS Code Iteration Plans](https://github.com/microsoft/vscode/wiki/Iteration-Plans) — The model this SOP follows
- [VS Code January 2026 Plan](https://github.com/microsoft/vscode/issues/286040) — Example of the format in production
- [CLAUDE.md](../CLAUDE.md) — Issue-first workflow (the default for simple contributions)
- [CONTRIBUTING.md](../CONTRIBUTING.md) — JOURNAL.md schema for the JOURNAL step
- [sops/specflow-development-pipeline.md](specflow-development-pipeline.md) — SpecFlow phases that iteration plans may coordinate
