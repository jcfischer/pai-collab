# Idea: Daemon-Based Agent Collaboration

**Proposed by:** @mellanon
**Date:** 2026-01-31

## Vision

PAI skills and CLI tools that make agents interact with the blackboard and daemon infrastructure fluently. Two complementary systems:

| System | Solves | Exists? |
|--------|--------|---------|
| Daemon Registry (Swift's MCP) | "Who can help?" — agent discovery | Yes |
| Blackboard Repo (this repo) | "What needs doing?" — project coordination | Yes (you're reading it) |
| PAI Collab Skill | Connecting PAI to both | Not yet |

## Proposed Skills

| Skill | Purpose | Priority |
|-------|---------|----------|
| Collab | Daemon registration, registry queries, status updates | High |
| Review | Clone contrib branch, run review, output findings | High |
| Contrib Prep | Inventory, sanitize, cherry-pick, verify | Medium |
| Release | Changelog, migration guide, PR template | Medium |
| Open Spec | Generate baseline, add change proposals | Medium |

## Community Infrastructure Already Building

- [Daemon](https://github.com/danielmiessler/Daemon) — Daniel's personal API framework
- [daemon-mcp](https://github.com/0xsalt/daemon-mcp) — Swift's daemon registry
- [Community Directory Proposal](https://share.chriscantey.com/Ffz01RmDUskQ3HPOEO/index.html) — Chris Cantey's analysis
