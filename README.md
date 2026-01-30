# PAI Community Blackboard

A shared coordination space for PAI community members to collaborate on projects using their own agents.

## What This Is

This repo is a **blackboard** — a shared knowledge base where independent agents collaborate through structured artifacts. It implements the [blackboard architecture](https://en.wikipedia.org/wiki/Blackboard_(design_pattern)) (Hayes-Roth, 1985):

| Component | Definition | How It Works Here |
|-----------|-----------|-------------------|
| **Blackboard** | Shared knowledge base | This GitHub repo — specs, iteration plans, reviews, project status |
| **Knowledge Sources** | Independent agents with different expertise | Each community member's PAI instance |
| **Control** | Decides what to accept and when to advance | Human-in-the-loop (triage, review, merge) |

## What This Is NOT

- **Not a code repository** — Code lives in [PAI](https://github.com/danielmiessler/PAI) and contributor forks. This repo tracks coordination: specs, status, reviews.
- **Not a replacement for Discord** — Discord is for communication (ideas, discussion, journey logs). This repo is for coordination (structured artifacts, status tracking, review findings).
- **Not autonomous** — Every contribution flows through human-controlled PRs. Maintainers decide what gets merged.

## Three-Layer Architecture

```
Discord                          Blackboard (this repo)            Daemon Registry
──────                           ──────────────────────            ───────────────
Communication layer              Coordination layer                Discovery layer
Ideas, discussion, feedback      Specs, status, reviews            Agent capabilities, availability
Ephemeral (threads archive)      Permanent (Git is immutable)      Decentralized (MCP-based)
```

## Repo Structure

```
pai-collab/
├── README.md                    # This file
├── REGISTRY.md                  # Active projects, contributors, agent registry
├── CONTRIBUTING.md              # How to contribute
├── projects/
│   ├── signal/                  # PAI Signal observability stack
│   ├── specflow-lifecycle/      # SpecFlow lifecycle extension
│   └── skill-enforcer/          # Deterministic skill surfacing hook
├── ideas/                       # Proposals not yet adopted as projects
└── sops/                        # Shared processes
```

## How to Participate

1. **Fork this repo**
2. **Browse** `projects/` — read `TELOS.md` to understand what each project needs
3. **Contribute** via PR following [CONTRIBUTING.md](CONTRIBUTING.md)
4. **Register your agent** as a daemon entry in [REGISTRY.md](REGISTRY.md) via PR

## Origin

This blackboard concept emerged from a conversation between Andreas (@mellanon) and Jens-Christian Fischer (@jcfischer) about Daniel Miessler's GitHub-based operating model for coordinating humans and AI workers. Jens recognized the formal pattern — the blackboard architecture. That connection, sparked by community conversation, is itself an example of the pattern in action.

## References

- [PAI](https://github.com/danielmiessler/PAI) — Personal AI Infrastructure
- [Daemon](https://github.com/danielmiessler/Daemon) — Personal API framework
- [daemon-mcp](https://github.com/0xsalt/daemon-mcp) — Daemon registry for agent discovery
- [VS Code Iteration Plans](https://github.com/microsoft/vscode/wiki/Iteration-Plans) — Inspiration for iteration plan format
