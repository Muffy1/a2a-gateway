# A2A Collaboration

This directory is the control plane for **Agent-to-Agent (A2A)** collaboration
across Muffy1's hybrid Android ⇄ workstation ⇄ cloud agent stack.

## What A2A means here
Agents (Operit, Jenny, Kortix, Notte, OpenTerminal, sub-agents, CI runners)
discover each other, advertise capabilities, and hand off work — instead of
every agent talking directly to every other (N×N), they register with this
gateway and talk through **agent cards + a discovery registry**.

## Files
| File | Purpose |
|---|---|
| `agent-card.example.json` | Schema for how an agent describes itself (name, skills, endpoints, auth, capabilities). Copy + fill per agent. |
| `registry.yaml` | The discovery registry: every agent, its endpoint, health URL, and role. |
| `README.md` | This file. |

## Registering an agent
1. Copy `agent-card.example.json` → `agents/<agent-name>.json` and fill it in.
2. Add the agent to `registry.yaml` (name, endpoint, health URL, role).
3. The scheduled `agent-health` workflow pings every health URL and opens an
   issue if an agent is unreachable.

## Agent roles in the stack
- **Operit** (Android) — orchestrator / primary assistant.
- **Jenny** (Termux) — on-device shell + task executor.
- **Kortix** — workflow/connector wrapper.
- **Notte** — browser automation.
- **OpenTerminal** — remote command execution.

## Invocation model
Prefer **least autonomy**: agents ask before consequential, credential-related,
or irreversible actions. Use scoped tokens, never share master keys.