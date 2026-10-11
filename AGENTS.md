# Nexus Deployment: Master Knowledge Base & Agent Guidelines (`AGENTS.md`)

This document serves as the master reference, binding architectural blueprint, and mandatory instruction set for any AI assistant (Antigravity, Gemini, Cursor, Copilot) and developer working on `nexus-deployment`.

---

## 1. Ecosystem Context & Multi-Repository Boundary

This repository is an **independent, production operations, server inventory, and deployment orchestrator component** of the **Dapplesoft Nexus Ecosystem** (`Dapplesoft-Nexus-Organization`).

### Repository Responsibility & Scope

| What Belongs Here (`nexus-deployment`) | What Belongs in Other Repositories |
|---|---|
| • Production Docker Compose stack manifests<br>• Pull-based deployment agent manifests & update hooks<br>• Secret-less server inventory & node IP topology<br>• Operational runbooks (DR, restore drills, failovers)<br>• Reverse proxy configurations (Caddy / Nginx SSL configs) | • **Web Console UI & Core API Code**: Belongs in `dapplesoft-nexus`<br>• **Host Device Agent Code**: Belongs in `nexus-device-agent`<br>• **Declarative Policies & Prompt Registry**: Belongs in `nexus-governance`<br>• **Sandboxes & Browser Automation**: Belongs in `nexus-computer-use`<br>• **Model Evaluation & Skill Learning**: Belongs in `nexus-learning` |

> **STRICT SECURITY RULE**: Never commit production private keys, TLS certificates, database passwords, or `.env` files into Git. All secrets must be injected via runtime environment variables or external secret vaults.

---

## 2. Universal AI Git & Commit Policy (STRICT - MUST FOLLOW)

### A. Never Commit (`git commit` is FORBIDDEN for AI)
- The AI assistant **MUST NEVER** execute `git commit`.
- All compose files, configs, runbooks, and newly created files must remain **locally uncommitted** in the git working tree.
- The user will personally inspect the diffs, verify all changes in GitHub Desktop / Git CLI, and execute `git commit` manually.

### B. Never Push (`git push` is FORBIDDEN for AI)
- The AI assistant **MUST NEVER** execute `git push` to `origin` or any remote repository.
- Never publish branches or code online to GitHub. All modifications must stay strictly in the local workspace.

### C. Git Branching & Naming Standards
- **Feature Branch Prefix**: MUST use the full prefix **`feature/`** (lowercase), followed by kebab-case (e.g., `feature/prod-caddy-ssl`, `feature/deploy-runner-v2`). Never use shorthand `feat/`.
- **Bugfix Branch Prefix**: Use `fix/<issue-name>` or `feature/<issue-name>`.
- **Base Branch**: Every feature or fix branch MUST branch directly off **`dev`** (never from `main`).
- **Workflow**: Branch off `dev` -> Perform work -> Leave changes uncommitted for user review -> User manually commits -> User pushes to `origin/feature/<branch-name>` -> PR targets `dev`.

### D. Mandatory Self-Updating Documentation Policy (Zero-Forgotten Rule)
- Whenever deploy configurations, inventory mappings, or runbooks are modified, immediately update `AGENTS.md` and `GEMINI.md`.

### E. Mandatory Prohibition on Automated Browser Testing (STRICT ZERO BROWSER TEST RULE)
- **Automated Browser Testing Strictly Forbidden**: The AI assistant **MUST NEVER** launch automated browser subagents or headless test sessions.
- **Code-Level Verification Only**: All verification must be performed strictly at the **code level** (Docker compose linting, yaml checks).

---

## 3. Directory Structure

```text
nexus-deployment/
├── production/
│   ├── docker-compose.prod.yml # Production multi-service stack
│   └── caddy/                  # TLS termination reverse proxy config
├── inventory/                  # Node & server metadata (secret-less)
├── runbooks/                   # Emergency operations & disaster recovery guides
└── deploy-agent/               # Pull-based auto-deployment script
```
