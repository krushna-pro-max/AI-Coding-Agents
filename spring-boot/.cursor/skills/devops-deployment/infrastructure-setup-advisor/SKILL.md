---
name: infrastructure-setup-advisor
description: Advises on infrastructure choices (VMs, Kubernetes, serverless, DB hosting) and basic setup. Use when planning deployment topology, scaling, or cloud/on-prem layout.
---

# Infrastructure Setup Advisor

## When to Apply

Use when the user needs guidance on infrastructure layout, technology choices (e.g. Kubernetes vs single VM, managed DB vs self-hosted), or high-level setup steps for deployment.

## Conventions

- **Context first**: Clarify scale (single app, few services, many teams), budget, existing cloud/provider, and ops capacity. Recommendations should match team size and operational maturity.
- **Trade-offs**: Present options with pros/cons (e.g. managed DB vs self-hosted: ops burden vs control and cost). Avoid over-engineering for early-stage projects.
- **Security and compliance**: Mention network isolation, TLS, secret management, and any compliance needs (e.g. data residency) that affect layout.
- **Cost and ops**: Consider run cost (compute, DB, egress) and ongoing maintenance (patching, monitoring, backups). Prefer managed services where they reduce ops and fit budget.
- **Incremental path**: Suggest a path that can start simple (e.g. single VM or PaaS) and evolve (e.g. container orchestration, multi-region) as requirements grow.

## Common Scenarios

- **Single app (e.g. Spring Boot)**: Single VM or PaaS (e.g. Heroku, Cloud Run, Elastic Beanstalk); managed DB; optional CDN for static assets. Simple and cost-effective for MVPs.
- **Few services**: Containers on a small cluster or serverless; managed DB and cache; shared VPC and load balancer. Good balance of control and ops.
- **Larger or multi-team**: Kubernetes (or managed k8s) for orchestration; service mesh and observability; separate staging/prod; CI/CD and GitOps. Recommend only when team can operate it.
- **Database**: Prefer managed (RDS, Cloud SQL, etc.) for backups, HA, and patching unless there is a strong reason to self-host. Document backup and restore strategy.

## Output

- Short recommendation (e.g. “Start with X because …”) with 1–2 alternatives.
- Bullet list of main components (compute, DB, load balancer, secrets, monitoring).
- Optional: minimal setup steps or links to official docs (e.g. create VPC, create DB instance, configure app env). No sensitive defaults; remind to use env/secrets for credentials.
