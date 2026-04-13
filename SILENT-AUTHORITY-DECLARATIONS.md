# SILENT AUTHORITY DECLARATIONS
# Appendix to AUTHORITY-CONTRACT.md
# Date: 2026-04-11
# Status: DRAFT - awaiting Arthur approval

## Purpose

These files influence system behavior without being explicitly declared as authoritative.
This document assigns each one a domain, a layer, and a canonical status.
Once approved, these declarations are added to the Authority Contract.

---

## Declarations

### Startup Layer (loaded at session init)

**CLAUDE.md** (/root/CLAUDE.md)
- Authority domain: Claude Code session entry point
- Defines: identity rules, guardrails, startup sequence, family member count
- Layer: VPS (moves to GitHub after D1 cutover)
- Canonical: YES - this is the root document for every Claude Code session
- Note: VPS version (15 members) is truth. GitHub version (12 members) is stale.

**LLM_STARTUP.md** (/root/family-data/LLM_STARTUP.md)
- Authority domain: LLM session rules and behavioral constraints
- Defines: rules 1-12 for Claude Code agent behavior, startup protocol
- Layer: VPS (moves to GitHub after D1 cutover)
- Canonical: YES for LLM behavioral rules

**BUSINESS_BUILDER.md** (/root/family-data/business-builder/BUSINESS_BUILDER.md)
- Authority domain: Business strategy reference
- Defines: go-to-market, pipeline, six doors framework
- Layer: VPS
- Canonical: YES for business strategy (but may need freshness review)

### Identity Layer

**family-roles.json** (/root/family-data/family-roles.json)
- Authority domain: Member registry
- Defines: who exists in the system, their IDs, names, roles, PM2 processes
- Layer: VPS (source of truth, referenced by mcp-nervous-system.js)
- Canonical: YES - this is THE member registry
- Note: AGENT_AUTHORITY_MAP.json is the audit-layer view. family-roles.json is the runtime view.

**ALL-SOULS.md** (/root/family-data/project-files/ALL-SOULS.md)
- Authority domain: Compiled SOUL reference
- Defines: all agent personalities in one file (for quick reference)
- Layer: VPS (derived from dept-*/SOUL.md files)
- Canonical: NO - derived artifact. dept-*/SOUL.md files are canonical.

**arthur-reply-style.md** (/root/family-data/arthur-reply-style.md)
- Authority domain: Arthur's communication style
- Defines: how Arthur writes, tone, patterns
- Layer: VPS
- Canonical: YES for Arthur persona replication

**VOICE_STANDARD.json** (/root/family-data/VOICE_STANDARD.json)
- Authority domain: Voice and tone standard
- Defines: voice parameters for agent communication
- Layer: VPS
- Canonical: YES for voice/tone

### Protection Layer

**UNTOUCHABLE_FILES.txt** (/root/UNTOUCHABLE_FILES.txt AND /root/family-data/UNTOUCHABLE_FILES.txt)
- Authority domain: File protection scope
- Defines: which files cannot be edited by agents
- Layer: VPS
- Canonical: YES - two copies exist (root and family-data). Need to confirm which is primary or if both are read.
- Action needed: verify which copy preflight.sh reads, make that one canonical, symlink the other.

**preflight.sh** (/root/preflight.sh)
- Authority domain: Execution gate
- Defines: pre-edit safety checks, UNTOUCHABLE enforcement
- Layer: VPS
- Canonical: YES for execution safety

### Guardrail Layer

**COMMS_GUARDRAILS.md** (/root/family-data/COMMS_GUARDRAILS.md)
- Authority domain: Communication rules
- Defines: what agents can/cannot say in external communications
- Layer: VPS (moves to GitHub after D1 cutover)
- Canonical: YES for communication constraints

**FAMILY_GUARDRAILS.md** (/root/family-data/FAMILY_GUARDRAILS.md)
- Authority domain: Family system operational rules
- Defines: inter-agent behavior rules, escalation patterns
- Layer: VPS (moves to GitHub after D1 cutover)
- Canonical: YES for system-level behavioral constraints

### Runtime Layer

**tamara-v6.js** (/root/tamara-v6.js)
- Authority domain: Ops runtime controller
- Defines: Tamara bot behavior, dispatch logic, team response
- Layer: VPS (UNTOUCHABLE, PM2 managed)
- Canonical: YES for ops runtime
- Note: PROTECTED. Do not edit. Do not inspect internals.

**tamara-dispatcher.js** (/root/family-workers/tamara-dispatcher.js)
- Authority domain: Dispatch routing
- Defines: which tasks go to which agents, scheduling logic
- Layer: VPS
- Canonical: YES for dispatch decisions

**llm-agent-runner.js** (/root/family-workers/llm-agent-runner.js)
- Authority domain: Agent execution runtime
- Defines: how Claude Code agents are launched and managed
- Layer: VPS
- Canonical: YES for agent execution

### Configuration Layer

**nervous-system.config.json** (/root/nervous-system.config.json)
- Authority domain: NS runtime configuration
- Defines: project root, data dirs, log dirs, HTML dirs
- Layer: VPS
- Canonical: YES for NS path configuration

**system-config.json** (/root/family-data/system-config.json)
- Authority domain: System-wide configuration
- Defines: system-level settings
- Layer: VPS
- Canonical: YES for system config (need to verify overlap with nervous-system.config.json)
- Action needed: confirm these two config files don't conflict

---

## Summary

| Status | Count |
|--------|-------|
| Canonical (confirmed) | 14 |
| Derived (not canonical) | 1 (ALL-SOULS.md) |
| Needs action | 2 (UNTOUCHABLE copies, config overlap) |

## Next steps
1. Arthur approves these declarations
2. Add to AUTHORITY-CONTRACT.md as appendix
3. Resolve the two action items (UNTOUCHABLE copy, config overlap)
4. After D1 cutover: move design-layer files to GitHub
