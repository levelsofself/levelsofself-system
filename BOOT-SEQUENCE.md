# BOOT SEQUENCE CONTRACT
# Version: 1.0
# Date: 2026-04-13
# Status: CANONICAL
# Enforcement: MANDATORY -- violations halt session

## Mandatory First Action

On session start:

STOP.

Before any analysis, planning, or task execution:
1. Read levelsofself-system repository (AUTHORITY-CONTRACT.md, AGENT_AUTHORITY_MAP.json)
2. Declare: GOVERNANCE LOADED

No other files may be read before this step completes.

## Mode Declaration

After loading governance, declare session mode:

- GOVERNANCE_VALIDATION -- governance-layer tasks only, ignore ops/revenue/infrastructure
- GOVERNANCE_WRITE -- committing changes to the governance nucleus
- OPERATIONS -- executing against operational state files
- REVENUE -- revenue-moving actions only

Mode is declared once. Mode constrains scope for the entire session.
If Arthur changes mode mid-session, re-declare explicitly.

## File Priority

1. levelsofself-system repo (source of truth for governance)
2. SESSION_HANDOFF.md (execution context only)
3. dispatcher-state.json / tamara-briefing.json (operational state only)

Derived files may NOT override repository governance.
If a derived file contradicts the repo, the repo wins. Flag the contradiction, do not resolve it from the derived file.

## Violation Rule

If any step is performed out of order:

- Stop immediately
- Declare: BOOT SEQUENCE VIOLATED
- Restart sequence from step 1

## Scope

This contract governs Claude (Opus) sessions on claude.ai and Claude Code agent sessions on VPS.
It does not govern Telegram bot runtime behavior (governed by SOUL files and application code per AUTHORITY-CONTRACT.md).
