# Project Instructions

Azure Migration project — Infrastructure as Code and deployment automation for a customer's cloud infrastructure migration to Microsoft Azure.

## Key References

- Architecture: `.claude/docs/architecture.md`
- Project context & stakeholders: `.claude/docs/project-context.md`
- Domain glossary: `.claude/docs/glossary.md`
- Architectural decisions: `.claude/docs/decisions.md`

## Conventions

- IaC: Terraform / OpenTofu
- Helm for Kubernetes workloads, kustomize for environment overlays
- CI/CD: GitHub Actions or Azure DevOps
- Confirm `terraform plan` / `tofu plan` before any apply
- Never store secrets in code — use Azure Key Vault references or environment variables
