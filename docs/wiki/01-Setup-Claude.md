---
title: "01 — Setup: Claude Code"
---

# 01 — Setup: Claude Code

## Prerequisites

- VS Code with the **Claude Code** extension (or the Claude Code desktop app / CLI), signed in.
- A test folder (empty is fine — e.g. `Test Folder`).
- Optional for L2/L3 infra tests: `terraform`, `tflint`, `tfsec`, `checkov`, `actionlint` on PATH. For diagram tests, the **draw.io desktop app** (its CLI does the PNG/SVG export — `winget install JGraph.Draw` / `brew install --cask drawio`); without it the drawio-skill falls back to a diagrams.net browser link. Prompts still work without these tools; agents will report which validations they could not run.

## Install (drag and drop)

1. Clone the repo and copy the `claude/` bundle contents into your test project. Yes — clone-then-copy is the intended workflow:

**Windows (PowerShell):**
```powershell
git clone https://github.com/HybridCloudWorks/Demo-Agentic_AI_with_Copilot.git
Copy-Item -Recurse -Force Demo-Agentic_AI_with_Copilot\claude\* your-project\
```

**macOS/Linux:**
```bash
git clone https://github.com/HybridCloudWorks/Demo-Agentic_AI_with_Copilot.git
cp -r Demo-Agentic_AI_with_Copilot/claude/. your-project/
```

(Or download the ZIP from GitHub → Code → Download ZIP and drag the *contents* of `claude/` into your project root. Note the trailing `.` / `\*` — you're copying the folder's contents, not the folder itself.)

> **Install location rule:** always install into a **new, blank folder**. Do not reuse a folder that already has files, and do not open the cloned repo itself as your project.

**Verify the nesting before opening VS Code** — this is the #1 install mistake. At the TOP level of your project you must see `CLAUDE.md` and `.claude/`:

```
your-project/          <- open THIS folder in VS Code
├── CLAUDE.md
└── .claude/
```

If you instead see `your-project/claude/...`, you copied the *folder* instead of its *contents* — the agents and skills will NOT register. Fix by moving everything up one level:

```powershell
Move-Item your-project\claude\* your-project\ -Force; Remove-Item your-project\claude
```

2. After copying, your project should look like:

```
your-project/
├── CLAUDE.md                 ← orchestrator, auto-loaded every session
└── .claude/
    ├── agents/               ← 7 agent definitions
    │   ├── azure-architect.md
    │   ├── aws-architect.md
    │   ├── terraform-engineer.md
    │   ├── github-expert.md
    │   ├── software-engineer.md
    │   ├── architecture-reviewer.md
    │   └── plan-mode-reviewer.md
    └── skills/               ← 12 skills (one folder per skill, SKILL.md inside; larger skills bundle references, scripts, and assets)
```

> Windows tip: `.claude` is a dot-folder — make sure hidden files are visible in Explorer, or copy via terminal: `Copy-Item -Recurse claude\* your-project\`.

3. Open the project in VS Code and start a **new** Claude session (agents/skills are read at session start).

## Verify in the Agents center

Open **Customizations** in the Claude panel (the same view as in the demo screenshots):

- **Agents** → should list all 7 agents (Project scope, from `.claude/agents/`).
- **Skills** → count should include the project skills: `adr-authoring`, `azure-cloud-migrate`, `azure-compliance`, `azure-cost`, `azure-deploy`, `azure-verified-modules`, `drawio-skill` (the official diagrams skill), `github-actions-security`, `handoff-contracts`, `report-issue`, `terraform-validation`.
- **Instructions** → `CLAUDE.md` should show as the project instruction file.

Quick smoke test — ask Claude:

> "List the agents and skills available in this project and what each is for."

Expected: it names all 7 agents with codenames (Arc, Outpost, Atlas, Actions, Forge, Compass, Sentinel) and all 12 skills.

## How routing works

- `CLAUDE.md` is loaded into every session and tells the main model how to classify requests and which subagent to dispatch via the Agent/Task tool.
- Agent `description` frontmatter fields say "Use PROACTIVELY…" so Claude delegates without being told.
- Skills auto-trigger by description match (e.g., editing a workflow file triggers `github-actions-security`), or invoke manually: "use the terraform-validation skill".

## Troubleshooting

| Symptom | Fix |
|---|---|
| Agents/skills don't appear at all | Nesting is wrong — check nothing lives under `your-project/claude/` or `your-project/copilot/`; the dot-folder must be at the project top level. |
| Agents don't appear | Confirm files are at `.claude/agents/*.md` with valid YAML frontmatter (`name`, `description`); restart the session. |
| Skills don't appear | Each skill must be a folder containing `SKILL.md` with `name` + `description` frontmatter. |
| Orchestrator ignored | `CLAUDE.md` must be at project root; check the Instructions tab shows it. |
| Agent won't run a tool | Its `tools:` list is intentionally restricted (reviewers are read-only by design). |

Next: [03 — Test Prompts L1](03-Test-Prompts-L1.md)
