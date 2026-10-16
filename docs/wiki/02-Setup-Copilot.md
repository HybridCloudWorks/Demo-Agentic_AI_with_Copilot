---
title: "02 — Setup: GitHub Copilot"
---

# 02 — Setup: GitHub Copilot

## Prerequisites

- VS Code with **GitHub Copilot + Copilot Chat** extensions, signed in with a plan that includes agent mode / custom agents.
- A test folder.
- Optional for L2/L3 infra tests: `terraform`, `tflint`, `tfsec`, `checkov`, `actionlint` on PATH. For diagram tests, the **draw.io desktop app** (its CLI does the PNG/SVG export); without it the drawio-skill falls back to a diagrams.net browser link.

## Install (drag and drop)

1. Clone the repo and copy the `copilot/` bundle contents into your test project. Yes — clone-then-copy is the intended workflow:

**Windows (PowerShell):**
```powershell
git clone https://github.com/HybridCloudWorks/Demo-Agentic_AI_with_Copilot.git
Copy-Item -Recurse -Force Demo-Agentic_AI_with_Copilot\copilot\* your-project\
```

**macOS/Linux:**
```bash
git clone https://github.com/HybridCloudWorks/Demo-Agentic_AI_with_Copilot.git
cp -r Demo-Agentic_AI_with_Copilot/copilot/. your-project/
```

(Or download the ZIP from GitHub → Code → Download ZIP and drag the *contents* of `copilot/` into your project root. Note the trailing `.` / `\*` — you're copying the folder's contents, not the folder itself.)

> **Install location rule:** always install into a **new, blank folder**. Do not reuse a folder that already has files, and do not open the cloned repo itself as your project.

**Verify the nesting before opening VS Code** — this is the #1 install mistake. At the TOP level of your project you must see `.github/`:

```
your-project/          <- open THIS folder in VS Code
└── .github/
```

If you instead see `your-project/copilot/...`, you copied the *folder* instead of its *contents* — the agents and skills will NOT register. Fix by moving everything up one level:

```powershell
Move-Item your-project\copilot\* your-project\ -Force; Remove-Item your-project\copilot
```

2. After copying, your project should look like:

```
your-project/
└── .github/
    ├── copilot-instructions.md    ← orchestrator, auto-loaded
    ├── agents/                    ← 7 custom agents (*.agent.md)
    │   ├── azure-architect.agent.md
    │   ├── aws-architect.agent.md
    │   ├── terraform-engineer.agent.md
    │   ├── github-expert.agent.md
    │   ├── software-engineer.agent.md
    │   ├── architecture-reviewer.agent.md
    │   └── plan-mode-reviewer.agent.md
    └── skills/                    ← 12 skills (one folder per skill, SKILL.md inside; larger skills bundle references, scripts, and assets)
```

3. Reload VS Code (or start a new Copilot session).

## Verify

- Open Copilot Chat → the **Agent** picker (as in the demo screenshots) → all 7 custom agents should be listed alongside the built-ins.
- The Customizations/Agents view should show them sourced from `.github/agents/`.
- `copilot-instructions.md` applies to every chat automatically.

Smoke test:

> "@workspace What custom agents and skills are configured in this repo?"

Expected: names all 7 agents with codenames and the 12 skills.

## How routing works

- `copilot-instructions.md` gives every session the routing table and gate rules.
- Selecting an agent in the picker scopes the chat to that agent; agents also hand off to each other via the `task` tool and the `handoffs:` buttons defined in their frontmatter (e.g., **software-engineer → architecture-reviewer**).
- The `software-engineer` agent declares `agents: ['architecture-reviewer']` so the 2-pass review runs automatically after implementation.

## Notes on platform differences

| Concern | Copilot behavior |
|---|---|
| Agent format | `.github/agents/<name>.agent.md`, YAML frontmatter with `tools`, `agents`, `handoffs`, optional `model` |
| Model pinning | `software-engineer` pins `Claude Sonnet 4.6 (copilot)`; edit or remove if unavailable on your plan |
| Handoff buttons | May appear in VS Code; in Copilot CLI, the `task` tool is the only mechanism — agents are instructed to use it regardless |
| Skills | `.github/skills/<name>/SKILL.md`; if your Copilot version predates Agent Skills, paste the SKILL.md content into the prompt or convert to `.github/instructions/*.instructions.md` |

## Troubleshooting

| Symptom | Fix |
|---|---|
| Agents/skills missing entirely | Nesting is wrong — `.github/` must be at the project top level, not under `your-project/copilot/`. |
| Agents missing from picker | Filenames must end `.agent.md`; frontmatter must parse (watch quoted strings); reload window. |
| Handoff button does nothing | Invoke via chat instead: select the target agent and paste the handoff payload. |
| Model error on software-engineer | Remove the `model:` line to use your default model. |

Next: [03 — Test Prompts L1](03-Test-Prompts-L1.md)
