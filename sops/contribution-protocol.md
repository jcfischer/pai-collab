# SOP: Contribution Preparation

How to extract a contribution from a private PAI trunk for public collaboration.

## Pipeline

```
INVENTORY → SANITIZE → EXTRACT → VERIFY → TEST → STAGE → GATE → PUBLISH
```

## Three Concerns (Cleanly Separated)

| Phase | Question It Answers |
|-------|-------------------|
| Contrib Prep | "Is this safe to share?" |
| Review | "Is this good code?" |
| Release | "Is this ready to merge?" |

## Steps

### 1. Inventory

Create `CONTRIBUTION-REGISTRY.md` listing every file to include and exclude. The inventory is law — only listed files get extracted.

### 2. Sanitize

Scan for PII, secrets, personal paths (`/Users/*/`, API keys, credentials). Automated scan + manual review.

### 3. Extract

- Set up remotes: `upstream` (target repo) and `fork` (your public fork)
- Tag tested code on feature branch: `git tag -a <project>-v<version>`
- Create clean contrib branch from `upstream/main`
- Cherry-pick only inventory files from tag

### 4. Verify

- Diff review: no excluded files present
- No secrets in the diff
- Tests pass on the clean branch

### 5. Publish

Push contrib branch to public fork. Update `PROJECT.yaml` with contrib branch link.

## Reference

[PAI Release Runbook](https://github.com/mellanon/PAI) — battle-tested across Context Skill (50 files), Jira Skill (18 files), pai-knowledge Bundle (63 files).
