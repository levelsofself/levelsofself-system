# AUTHORITY CONTRACT
# Version: 1.0
# Date: 2026-04-11
# Status: CANONICAL
# Location: /root/family-data/AUTHORITY-CONTRACT.md

## Purpose

This document defines the formal separation of authority across the Levels Of Self agent system. Every component, agent, and process must conform to this contract. Violations are system bugs, not judgment calls.

## Authority Layers

### Layer A: Identity (SOUL)

**Source:** `/root/dept-{agent}/SOUL.md`
**Defines:** who the agent is -- personality, goals, decision-making style, communication patterns, domain expertise, persona boundaries
**Loaded by:** Telegram bot processes at runtime
**Does NOT define:** permissions, tool access, cost limits, escalation rules

### Layer B: Governance (YAML + ns_stub.py)

**Source:** `/root/levels-os/governance/policies/agents/{agent}.yaml`
**Enforced by:** `ns_stub.py` on port 3490 via `.claude/hooks/ns-pre-tool.sh`
**Defines:** what the agent is allowed to do -- tool permissions, protected paths, escalation thresholds, runtime limits, cost caps
**Does NOT define:** personality, goals, communication style
**Scope:** Claude Code agents ONLY. Telegram bot processes are outside this enforcement path.
**Fallback:** agents without explicit policies inherit `global.yaml` defaults.

### Layer C: Runtime (PM2)

**Source:** PM2 process list
**Defines:** which agents are actually running, on which platforms, with which entry points
**Does NOT define:** identity or permissions (those come from Layers A and B)

## Precedence Rule

> **Governance constrains execution, never overrides identity.**

An agent can intend anything its SOUL defines. Governance decides whether that intent can execute. If governance blocks an action, the agent's identity is not changed -- only its capability is limited.

## Binding Requirements

Every agent in the system MUST have:

1. **Exactly one canonical name** (the agent_id used everywhere)
2. **Exactly one SOUL file** at `/root/dept-{agent_id}/SOUL.md`
3. **Exactly one governance policy** at `/root/levels-os/governance/policies/agents/{agent_id}.yaml`
4. **Exactly one manifest** at `/root/levels-os/governance/manifests/{agent_id}.manifest.yaml`
5. **Zero or more runtime instances** (PM2 processes)

Exception: Claude Code utility agents (auditor, dispatcher, inbox) operate without SOUL files or explicit policies. They inherit global.yaml defaults. This is intentional -- they are operational tools, not persona agents.

## Naming Standard

No aliases. No variations. The canonical name is the single key used across all layers:

```
agent_id   = aram
dept       = dept-aram
soul       = /root/dept-aram/SOUL.md
policy     = /root/levels-os/governance/policies/agents/aram.yaml
manifest   = /root/levels-os/governance/manifests/aram.manifest.yaml
pm2        = aram-bot (or aram-{platform} for multi-platform)
```

If a naming mismatch exists between any two layers, it is a bug that must be fixed before any other work on that agent.

## Visibility Rule

When governance blocks an action:
- The denial MUST be logged (ns_stub.py already does this)
- The denial reason MUST include the policy rule that triggered it
- Future: denial should be surfaced to the agent response layer so operators can see why behavior appears limited

## Governance Scope Boundary

The governance layer (ns_stub.py + hooks) enforces on Claude Code agents only. Telegram bots are governed by:
- Their SOUL file (identity)
- Their application code (behavioral constraints)
- Their LLM provider settings (model, temperature, etc.)

This is an intentional boundary. The governance layer protects the system from its own development agents. The SOUL layer protects users from inappropriate bot behavior. These are different threat surfaces.

## Authority Map

The canonical mapping of all agents lives at:
`/root/family-data/audit/AGENT_AUTHORITY_MAP.json`

This file must be updated whenever an agent is added, removed, renamed, or has its governance changed.

## Amendments

Changes to this contract require Arthur's explicit approval. This document is append-only for amendments.
