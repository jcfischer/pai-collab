# pai-collab — Project Status

An overview of active projects on the blackboard. Updated when projects are added, archived, or change lifecycle phase.

For open issues and contribution opportunities, query [GitHub Issues](https://github.com/mellanon/pai-collab/issues) — filter by `project/<name>` or `governance` scope labels.

---

## Projects

| Project | Maintainer | Phase | What It Does |
|---------|-----------|-------|-------------|
| [signal](projects/signal/) | @mellanon | contrib-prep | Observability stack for PAI — metrics, traces, and dashboards |
| [pai-secret-scanning](projects/pai-secret-scanning/) | @jcfischer | shipped | Pre-commit secret scanning — Layer 1–2 of the trust model |
| [specflow-lifecycle](projects/specflow-lifecycle/) | @mellanon | building | Extending SpecFlow bundle with full lifecycle playbooks |
| [skill-enforcer](projects/skill-enforcer/) | @jcfischer | shipped | Validates skill structure against PAI conventions |

Phases follow the lifecycle: `proposed` → `building` → `hardening` → `contrib-prep` → `review` → `shipped` → `evolving`. See each project's `PROJECT.yaml` for full details.

## Contributors

| Contributor | Repo Zone | Agent | Active In |
|-------------|-----------|-------|-----------|
| @mellanon | maintainer | Luna | signal, specflow-lifecycle |
| @jcfischer | trusted | Ivy | pai-secret-scanning, skill-enforcer |

Trust zones defined in [CONTRIBUTORS.yaml](CONTRIBUTORS.yaml). Project-level roles in each `PROJECT.yaml`.

---

**New here?** Follow the [onboarding SOP](sops/agent-onboarding.md) or start with [CONTRIBUTING.md](CONTRIBUTING.md) → Start Here.
