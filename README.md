# Muffy1 A2A Gateway

Agent-to-Agent (A2A) control plane for Muffy1's hybrid
**Android ⇄ local workstation ⇄ cloud** agent stack.

Agents (Operit, Jenny, Termux-MCP, Kortix, Notte, OpenTerminal) advertise
capabilities via **agent cards** and discover each other through a YAML
**registry**, so they can hand off work instead of talking N×N.

## Layout
- `a2a/agent-card.example.json` — schema for describing an agent.
- `a2a/registry.yaml` — discovery registry (agents + health endpoints).
- `a2a/README.md` — how to register agents and collaborate.
- `AGENTS.md` — operating rules for humans + agents.
- `.github/workflows/agent-health.yml` — scheduled health checks + validation.

## Quick start
1. Copy `a2a/agent-card.example.json` → `a2a/agents/<name>.json`, fill it in.
2. Add the agent to `a2a/registry.yaml`.
3. Wire a self-hosted runner (or public endpoints) for the `agent-health`
   workflow to ping local health URLs.

Local-first, private, self-hosted. Scoped tokens only — never commit secrets.