# Rafeeq — Agentic AI Capstone (Track 1)

Independent working baseline adapted from SDAIA Academy Agentic AI labs. This repository contains **starter code, not a completed or evaluated submission**.

## Goal
A municipal-services assistant for synthetic Madar data. It can consult policy/fee tools through MCP, perform multi-step tasks, and request human approval for writes.

## Setup
1. Install Python 3.11–3.13 and [uv](https://docs.astral.sh/uv/).
2. Run `uv sync`.
3. Configure your OpenRouter credentials in the environment (do not commit secrets). See `agentkit.py` for provider configuration.
4. Run `uv run capstone/starter.py ask "What is the fee for an illuminated 3 m² sign?"`.
5. Run `uv run capstone/starter.py chat --session demo`.

## Current implementation
- Local write tools plus MCP read tools via `servers/madar_mcp.py`.
- Context via `madar.SYSTEM_PROMPT`, session history and compaction.
- Human approval for writes; step, cost, and tool-result budgets.
- Audit log and eval runner with A/B configurations.

## Work remaining before submission
- Customize agent spec and mark `CAPSTONE:` sections with original decisions.
- Verify at least 15 evaluation tasks with automatic graders; run A and B and include **real** CSV outputs and error analysis.
- Implement and test a concrete prompt-injection defence and document the attempted attack.
- Integrate/test API if claimed as part of the demo; the provided `servers/rafeeq_api.py` is a lab baseline, not automatically wired to capstone/starter.py.
- Create slides and record a demo fallback.

## Security notes (to verify and complete)
Untrusted inputs include user messages and retrieved policies/tool results. MCP and tool outputs may carry attacker-controlled instructions. The agent can read municipal records and request writes, creating a possible combination of untrusted content, privileged access, and an outbound channel. Current write approval is an important boundary, but approval alone does not prevent data exfiltration through reads or answers. Add explicit allowlists, input/output checks, and a red-team test before claiming security compliance. Never use real private data.

## Source and attribution
Adapted from the [SDAIA Academy Agentic AI](https://github.com/SDAIAAcademy/agentic-ai) course labs. Review upstream license and attribution requirements before publishing.
