# GOVERNANCE WRITE CONTRACT
# Version: 1.0
# Date: 2026-04-13
# Status: CANONICAL
# Enforcement: MANDATORY

## Governed Files

Only these files constitute governance. Everything else is operational.

1. AUTHORITY-CONTRACT.md
2. AGENT_AUTHORITY_MAP.json
3. TOOL-MAP-CANONICAL.md
4. SILENT-AUTHORITY-DECLARATIONS.md
5. PHASE-2-DECISIONS.md
6. BOOT-SEQUENCE.md
7. GOVERNANCE-WRITE-CONTRACT.md (this file)

## Write Authority

Authorized writers:
- Arthur Palyan (direct or via explicit instruction)
- Claude Opus (claude.ai session, with Arthur present)
- Claude Code agents (VPS, only when dispatched by Arthur with explicit governance task)

No other actor may commit to this repository.
No implicit edits. No batch updates. No derived-file-triggers-governance-change.

## Preconditions (all required)

Before any commit to a governed file:

1. BOOT-SEQUENCE.md has been executed (governance loaded)
2. Session mode is GOVERNANCE_WRITE
3. The change does not contradict AUTHORITY-CONTRACT.md
4. Internal consistency is maintained across all 7 governed files

If any precondition is unmet, the commit is invalid.

## Commit Validation

Every commit to a governed file must include in the commit message:

- WHAT: the specific change
- WHY: the reason it is needed
- IMPACT: expected behavioral change (or "none" if structural only)

Commits without all three are violations.

## Violation Rule

A governance change is invalid and must be discarded or overwritten if it was made:

- Outside this repository
- Without GOVERNANCE_WRITE mode declared
- Without meeting all preconditions
- Without validated commit message

Operational files on VPS may reference governance but do not define it.
If a VPS file contradicts the repository, the repository wins.

## Amendments

Changes to this contract require Arthur's explicit approval.
This document is append-only for amendments.
