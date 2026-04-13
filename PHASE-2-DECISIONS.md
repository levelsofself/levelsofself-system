# PHASE-2-DECISIONS.md
# Generated: 2026-04-11
# Status: ACTIVE - Awaiting Arthur's decisions
# Context: System audit Phase 1 complete. Authority Contract written. 3 gaps fixed.

---

## RESOLVED (no further action needed)

### R1. Agent identity authority
**Decision:** SOUL.md owns identity. Governance YAML owns Claude Code permissions. These are orthogonal, not competing.
**Resolved by:** AUTHORITY-CONTRACT.md (2026-04-11)

### R2. Lou identity split
**Decision:** Identity files copied to dept-lou (canonical). dept-uncle-lou preserved as backup.
**Resolved by:** Direct fix (2026-04-11). MCP alt-path workaround still functional but no longer sole path.

### R3. George and Hovo missing governance
**Decision:** Explicit policies created (george.yaml, hovo.yaml). Verified via ns_stub policy resolution.
**Resolved by:** Direct fix (2026-04-11). Both resolve to named policies, not global fallback.

### R4. Governance enforcement scope
**Decision:** ns_stub.py + hooks enforce on Claude Code agents only. Telegram bots are outside this layer.
**Resolved by:** Documented in AUTHORITY-CONTRACT.md. This is intentional, not a gap.

---

## DECISIONS NEEDED (Arthur)

### D1. VPS / GitHub authority model [DECIDED 2026-04-11]

**The problem:** VPS is current runtime and design truth. GitHub repos are stale mirrors. CLAUDE.md on VPS has 15 members, repo version has 12. No sync mechanism.

**Options:**
- A) VPS-first: VPS stays authoritative. Push reconciled state to GitHub periodically.
- B) GitHub-first: repos become canonical source. VPS redeployed from them.
- C) Hybrid: VPS authoritative for runtime state/config, GitHub authoritative for code/design. Explicit sync discipline.


**DECISION (Arthur, 2026-04-11):** Hybrid model adopted.
- Phase A (immediate): VPS is temporary source of truth. Reconcile and push MCP servers + core docs to GitHub.
- Phase B (after sync): GitHub becomes canonical for design + code. VPS becomes runtime + state only.
- Hard rule after Phase B: No design truth is edited directly on VPS.
- Cutover condition: GitHub becomes canonical only after all MCP servers match deployed versions, authority contract is committed, tool map is consolidated, and external-facing repos reflect runtime behavior.

**Original recommendation:** C (hybrid) with immediate VPS-to-GitHub reconciliation. VPS is clearly freshest. Pretending GitHub is canonical would be false. But leaving design truth stranded on VPS preserves the problem.

**Affected files:** CLAUDE.md, all MCP server files, family-workers/, dept-*/SOUL.md

### D2. Repo hierarchy [DECIDED 2026-04-11]

**The problem:** palyan-family-system contains mirrors of VPS content (dept-*/SOUL files, family-workers, bot code). Individual repos (mcp-nervous-system, mcp-ops-server, mcp-server) also exist with their own commit history.

**Options:**
- A) palyan-family-system = canonical monorepo. Individual repos become read-only mirrors.
- B) Individual repos = canonical. palyan-family-system archived or demoted to deployment snapshot.
- C) Both maintained with explicit scope boundaries.

**Context:** palyan-family-system is referenced by palyan-watchdog, github-sync, git-push, git-sync scripts. Individual repos have their own histories and are what's published externally.

**External visibility matters here:**
- mcp-nervous-system: npm v1.11.0 published, Anthropic MCP Directory submission (in review), GitHub Actions Marketplace listed, MCP Marketplace auto-imported
- mcp-ops-server: Anthropic MCP Directory submission (in review), GitHub public
- mcp-server: GitHub public (game server)
- palyan-agent-skills: GitHub public


**DECISION (Arthur, 2026-04-11):** Do NOT promote palyan-family-system.
- Verify no active PM2/cron/runtime dependency, then archive
- Canonical repos are modular: mcp-nervous-system, mcp-ops-server, mcp-server, human-systems-foundation
- Consider creating a new system-definition repo for architecture, authority contract, capability matrix, tool map

**Original recommendation:** B. Individual repos are the public-facing canon (npm, Anthropic, marketplace). palyan-family-system becomes a deployment/sync tool, not a source of truth.

### D3. MCP server divergence [HIGH]

**The problem:** PM2 runs files from /root/ (e.g., /root/mcp-nervous-system.js). GitHub repos live at /root/github-repos/. No confirmed sync between these paths. Agent 4 found git commands were blocked by hooks during audit, so diff was not possible.

**Action needed:**
1. Diff VPS runtime files vs GitHub repo versions for all 3 MCP servers
2. If diverged: VPS is truth, push to repos
3. Establish sync discipline going forward

**Critical because:** npm v1.11.0 is published. Anthropic is reviewing. If the published version diverges from what's running, that's a credibility risk.

### D4. Tool map consolidation [MEDIUM]

**The problem:** 6 documents all describe tools:
1. TOOL-REFERENCE.md
2. TOOL-DECISION-TREE.md
3. MASTER-TOOL-INVENTORY.md
4. TOOL-MAP.md
5. COMPLETE-TOOL-MAP.md
6. MCP-TOOLS-REFERENCE.md

**Action:** Pick one canonical doc. Merge any unique content from others. Archive the rest.

**Note:** Pick the doc that best matches the layer model (VPS tools / Claude Code tools / MCP tools / external integrations), not just by recency or filename.

### D5. Roman's fate [MEDIUM]

**The problem:** dept-roman has SOUL + governance + manifest, but no PM2 bot process. tamara-dispatcher still reads dept-roman/drafts/. Roman is used as a Claude Code agent name.

**Options:**
- A) Keep dept-roman as Claude Code agent workspace. No bot needed.
- B) Revive Roman as a Telegram bot.
- C) Archive dept-roman, reassign Claude Code agent name.

### D6. Ops MCP auth [MEDIUM]

**The problem:** mcp-ops-server on port 3472 has a known auth issue. Submitted to Anthropic for review. Still broken.

**Action:** Fix auth before or shortly after Anthropic review response. Broken auth on a submitted product is a credibility risk.

---

## MECHANICAL CLEANUP (no decision needed, execute after above)

### C1. Delete SOUL-thick.md everywhere
14 files. All identical to SOUL.md. Loaded by nothing. Safe delete after D1 is decided (so GitHub sync includes the deletion).

### C2. Review SOUL-thin.md
7 files not referenced by code (delete). 5 files referenced by Ollama fallback paths (review: is Ollama fallback still needed after Apr 8 Claude-direct routing?).

### C3. Fix discovery-scanner cron path
Cron points to /root/discovery-scanner.js but file is at /root/family-workers/discovery-scanner.js.

### C4. Remove orphaned Caddy routes
- /agent-viewer/* has no backend
- /bridge/* is deprecated (blocked since Apr 3)

### C5. Skills cleanup
- 43+ unused bulk-installed skills (28 c-level advisor, 15 senior engineering)
- 6 Palyan-custom skills in /root/skills/ not installed in .claude/skills/
- 3 frontend skills overlap (frontend-design vs ui-ux-pro-max vs senior-frontend)

### C6. Credentials backup cleanup
/root/family-data/business-builder/api-credentials.json.bak.1773421459 flagged as UNCERTAIN by Agent 1. Review for secrets, then delete.

### C7. Archive dept-uncle-lou
After D1 sync is complete and dept-lou is confirmed canonical in GitHub, archive dept-uncle-lou.

---

## SILENT AUTHORITY DECLARATIONS (add to Authority Contract)

These 17 files influence system behavior without being declared canonical. Each needs an explicit domain ownership statement:

| File | Proposed authority domain |
|------|-------------------------|
| /root/CLAUDE.md | Agent startup contract (Claude Code session entry) |
| /root/UNTOUCHABLE_FILES.txt | Protection scope definition |
| /root/nervous-system.config.json | NS runtime configuration |
| /root/tamara-v6.js | Ops runtime (UNTOUCHABLE) |
| /root/preflight.sh | Execution gate (pre-edit safety) |
| /root/family-workers/tamara-dispatcher.js | Dispatch routing authority |
| /root/family-workers/llm-agent-runner.js | Agent execution runtime |
| /root/family-data/LLM_STARTUP.md | LLM session rules and startup sequence |
| /root/family-data/BUSINESS_BUILDER.md | Business strategy reference |
| /root/family-data/COMMS_GUARDRAILS.md | Communication rules |
| /root/family-data/FAMILY_GUARDRAILS.md | Family system rules |
| /root/family-data/family-roles.json | Member registry (source of truth for who exists) |
| /root/family-data/system-config.json | System-wide configuration |
| /root/family-data/UNTOUCHABLE_FILES.txt | Protection list (copy) |
| /root/family-data/VOICE_STANDARD.json | Voice/tone standard |
| /root/family-data/project-files/ALL-SOULS.md | Compiled SOUL reference |
| /root/family-data/arthur-reply-style.md | Arthur communication style |

---

## EXTERNAL-FACING ASSETS (do not break)

These are publicly visible and/or under external review. Any changes must preserve or improve them:

| Asset | Status | Location |
|-------|--------|----------|
| npm mcp-nervous-system v1.11.0 | Published | npmjs.com |
| GitHub mcp-nervous-system | Public, MIT | github.com/levelsofself/mcp-nervous-system |
| GitHub mcp-ops-server | Public, MIT | github.com/levelsofself/mcp-ops-server |
| GitHub mcp-server | Public, MIT | github.com/levelsofself/mcp-server |
| GitHub palyan-agent-skills | Public | github.com/levelsofself/palyan-agent-skills |
| GitHub human-systems-foundation | Public | github.com/levelsofself/human-systems-foundation |
| GitHub Actions: nervous-system-check | Marketplace listed | GitHub Actions Marketplace |
| MCP Marketplace | Listed (auto-imported) | mcp-marketplace.io |
| Anthropic MCP Directory: NS | Submitted, in review | Anthropic |
| Anthropic MCP Directory: Ops | Submitted, in review | Anthropic |
| Anthropic CPN application | 1/10 certs, awaiting 9 more | claude.com/partners |
| Wix blog | 21 posts | levelsofself.com/blog |
| Dev.to | 14 articles | dev.to |
| api.100levelup.com/family/ | 14 tiles live | VPS |
| Moltbook | humansystems agent, 1 post live | moltbook.com |
| HSF 501c3 | Form 1023-EZ submitted | Pay.gov 77346719473 |

---

## PRIORITY ORDER

1. D1 (VPS/GitHub) + D3 (MCP divergence) -- these are coupled
2. D2 (repo hierarchy) -- follows from D1
3. D6 (ops MCP auth) -- credibility risk with Anthropic submission
4. D4 (tool map) -- documentation quality
5. D5 (Roman) -- low urgency
6. C1-C7 -- mechanical, after decisions are locked
