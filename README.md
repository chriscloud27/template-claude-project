# Project

This examples project is about an Azure Migration - Infrastructure as Code and deployment automation for a customer's cloud infrastructure migration to Azure.

## Claude Setup

This project uses Claude Code for AI-assisted development and infrastructure automation. The `.claude/` directory contains configuration, skills, agents, and documentation.

### Directory Structure

```
.
├── CLAUDE.md                    # Essential project instructions (committed)
├── CLAUDE.local.md              # Personal overrides (gitignored)
├── .claude/
│   ├── settings.json            # Permissions, hooks, and MCP configs (committed)
│   ├── settings.local.json      # Personal permission overrides (gitignored)
│   ├── .mcp.json                # Dedicated MCP server definitions (committed)
│   ├── rules/                   # Modular, path-scoped instructions (committed)
│   ├── skills/                  # Reusable, auto-invoked workflows (committed)
│   │   ├── deploy-staging/      # Skill: /deploy-staging command
│   │   │   ├── SKILL.md         # Skill definition with frontmatter
│   │   │   ├── scripts/         # Helper scripts (e.g., deploy.sh)
│   │   │   └── templates/       # Static resources
│   │   └── code-review/         # Skill: /code-review command
│   │       └── SKILL.md         # Skill definition with frontmatter
│   ├── agents/                  # Specialized subagent personas (committed)
│   │   ├── security-auditor.md  # Security review agent
│   │   └── api-tester.md        # API testing agent
│   ├── docs/                    # Detailed reference documents (committed)
│   └── hooks/                   # Event-driven automation scripts (committed)
├── .claudeignore                # Files to exclude from Claude's context
└── ...                          # Source code and infrastructure files
```

### Configuration Files

- **CLAUDE.md**: Committed project instructions, guidelines, and requirements visible to all team members
- **CLAUDE.local.md**: Personal overrides and local-only instructions (gitignored)
- **.claude/settings.json**: Global permissions, hooks, and MCP server configurations
- **.claude/settings.local.json**: Personal permission overrides (gitignored)
- **.claude/.mcp.json**: Dedicated MCP server definitions for Claude integration
- **.claudeignore**: Patterns for files Claude should exclude from context

### Skills

Reusable workflows that can be invoked as slash commands:

- **/deploy-staging**: Automated deployment to staging environment
- **/code-review**: Automated code review workflow

### Agents

Specialized subagent personas for specific tasks:

- **security-auditor.md**: Security review and vulnerability assessment
- **api-tester.md**: API testing and integration validation

### Documentation & Rules

#### `.claude/docs/`

Reference documents Claude reads when relevant or when explicitly referenced in `CLAUDE.md`. Always-loaded is `CLAUDE.md` itself — keep it short and link to docs for detail.

Best for:
- Architecture overview and target state
- Domain glossary / customer-specific terminology
- Project context, stakeholders, background
- Migration scope and workstreams
- Key decisions / ADRs

Example files:
- `architecture.md` — Azure target architecture
- `project-context.md` — Customer background, stakeholders, migration goals
- `glossary.md` — Domain terms and customer-specific vocabulary
- `decisions.md` — Key architectural and technical decisions

#### `.claude/rules/`

Modular instructions scoped to specific file paths. Claude applies them automatically when working in the matched directory — no need to repeat conventions in every prompt.

Best for:
- Terraform / OpenTofu style conventions (`terraform/`)
- Helm chart authoring guidelines (`helm/`)
- CI/CD pipeline standards (`.github/workflows/`)
- Any folder with non-obvious project-specific rules

#### `.claude/hooks/`

Shell scripts triggered automatically by Claude Code lifecycle events (e.g. after a file is saved, before a commit, when a task completes). Hooks run outside the model — they are deterministic automation, not AI behavior.

Best for:
- Auto-formatting on save
- Running `terraform validate` after `.tf` changes
- Posting notifications when Claude finishes a task
- Enforcing pre-commit checks