# PAI Skill Enforcer

**Status: Shipped (v1)** — by Jens-Christian Fischer ([@jcfischer](https://github.com/jcfischer))
**Extended: F-016** — by Andreas Åström ([@mellanon](https://github.com/mellanon)) in Signal

A deterministic skill surfacing hook for PAI that reinforces Claude Code's natural language skill routing with reliable enforcement and user customization injection.

## The Two-Layer Routing Model

PAI skill routing works in two layers:

1. **Claude Code's NLP router** — Claude naturally matches user intent to skills based on `USE WHEN` triggers in skill definitions. This is probabilistic: it usually works, but can miss or suggest rather than invoke.
2. **Skill Enforcer hook** — A `PreToolUse` hook that intercepts Skill tool calls and ensures deterministic behavior. When a skill fires, the enforcer guarantees the right context loads every time.

The enforcer doesn't replace Claude's routing — it reinforces it. Claude still decides *which* skill to invoke; the enforcer ensures that invocation is complete and correct.

## What It Solves

Skills in PAI are self-contained modules, but they have a known reliability problem: each skill is responsible for checking whether the user has customizations (`EXTEND.yaml`) and loading them. In practice, skills often forget. The enforcer moves this responsibility out of individual skills and into a system-level hook that fires on every skill invocation.

## How It Works

The hook runs as a `PreToolUse` event handler on the Skill tool:

1. Detects when the Skill tool is called with a skill name
2. Checks for `USER/SKILLCUSTOMIZATIONS/{SkillName}/EXTEND.yaml`
3. If found, injects loading instructions via `system-reminder` context — making customizations available to the model without modifying the skill itself
4. If not found, passes through silently with no overhead

This is architecturally separate from observability hooks (like `ToolUseInstrumentation`) because it needs to *inject context* (blocking), not just *emit events* (fire-and-forget).

## Origin

Built by Jens during the PAI Signal Requirements Discord thread (Jan 2026). The spec discussion about skill invocation patterns led directly to this hook — an example of community cross-pollination through the blackboard pattern.

The Signal project (F-016) extended Jens' v1 with EXTEND.yaml customization loading, path traversal prevention, distributed tracing integration, and a 35+ test suite.

## Source Code

| What | Where |
|------|-------|
| Upstream (v1) | [jcfischer/pai-skill-enforcer](https://github.com/jcfischer/pai-skill-enforcer) |
| Signal extension (F-016) | `hooks/SkillInvocationEnforcement.hook.ts` on `feature/signal-agent-2` |
| F-016 spec | `.specify/specs/f-016-skill-invocation-enforcement/spec.md` |

## Project Files

| File | Purpose |
|------|---------|
| [PROJECT.yaml](PROJECT.yaml) | Source pointers |
| [JOURNAL.md](JOURNAL.md) | Status log |
