# Modular Copilot Agents

This directory contains specialized instruction profiles that extend the global base in `copilot-instructions.md`. Repositories selectively enable agents relevant to their stack.

## Available Agents

| Category | File | Purpose |
|----------|------|---------|
| Security (Defensive) | `security/defensive-security.md` | OWASP, secrets, auth, secure coding |
| Frontend (React) | `frontend/react-frontend.md` | React + TS patterns, performance, a11y |
| Accessibility | `accessibility/accessibility-wcag.md` | WCAG 2.1 AA enforcement |
| Performance | `performance/performance-guardian.md` | Budgets, Web Vitals, bundle analysis |
| DevOps (placeholder) | `devops/` | Future IaC, Kubernetes, CI/CD guidance |

## How to Activate an Agent (In a Repository)

Add a lightweight project-specific `./.github/copilot-instructions.md` that references active agents:

```markdown
# Project Copilot Instructions

Base: Inherit global standards from organization `.github` repository.

Active Agents:
- React Frontend: `frontend/react-frontend.md`
- Accessibility: `accessibility/accessibility-wcag.md`
- Performance: `performance/performance-guardian.md`
- Defensive Security: `security/defensive-security.md`

Project Overrides:
1. Test coverage minimum: 70% (UI heavy)
2. Performance budget: +15KB allowed during migration phase
3. Disable Python/Go rules (frontend-only)
```

## Recommended File Strategy


| File Type | Global Base | Project Override Recommended? |
|-----------|-------------|-------------------------------|
| Base Standards | Yes | Optional (only overrides) |
| React Agent | Yes | Often (custom patterns) |
| Accessibility Agent | Yes | Rarely |
| Performance Agent | Yes | Sometimes (budgets) |
| Security Agent | Yes | Sometimes (auth model) |

## Adding a New Agent

1. Create folder: `agents/<category>`
2. Add clear purpose section
3. Define activation triggers
4. Provide checklist + auto comment template
5. Reference official docs (keep evergreen)
6. Keep file <250 lines for readability

## Philosophy

- Small, focused instruction surfaces improve Copilot relevance
- Agents should be composable and non-overlapping
- Avoid duplicating standards—extend the base, don’t rewrite it
- Prefer explicit activation (comment triggers) + auto triggers by path/keywords

## Future Roadmap

- DevOps Agent: Terraform, Kubernetes patterns, observability
- Backend Agent: API versioning, caching layers, database optimization
- Red Team Agent: Offensive security (kept separate from defensive)

## Maintenance

- Review quarterly
- Deprecate agents if unused
- Validate checklists against evolving best practices

---

Last Updated: 2025-11-12
Maintainer: Engineering Standards Group
