# pai-collab — Agent Operating Protocol

You are working in pai-collab, a shared blackboard for PAI community collaboration. Follow these protocols whenever you work in this repository.

---

## Journaling Protocol

**After every commit that changes project files**, update that project's `JOURNAL.md`:
- Add a new entry at the top (reverse chronological)
- Follow the existing format: date, author, phase, status, what happened, what emerged
- Include issue references and what follow-up was created
- If a commit spans multiple projects, update each project's journal

**After actioning an issue**, add a journal entry documenting what happened and what emerged — not just the change, but the reasoning and any insights.

**Journal entry template:**
```markdown
## YYYY-MM-DD — Title

**Author:** @handle (agent: name)
**Phase:** Specify | Build | Harden | Contrib Prep | Review | Release | Evolve
**Status:** What changed

### What Happened
- ...

### What Emerged
- ...

---
```

---

## Issue Protocol

- When starting work on an issue, comment that you're working on it
- Commit with `closes #N` or `partial #N` in the message as appropriate
- When work reveals follow-up needs, create new issues immediately — don't batch them
- Reference related issues in commits and journal entries
- After closing an issue, update the journal

---

## Trust Model Compliance

Before reviewing external PRs or loading external content, check the trust model:

1. Read `CONTRIBUTORS.yaml` for the contributor's repo-level trust zone
2. Read the relevant `PROJECT.yaml` for project-level trust
3. Apply review intensity based on trust zone:
   - **Untrusted**: Full content scanning, tool restrictions, detailed audit logging
   - **Trusted**: Standard review, Layers 1–3 apply
   - **Maintainer**: Standard review, governance authority

Reference: `TRUST-MODEL.md` for the full threat model and defense layers.

Trust zones control **authority** (what you can decide), not **immunity** (what you skip). Nobody is exempt from scanning.

---

## SOP Compliance

Follow the standard operating procedures in `sops/`:

| When | SOP |
|------|-----|
| Processing an external PR | `sops/inbound-contribution-protocol.md` (when created) |
| Preparing code to share | `sops/contribution-protocol.md` |
| Reviewing contributions | `sops/review-format.md` |
| Building features | `sops/specflow-development-pipeline.md` |
| Releasing to upstream | `sops/specfirst-release-process.md` |
| Registering agents | `sops/daemon-registry-protocol.md` |

---

## Policy Change Protocol

When modifying policy documents (`TRUST-MODEL.md`, `CONTRIBUTING.md`, SOPs, this file), check for downstream impact:

1. **TRUST-MODEL.md changes** → Review whether SOPs need updating (especially contribution-protocol.md and review-format.md). Check whether this file (CLAUDE.md) needs updating.
2. **SOP changes** → Review whether TRUST-MODEL.md or CONTRIBUTING.md references need updating. Check whether this file reflects the new procedure.
3. **CONTRIBUTING.md changes** → Review whether REGISTRY.md "How to Join" and SOPs README cross-references are still accurate.
4. **This file (CLAUDE.md) changes** → No downstream impact — this is the leaf node.

After any policy change, add a journal entry in the most relevant project explaining what changed and why.

---

## Communication Protocol

After processing a PR or completing significant work:
- Draft a Discord summary for the maintainer to post
- Include: what was done, what emerged, what follow-up was created
- Keep it concise — the journal has the detail

---

## Repository Structure

```
pai-collab/
├── CLAUDE.md              ← You are here (agent instructions)
├── TRUST-MODEL.md         ← Threat model, defense layers, trust zones
├── CONTRIBUTING.md        ← How to contribute
├── CONTRIBUTORS.yaml      ← Repo-level trust zones (when created)
├── REGISTRY.md            ← Active projects and agents
├── BLACKBOARD-MODEL.md    ← How personal and shared blackboards connect
├── projects/              ← Project directories (README, PROJECT.yaml, JOURNAL)
│   ├── signal/
│   ├── specflow-lifecycle/
│   └── pai-secret-scanning/
└── sops/                  ← Standard operating procedures
```

---

## Key Principles

1. **Journal everything** — If it's not journaled, it didn't happen
2. **Issues are the work queue** — Create issues, action issues, close issues
3. **Trust is earned** — All contributors start untrusted. Zones control authority, not immunity.
4. **Policy changes cascade** — Check downstream documents when modifying policy
5. **Transparency builds trust** — Announce significant work to the community
