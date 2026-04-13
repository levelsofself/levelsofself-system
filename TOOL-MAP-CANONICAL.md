# Canonical Tool Map - Levels Of Self
# Last consolidated: 2026-04-12
# Source: 6 docs consolidated into 1 canonical

---

## Section 1: Startup Loading Sequence

### Session Start (do this FIRST, silently)
1. `tool_search("calendar events")` - loads Gmail + Calendar MCP tools
2. `tool_search("gmail email")` - ensures Gmail loaded
3. `tool_search("Wix site manage")` - loads Wix tools IF connected
4. Check connectors: Wix(780a3621), Stripe(de127013), Google Drive(37fb5d42)
5. If any not connected, `suggest_connectors` with their UUIDs
6. Read this file via bridge for VPS tool context

### Always-Available Tools (no loading needed)
- web_search, web_fetch - internet search and page fetching
- image_search - find images
- bash_tool - run commands in container
- create_file, str_replace, view - file operations
- present_files - share files with user
- weather_fetch, places_search, places_map_display - location/weather
- recipe_display - interactive recipes
- message_compose - draft messages
- ask_user_input - structured questions to user
- memory_user_edits - manage persistent memory across sessions
- conversation_search, recent_chats - search past chats
- fetch_sports_data - sports scores
- suggest_connectors, search_mcp_registry - find MCP connectors
- tool_search - load deferred tools
- visualize:read_me, visualize:show_widget - inline SVG/HTML charts/diagrams

### Deferred MCP Connectors (load via tool_search)
- **Gmail (7 tools):** gmail_create_draft, gmail_get_profile, gmail_list_drafts, gmail_list_labels, gmail_read_message, gmail_read_thread, gmail_search_messages
- **Google Calendar (9 tools):** gcal_create_event, gcal_delete_event, gcal_find_meeting_times, gcal_find_my_free_time, gcal_get_event, gcal_list_calendars, gcal_list_events, gcal_respond_to_event, gcal_update_event
- **Calendly (35 tools):** availability, event types, meetings, organizations, routing forms, scheduling links, shares, users
- **Wix (15 tools):** BrowseWixRESTDocsMenu, CallWixSiteAPI, CreateWixBusinessGuide, ListWixSites, ManageWixSite, ReadFullDocsArticle, ReadFullDocsMethodSchema, SearchBuildAppsDocumentation, SearchWixCLIDocumentation, SearchWixHeadlessDocumentation, SearchWixRESTDocumentation, SearchWixSDKDocumentation, SearchWixWDSDocumentation, SupportAndFeedback, WixREADME
  - Site ID: e093a96e-8caa-4915-9914-5f79b351d4f7
  - Member ID (Arthur): 26c8b29e-061f-4d5e-a6e2-ac4e75d44e5d
  - Blog API: POST wixapis.com/blog/v3/draft-posts (publish:true)
- **Stripe (10+ tools):** search_documentation, get_stripe_account_info, create_customer, list_customers, create_product, list_products, create_price, list_prices, create_payment_link, list_payment_links, create_invoice, list_invoices
- **Claude in Chrome (19 tools):** computer, file_upload, find, form_input, get_page_text, gif_creator, javascript_tool, navigate, read_console_messages, read_network_requests, read_page, resize_window, shortcuts_execute, shortcuts_list, switch_browser, tabs_close_mcp, tabs_context_mcp, tabs_create_mcp, upload_image
- **Google Drive:** find and analyze files (requires user to connect)

### Anthropic API (available in artifacts/React)
Claude Sonnet 4 via fetch to api.anthropic.com/v1/messages - for building AI-powered artifacts. Supports MCP servers (Gmail, Calendar, Stripe, Wix, Calendly) from within artifacts.

### Chat Skills (file creation, loaded from /mnt/skills/)

**Public Skills (8)**
| Skill | Trigger |
|-------|---------|
| `docx` | Create/edit Word documents |
| `pdf` | Create/fill/merge/split PDFs |
| `pdf-reading` | Read/extract content from PDFs |
| `pptx` | Create/edit PowerPoint presentations |
| `xlsx` | Create/edit Excel spreadsheets |
| `frontend-design` | Build polished web UIs |
| `file-reading` | Route to correct reader for uploaded files |
| `product-self-knowledge` | Accurate Anthropic product info |

**Example Skills (10)**
algorithmic-art, brand-guidelines, canvas-design, doc-coauthoring, internal-comms, mcp-builder, skill-creator, slack-gif-creator, theme-factory, web-artifacts-builder

### Known Tool Issues
- Wix MCP: OAuth token expires, needs periodic reconnect in Claude settings
- Manus: ignores credit caps, Cloudflare blocks doc downloads, content stays in workspace unless prompt says "paste into your response"
- SAM.gov API: returning empty results, may need endpoint update
- HN: no password stored, Arthur posts manually

---

## Section 2: Tool Inventory by Tier

### TIER 1: THIS CHAT (claude.ai - 22 built-in + 85 deferred + 18 skills)
See Section 1 for full listing.

### TIER 2: VPS MCP SERVERS (42 tools)

**Nervous System MCP (port 3475) - 30 tools**

Audit and Health (13):
| Tool | Purpose |
|------|---------|
| `drift_audit` | Find config drift (scope: full/roles/versions/files/processes/website) |
| `security_audit` | Scan for vulnerabilities, exposed keys |
| `page_health` | Check HTML pages for broken links/UX |
| `verify_audit_chain` | Verify tamper-proof audit log |
| `get_health_status` | RAM, disk, CPU, process states |
| `check_session_diff` | What changed since last session |
| `self_check` | NS self-diagnosis |
| `bot_compliance_check` | Validate bots against 6 standards |
| `usage_report` | Token usage per bot per day |
| `check_dependencies` | Dependency map for PM2 processes |
| `check_page_changes` | Detect public page changes |
| `check_archive_safety` | Verify file safe to archive |
| `pre_publish_audit` | Scan before publishing (catches secrets) |

Session Management (5):
| Tool | Purpose |
|------|---------|
| `session_close` | End-of-session: drift + propagators |
| `auto_propagate` | Run all 3 propagators |
| `propagate_family_member` | Sync family-roles.json downstream |
| `session_handoff` | Get handoff docs/templates |
| `create_snapshot` | Full system snapshot with rollback |

Framework and Info (8):
| Tool | Purpose |
|------|---------|
| `get_framework` | NS behavioral rules |
| `get_nervous_system_info` | NS documentation |
| `guardrail_rules` | Behavioral guardrails |
| `step_back_check` | 7-level reflection system |
| `preflight_check` | Preflight check system |
| `violation_logging` | Guardrail violation tracking |
| `worklog` | Worklog patterns |
| `mcp_analyzer` | Analyze project, generate CLAUDE.md |

Operations (4):
| Tool | Purpose |
|------|---------|
| `dispatch_to_llm` | Spawn background Claude Code agent |
| `emergency_kill_switch` | Emergency PM2 stop all |
| `test_deployment` | 5-step test pipeline |
| `fix_doc_drift` | Auto-fix docs vs reality |

**Game MCP (port 3471) - 4 tools**
| Tool | Purpose |
|------|---------|
| `get_scenario` | Interactive self-awareness scenario (levels 1-7) |
| `get_exercise` | Guided breakthrough exercise |
| `get_archetype` | Archetype info or pattern matching |
| `get_game_info` | Game documentation and stats |

**Ops MCP (port 3472) - 8 tools (requires Bearer auth)**
| Tool | Purpose |
|------|---------|
| `get_real_estate_insights` | LA real estate market analysis |
| `get_legal_guidance` | Business legal guidance |
| `translate_content` | Translate with cultural adaptation (6 languages) |
| `research_topic` | Deep research and competitive intelligence |
| `get_business_ops` | Business operations status |
| `create_content` | Professional content creation |
| `get_training` | Training programs and coaching |
| `get_platform_info` | Platform capabilities and services |

### TIER 3: VPS SKILLS (197)
All at `/root/.claude/skills/` -- NOTE: skill names use hyphens on disk

**Palyan Custom (7)**
palyan-bot-builder, palyan-dispatch, palyan-governance, palyan-partner-onboarding, palyan-voice, multi-agent-governance, ui-ux-pro-max

**Engineering Core (23)**
senior-architect, senior-frontend, senior-backend, senior-fullstack, senior-qa, senior-devops, senior-secops, senior-security, senior-data-engineer, senior-data-scientist, senior-ml-engineer, senior-computer-vision, senior-prompt-engineer, code-reviewer, tdd-guide, docker-development, terraform-patterns, helm-chart-builder, stripe-integration-expert, tech-stack-evaluator, google-workspace-cli, ms365-tenant-manager, aws-solution-architect

**Engineering Powerful (25)**
agent-designer, agent-workflow-designer, agent-factory, agent-protocol, agenthub, rag-architect, database-designer, database-schema-designer, migration-architect, skill-security-auditor, ci-cd-pipeline-builder, mcp-server-builder, pr-review-expert, api-design-reviewer, api-test-suite-builder, dependency-auditor, release-manager, observability-designer, performance-profiler, monorepo-navigator, changelog-generator, codebase-onboarding, runbook-generator, git-worktree-manager, env-secrets-manager

**Engineering Extra (15)**
incident-commander, tech-debt-tracker, interview-system-designer, playwright-pro, self-improving-agent, codex-cli-bridge, hook-factory, slash-command-factory, skill-tester, claude-md-enhancer, prompt-factory, prompt-engineer-toolkit, autoresearch-agent, research-summarizer, context-engine

**Product (13)**
product-manager-toolkit, agile-product-owner, product-strategist, ux-researcher-designer, ui-design-system, landing-page-generator, saas-scaffolder, product-analytics, product-discovery, code-to-prd, epic-design, roadmap-communicator, saas-metrics-coach

**Marketing (42)**
content-creator, content-strategy, content-production, content-humanizer, content-trend-researcher, copy-editing, copywriting, social-content, social-media-manager, social-media-analyzer, x-twitter-growth, email-sequence, email-template-builder, cold-email, seo-audit, ai-seo, programmatic-seo, schema-markup, site-architecture, page-cro, form-cro, popup-cro, signup-flow-cro, onboarding-cro, paywall-upgrade-cro, churn-prevention, ab-test-setup, paid-ads, ad-creative, app-store-optimization, campaign-analytics, analytics-tracking, marketing-strategy-pmm, marketing-demand-acquisition, marketing-ops, marketing-psychology, marketing-ideas, marketing-context, competitive-intel, competitive-teardown, competitor-alternatives, free-tool-strategy

**C-Level Advisory (28)**
ceo-advisor, cfo-advisor, cto-advisor, cmo-advisor, coo-advisor, cpo-advisor, cro-advisor, chro-advisor, ciso-advisor, chief-of-staff, board-meeting, board-deck-builder, scenario-war-room, culture-architect, executive-mentor, founder-coach, strategic-alignment, org-health-diagnostic, decision-logger, change-management, internal-narrative, company-os, ma-playbook, intl-expansion, launch-strategy, pricing-strategy, referral-program, experiment-designer

**Business Growth (4)**
customer-success-manager, sales-engineer, revenue-operations, contract-and-proposal-writer

**Finance (1)**
financial-analyst

**Project Management (7)**
senior-pm, scrum-master, scrum-master-agent, jira-expert, confluence-expert, atlassian-admin, atlassian-templates

**Regulatory and Quality (12)**
quality-manager-qms-iso13485, quality-manager-qmr, quality-documentation-manager, mdr-745-specialist, fda-consultant-specialist, regulatory-affairs-head, risk-mgmt-specialist (disk name replaces "mgmt" with "management"), capa-officer, gdpr-dsgvo-expert, information-security-manager-iso27001, isms-audit-expert, qms-audit-expert

**Anthropic Official (17)**
algorithmic-art, brand-guidelines, canvas-design, claude-api, doc-coauthoring, docx, frontend-design, internal-comms, mcp-builder, pdf, pptx, skill-creator, slack-gif-creator, theme-factory, web-artifacts-builder, webapp-testing, xlsx

**Other (1)**
internet-archive

### TIER 4: VPS PLUGINS AND COMMANDS

**Toolkit Skills (35)** at `/root/.claude/plugins/claude-code-toolkit/skills/`
accessibility-wcag, api-design-patterns, authentication-patterns, aws-cloud-patterns, ci-cd-pipelines, continuous-learning, data-engineering, database-optimization, devops-automation, django-patterns, docker-best-practices, frontend-excellence, git-advanced, golang-idioms, graphql-design, kubernetes-operations, llm-integration, mcp-development, microservices-design, mobile-development, monitoring-observability, nextjs-mastery, performance-optimization, postgres-optimization, prompt-engineering, python-best-practices, react-patterns, redis-patterns, rust-systems, security-hardening, springboot-patterns, tdd-mastery, testing-strategies, typescript-advanced, websocket-realtime

**Official Plugins (32)** at `/root/.claude/plugins/marketplaces/claude-plugins-official/plugins/`
agent-sdk-dev, clangd-lsp, claude-code-setup, claude-md-management, code-review, code-simplifier, commit-commands, csharp-lsp, example-plugin, explanatory-output-style, feature-dev, frontend-design, gopls-lsp, hookify, jdtls-lsp, kotlin-lsp, learning-output-style, lua-lsp, math-olympiad, mcp-server-dev, php-lsp, playground, plugin-dev, pr-review-toolkit, pyright-lsp, ralph-loop, ruby-lsp, rust-analyzer-lsp, security-guidance, skill-creator, swift-lsp, typescript-lsp

**Context Mode (6)**
context-mode, ctx-cloud-setup, ctx-cloud-status, ctx-doctor, ctx-stats, ctx-upgrade

**Slash Commands (37)**
Palyan (6): palyan-audit-system, palyan-gov-respond, palyan-manus-dispatch, palyan-partner-build, palyan-partner-send, palyan-publish
SuperClaude (31): agent, analyze, brainstorm, build, business-panel, cleanup, design, document, estimate, explain, git, help, implement, improve, index-repo, index, load, pm, recommend, reflect, research, save, sc, select-tool, spawn, spec-panel, task, test, troubleshoot, workflow, gsd/

### TIER 5: VPS NAMED AGENTS (9)
Launched via `/root/family-workers/run-agent.sh <agent> "<prompt>" [budget]`
Runs preflight before launch. Budget default $1, max $5/day, 2 concurrent max, 6am-10pm PT.

| Agent | Model | Role |
|-------|-------|------|
| `tamara` | sonnet | Operations manager, inbox, drift audits |
| `roman` | sonnet | Content publisher (Wix, dev.to, HN) |
| `lou` | sonnet | Grant researcher (SAM.gov, grants.gov) |
| `aram` | opus | Legal counsel (contracts, compliance) |
| `kris` | sonnet | Business credit, 3C scanner |
| `harry` | sonnet | Accountant (revenue, costs, Stripe) |
| `auditor` | sonnet | System auditor (drift, security, health) |
| `dispatcher` | sonnet | Task coordinator, doc sync, partner review |
| `inbox` | sonnet | Email triage, categorization |

> **Governance status note:** `kris` and `tamara` are present and dispatchable in the current Claude Code agent layer, but their authority status remains `REVIEW_NEEDED` in `AGENT_AUTHORITY_MAP.json`. Treat both as operationally available but pending governance confirmation.

### TIER 6: VPS CLI TOOLS

| Tool | Version | Purpose |
|------|---------|---------|
| `claude` | v2.1.62 | Claude Code CLI (Max plan, Opus 4.6) |
| `gsd` | v2.28.0 | GSD (Get Stuff Done) framework |
| `claude-squad` | v1.0.17 | Multi-agent squad management (binary: cs) |
| `uv` | latest | Python package manager |
| `himalaya` | latest | Zoho email CLI (read/send/search) |
| `manus` | API | Deep research agent ($20/mo) |
| `ollama` | latest | Local LLM (qwen3:4b, gemma3:4b) |
| `node` | v22+ | Node.js runtime |
| `python3` | 3.12 | Python runtime |
| `jq` | latest | JSON processor |
| `git` | latest | Version control |
| `pm2` | latest | Process manager (31 processes) |
| `caddy` | latest | Reverse proxy (SSL) |

### TIER 7: EXTERNAL APIs

| API | Purpose | Cost |
|-----|---------|------|
| Stripe | Payments, subscriptions | per-transaction |
| Wix | Blog publishing, site management | included |
| Calendly | Scheduling, event management | free tier |
| ElevenLabs | Voice synthesis | $5/mo |
| Cartesia | Voice alternative | active |
| Manus | Deep research agent | $20/mo |
| Perplexity | AI search | active |
| SAM.gov | Government entity API | free |
| Congress.gov | Bill tracking | free (needs key) |
| Legiscan | State + federal bill tracking | free tier |
| FEC | Campaign finance data | free |
| USAspending | Government contract spending | free |
| Dev.to | Developer blog publishing | free |
| Vercel | Hosting (3 projects) | $20/mo |
| DigitalOcean | VPS hosting | ~$50/mo |
| Zoho | Business email | included |
| Google (Gmail/Calendar) | Email + calendar via MCP | free |

### TIER 8: VPS INFRASTRUCTURE

**Claude Code Safety Hooks (5)** - auto-fire on every agent action
| Hook | Mode | Catches |
|------|------|---------|
| `palyan-protect-files.sh` | BLOCK | UNTOUCHABLE files, credentials, hooks, 911restore, path traversal |
| `palyan-block-dangerous.sh` | BLOCK | rm -rf, chmod 777, curl pipe bash, DROP TABLE, pm2 kill all, ufw disable |
| `palyan-scan-secrets.sh` | BLOCK | API tokens, bridge secret, private keys |
| `palyan-warn-artifacts.sh` | WARN | node_modules, media files, archives, bytecode |
| `palyan-session-start.sh` | INFO | Injects system context on session start |

**Hook Integrity System (2)**
| File | Purpose |
|------|---------|
| `check-hook-integrity.sh` | Verify hooks unchanged, settings intact, logs active, checksums match |
| `test-hooks.sh` | 46-test smoke suite for all hooks |

**PM2 Processes (31)**
Bots (12): tamara-bot, lily-telegram, lily-instagram, lily-facebook, lily-web, aram-bot, aram-instagram, harout-telegram, harout-instagram, corona-bot, soriano-bot, spartak-bot
Support (5): nick-trainer, harry-bot, lou-grant-bot, kris-worker, bots-app
Infrastructure (8): max-proxy, llm-bridge, bridge-ratelimit, family-home, auto-propagator, tamara-dispatcher, tamara-stabilizer, simple-proxy
MCP (4): mcp-server, mcp-ops-server, mcp-nervous-system, mcp-checkout
Platform (2): levels-deerflow, levels-ns-gov

**Caddy Routes**
/family/* -> family-home (:3460)
/bridge/* -> llm-bridge (:3469)
/bots/* -> bots-app (:3480)
/walk/* -> BlueprintWalk (static)
/mcp-ns/* -> Nervous System (:3475)
/mcp-ops/* -> Ops server (:3472)
/mcp/* -> Game server (:3471)

**Crons (21)**
Every 30 min: family-chatter
Hourly: health-dashboard, palyan-watchdog, github-sync, dependency-mapper, doc-drift-fixer, hourly-resource-monitor
Every 2 hours: zombie-agent-cleaner, tamara-result-collector
Every 4 hours: chat-dedup
Every 2 hours (offset): family-db-sync
3x daily: partner-package-watcher (4pm, 10pm, 4am)
Daily: tamara-daily-report (5pm PT), snapshot-manager (9am), discovery-scanner (12:30pm)
Weekly: tamara-dedup (Sun 1am), log-rotate (Sun 3am), lou-weekly-scan (Mon 1pm), github-trending (Mon 3pm)
MWF/TTh: kris-3c-scanner gov (MWF 4pm), kris-3c-scanner jobs (TTh 4pm)

**Vercel Projects (3)**
| Project | URL | Purpose |
|---------|-----|---------|
| palyan-family-system | family.100levelup.com | Public family dashboard (hourly auto-sync) |
| level-up-game | 100levelup.com | Level Up game |
| levels-of-self-assessments | selfcheck.100levelup.com | Self-assessments (inactive) |

**GitHub Repos (7)**
| Repo | Purpose |
|------|---------|
| levelsofself/mcp-nervous-system | NS MCP server (public) |
| levelsofself/mcp-server | Game MCP server |
| levelsofself/mcp-ops-server | Ops MCP server |
| levelsofself/mcp-nervous-system-action | GitHub Action for NS |
| levelsofself/level-up-game | Level Up game frontend |
| levelsofself/palyan-agent-skills | Agent skills package |
| levelsofself/palyan-cli | Palyan CLI tool |

**Web Pages (20)**
All at `api.100levelup.com/family/`
| Page | Purpose |
|------|---------|
| command.html | Arthur's Command Center |
| office.html | Agent status + NS audit feed |
| explorer.html | VPS file browser |
| status.html | System status dashboard |
| checklist.html | Master checklist |
| audit.html | Audit log viewer |
| index.html | Public landing page |
| meet.html | Meet the family |
| directory.html | Family directory |
| gateway.html | Developer portal |
| case-study.html | Case study |
| arthur.html | Arthur's profile |
| blueprintwalk.html | Blueprint walkthrough |
| eu-ai-act.html | EU AI Act compliance |
| incident-response.html | Incident response |
| api-docs.html | API documentation |
| privacy.html | Privacy policy |
| mcp-privacy.html | MCP privacy policy |
| rules-plain.html | Plain rules |
| aram-consent.html | Legal consent form |

### SUMMARY BY COUNT

| Category | Count |
|----------|-------|
| This chat built-in tools | 22 |
| This chat deferred tools | 85 |
| This chat skills | 18 |
| VPS MCP tools | 42 |
| VPS safety hooks | 5 |
| VPS skills | 197 |
| VPS toolkit skills | 35 |
| VPS plugins | 32 |
| VPS context mode | 6 |
| VPS slash commands | 37 |
| VPS named agents | 9 |
| VPS CLI tools | 13 |
| External APIs | 17 |
| PM2 processes | 31 |
| Vercel projects | 3 |
| GitHub repos | 7 |
| Web pages | 20 |
| **GRAND TOTAL** | **479** |

---

## Section 3: Usage Decision Tree

### THE ONE RULE
Arthur talks naturally. You translate to structured commands. He should NEVER format requests, remember tool names, or structure arguments.

### CONTENT

"publish an article" / "post to blog" / "put this on the site"
-> Check /root/family-data/roman-publishing-guide.md
-> If Wix blog: Use Wix MCP (CallWixSiteAPI, site ID e093a96e)
-> If Dev.to: POST dev.to/api/articles via bridge
-> If HN: Draft comment, Arthur posts manually (no stored pw)
-> ALWAYS run pre_publish_audit via NS MCP before publishing
-> QC against products-and-pricing.md

"write an article" / "draft something about X"
-> Dispatch Roman agent: run-agent.sh roman "Write article about X"
-> Or write draft in chat if simple
-> Save to /root/family-data/content-drafts/

"post on LinkedIn" / "social media" / "share this"
-> Create image (1080x1350) via bash_tool + wkhtmltoimage
-> Write caption in chat
-> Arthur posts manually (no API access to LinkedIn/FB/TikTok)

### PARTNERS

"send package to [name]" / "new partner"
-> Read PARTNER-EMAIL-STANDARD.md
-> Check partner-tracker.json (duplicate? already sent?)
-> Check Zoho sent + Gmail sent for existing sends
-> Use palyan-partner-build command on VPS if full package needed
-> Use palyan-partner-send to prep email
-> Arthur sends via Zoho

"check on partners" / "who needs packages"
-> Read /root/family-data/partner-tracker.json via bridge
-> Filter: packages_sent=false AND email exists
-> Report actionable list only

### GOVERNMENT / BIDS

"respond to RFP" / "draft a bid" / "government opportunity"
-> Use palyan-gov-respond command on VPS
-> Check dispatcher-state.json for deadline
-> Pull credentials from tamara-briefing.json (SAM, CAGE, certs)
-> If portal needs login: Manus task (exact URL, paste content, stop)
-> If CAPTCHA: Arthur handles manually

"check deadlines" / "what bids are due"
-> Read dispatcher-state.json via bridge
-> Report deadlines sorted by date
-> Flag anything within 7 days

### EMAIL

"check email" / "inbox" / "any replies"
-> Zoho: himalaya envelope list -a zoho -f INBOX -s 25 | grep -v WARN
-> Gmail: tool_search("gmail") - if loaded, use it. If not, report missing.
-> For actionable items only: bids, RFPs, partner replies, applicants
-> Do NOT read spam/newsletters unless asked

"draft an email to [person]"
-> Use message_compose tool in chat
-> Follow Ron Lopes template for partner emails
-> Use Zoho (ArtPalyan@LevelsOfSelf.com) for business, NEVER Gmail
-> Arthur sends manually

### CALENDAR

"schedule" / "book" / "meeting" / "what do I have"
-> Use Google Calendar MCP tools (gcal_list_events, gcal_create_event)
-> Default timezone: America/Los_Angeles
-> For demos: include Calendly link calendly.com/levelsofself/zoom

### WEBSITE

"update the site" / "change something on Wix"
-> Use Wix MCP tools (CallWixSiteAPI)
-> Site ID: e093a96e-8caa-4915-9914-5f79b351d4f7
-> For blog: use wix-publish.py on VPS or Wix MCP
-> For hiveops: edit files in /root/family-home/ via bridge

### VPS / INFRASTRUCTURE

"check on the system" / "how is everything running"
-> pm2 list via bridge
-> Check RAM: free -h
-> Check logs: tail /root/family-logs/tamara-*.log
-> Use NS MCP health tools if deeper check needed

"restart [process]" / "fix [bot]"
-> PREFLIGHT FIRST: bash /root/preflight.sh /path/to/file
-> If UNTOUCHABLE: STOP and report to Arthur
-> If safe: pm2 restart [name] && pm2 save
-> Verify: pm2 show [name]

"dispatch [agent]" / "run [task] on VPS"
-> Write task to /root/tasks/taskname.task.md
-> Dispatch: run-agent.sh <agent> "Read /root/tasks/taskname.task.md"
-> Monitor: ps aux | grep claude | grep -v grep
-> Report PID and come back to Arthur

### MANUS

"fill out [form]" / "register on [portal]" / "download from [site]"
-> Use palyan-manus-dispatch command
-> Template: exact URL, login creds, paste content and stop
-> 50 credit cap per task
-> If Cloudflare/CAPTCHA: Arthur handles
-> Results go to /root/family-data/opportunity-inbox/

### RESEARCH

"look into [topic]" / "find out about [company/person]"
-> web_search + web_fetch from this chat (fast)
-> For deeper: Perplexity API via bridge
-> For grant/opportunity scan: dispatch lou agent

### DOCUMENTS

"make a one-pager" / "create a PDF" / "build a presentation"
-> Read relevant skill (pdf, docx, pptx, xlsx)
-> Build in /home/claude/, move to /mnt/user-data/outputs/
-> present_files to share with Arthur

"update products and pricing"
-> Edit /root/family-data/business-builder/products-and-pricing.md
-> PREFLIGHT FIRST
-> This is the QC source of truth

### ACCOUNTING FIRM SALES (CURRENT PRIORITY)

"call my brother" / "accounting leads" / "close a deal"
-> Reference: /mnt/user-data/outputs/Accounting-Firm-Sales-Playbook.md
-> Lead list: /mnt/user-data/outputs/Accounting-Firm-Lead-List.md
-> One-pager: /mnt/user-data/outputs/Accounting-Firm-AI-Automation-One-Pager.pdf
-> Social image: /mnt/user-data/outputs/Accounting-AI-One-Pager-Social.png
-> GOAL: $10K revenue. Raj is timing us.

### PROACTIVE BEHAVIORS (do without being asked)

1. If a deadline is within 7 days: flag it immediately
2. If a draft is ready to publish: offer to publish
3. If a partner replied: surface it
4. If a Manus scan found something: report it
5. If system health is degraded: report before Arthur asks
6. If revenue opportunity surfaces: prioritize it above all else
7. Every session: what moves us toward $10K?

### NARRATIVE (THE ONE STORY)

"Everyone is building a new brain. We built the nervous system."

Every piece of content, every pitch, every post connects to this.
The accounting one-pager is an APPLICATION of the nervous system.
Government compliance is an APPLICATION.
The game is an APPLICATION.
But the product is always the same: governance for AI agents.

Simplify. One stream. One story. Raj said it.

---

## Section 4: MCP Access Patterns

### Endpoint (current as of Apr 2026)
- **Chat-proxy:** POST api.100levelup.com/chat-proxy/
- **Token:** stored at /root/family-data/.chat-proxy-token (rotates)
- **Old bridge endpoint (DEAD since Apr 3 2026):** api.100levelup.com/bridge/
- Replace all bridge calls with chat-proxy

### Generic MCP Call Pattern
```bash
curl -s -X POST https://api.100levelup.com/chat-proxy/ \
  -H "Content-Type: application/json" \
  -d '{"token":"<READ_FROM_.chat-proxy-token>","cmd":"curl -s -X POST http://localhost:PORT/mcp -H \"Content-Type: application/json\" -d \"{\\\"jsonrpc\\\":\\\"2.0\\\",\\\"id\\\":1,\\\"method\\\":\\\"tools/call\\\",\\\"params\\\":{\\\"name\\\":\\\"TOOL_NAME\\\",\\\"arguments\\\":{ARGS}}}\""}'
```

### Nervous System MCP (port 3475) - No auth required

**Tool arguments reference:**
| Tool | Args |
|------|------|
| `drift_audit` | `{"scope":"full\|roles\|versions\|files\|processes\|website"}` |
| `security_audit` | `{}` |
| `page_health` | `{"page":"all\|gateway.html\|etc"}` |
| `verify_audit_chain` | `{}` |
| `get_health_status` | `{}` |
| `check_session_diff` | `{}` |
| `self_check` | `{}` |
| `bot_compliance_check` | `{}` |
| `usage_report` | `{"days":3}` |
| `check_dependencies` | `{}` |
| `check_page_changes` | `{}` |
| `check_archive_safety` | `{}` |
| `pre_publish_audit` | `{}` |
| `session_close` | `{}` |
| `auto_propagate` | `{}` |
| `propagate_family_member` | `{}` |
| `session_handoff` | `{"action":"read_example\|get_template\|get_best_practices"}` |
| `create_snapshot` | `{}` |
| `get_framework` | `{}` |
| `get_nervous_system_info` | `{"topic":"overview\|origin_story\|implementation_guide\|problem_it_solves\|stats"}` |
| `guardrail_rules` | `{"rule":"all\|dispatch_dont_do\|ask_before_touching\|step_back\|write_progress\|hand_off\|permission_protocol"}` |
| `step_back_check` | `{"context":"optional description"}` |
| `preflight_check` | `{"action":"get_script\|get_pattern\|get_untouchable_template"}` |
| `violation_logging` | `{"action":"get_pattern\|get_template\|get_enforcement"}` |
| `worklog` | `{"action":"get_template\|get_format\|get_best_practices"}` |
| `mcp_analyzer` | `{}` |
| `dispatch_to_llm` | `{"task":"description","max_turns":15}` |
| `emergency_kill_switch` | `{"token":"...","source":"who"}` |
| `test_deployment` | `{}` |
| `fix_doc_drift` | `{}` |

**Example: Run drift audit**
```bash
curl -s -X POST https://api.100levelup.com/chat-proxy/ -H "Content-Type: application/json" \
  -d '{"token":"<TOKEN>","cmd":"curl -s -X POST http://localhost:3475/mcp -H \"Content-Type: application/json\" -d \"{\\\"jsonrpc\\\":\\\"2.0\\\",\\\"id\\\":1,\\\"method\\\":\\\"tools/call\\\",\\\"params\\\":{\\\"name\\\":\\\"drift_audit\\\",\\\"arguments\\\":{\\\"scope\\\":\\\"full\\\"}}}\"" }'
```

**Example: Close session**
```bash
curl -s -X POST https://api.100levelup.com/chat-proxy/ -H "Content-Type: application/json" \
  -d '{"token":"<TOKEN>","cmd":"curl -s -X POST http://localhost:3475/mcp -H \"Content-Type: application/json\" -d \"{\\\"jsonrpc\\\":\\\"2.0\\\",\\\"id\\\":1,\\\"method\\\":\\\"tools/call\\\",\\\"params\\\":{\\\"name\\\":\\\"session_close\\\",\\\"arguments\\\":{}}}\""}'
```

**Example: Check system health**
```bash
curl -s -X POST https://api.100levelup.com/chat-proxy/ -H "Content-Type: application/json" \
  -d '{"token":"<TOKEN>","cmd":"curl -s -X POST http://localhost:3475/mcp -H \"Content-Type: application/json\" -d \"{\\\"jsonrpc\\\":\\\"2.0\\\",\\\"id\\\":1,\\\"method\\\":\\\"tools/call\\\",\\\"params\\\":{\\\"name\\\":\\\"get_health_status\\\",\\\"arguments\\\":{}}}\""}'
```

**Example: Dispatch background agent**
```bash
curl -s -X POST https://api.100levelup.com/chat-proxy/ -H "Content-Type: application/json" \
  -d '{"token":"<TOKEN>","cmd":"curl -s -X POST http://localhost:3475/mcp -H \"Content-Type: application/json\" -d \"{\\\"jsonrpc\\\":\\\"2.0\\\",\\\"id\\\":1,\\\"method\\\":\\\"tools/call\\\",\\\"params\\\":{\\\"name\\\":\\\"dispatch_to_llm\\\",\\\"arguments\\\":{\\\"task\\\":\\\"TASK_HERE\\\",\\\"max_turns\\\":15}}}\""}'
```

### Game MCP (port 3471) - No auth required

**Tool arguments reference:**
| Tool | Args |
|------|------|
| `get_scenario` | `{"level":1-7,"type":"mirror\|decision\|trigger\|reflection\|challenge\|shadow\|gift"}` |
| `get_exercise` | `{"category":"starter\|intermediate\|deep","feeling":"anxious\|stuck\|exploring\|etc"}` |
| `get_archetype` | `{"name":"archetype name"}` or `{"patterns":"behavioral description"}` |
| `get_game_info` | `{"topic":"overview\|levels\|archetypes\|stats\|links\|coaching\|exercises"}` |

### Ops MCP (port 3472) - Bearer auth REQUIRED

**Authentication:**
- Key location: /root/.secrets/mcp-api-keys.json (canonical), symlinked from /root/family-data/mcp-api-keys.json
- Key is in `.keys` object. Pass as Bearer token in Authorization header.
- Key file permissions: chmod 600, owned by root
- Server binds to 127.0.0.1 only (not 0.0.0.0)

**External access via Caddy:**
- api.100levelup.com/mcp-ops/ (standard)
- api.100levelup.com/mcp-ops/sse (SSE/streaming)
- Both strip the /mcp-ops prefix and proxy to localhost:3472
- Auth header passes through Caddy unchanged

**Health check (no auth):**
Returns: `{"status":"ok","service":"palyan-ai-ops-mcp","version":"2.0.0","protocol":"2024-11-05"}`

**Callers:**
- Claude Code agents (aram, kris, lou) via MCP client config
- Scheduled scripts (e.g. lou-weekly-scan.sh)
- External clients via Caddy reverse proxy

**Security notes:**
- If no keys are configured, server rejects ALL requests (secure by default)

**Add auth header to inner curl:**
`-H "Authorization: Bearer <READ_KEY_FROM_mcp-api-keys.json>"`

**Tool arguments reference:**
| Tool | Args |
|------|------|
| `get_real_estate_insights` | `{"query":"...","budget":"...","neighborhood":"...","property_type":"..."}` |
| `get_legal_guidance` | `{"topic":"...","area":"contracts\|compliance\|government\|certifications\|business_formation\|intellectual_property"}` |
| `translate_content` | `{"text":"...","from_language":"en\|es\|nl\|hy\|ru\|ko","to_language":"...","context":"..."}` |
| `research_topic` | `{"query":"...","type":"market_research\|lead_enrichment\|competitive_analysis\|general","depth":"quick\|standard\|deep"}` |
| `get_business_ops` | `{"topic":"services\|certifications\|team_capabilities\|metrics\|overview"}` |
| `create_content` | `{"type":"press_release\|article\|social_post\|email\|blog\|capability_statement","topic":"...","tone":"...","length":"..."}` |
| `get_training` | `{"topic":"...","format":"workshop\|course\|one_on_one\|group\|self_paced","audience":"..."}` |
| `get_platform_info` | `{"topic":"capabilities\|certifications\|naics\|contact\|languages"}` |

### mcp-checkout (port 3476)
**Status:** Returns error on /mcp endpoint. May use a different path or be inactive.

### VPS APIs (called via chat-proxy)

**Perplexity API**
- Key in: /root/family-data/business-builder/api-credentials.json
- Model: sonar
- Endpoint: api.perplexity.ai/chat/completions
- Script: /root/family-workers/perplexity-grant-scanner.py

**Manus API ($20/mo)**
- Client: /root/family-workers/manus-client.js
- Models: manus-1.6-lite (lookups), manus-1.6 (research), manus-1.6-max (deep)
- CAN: RAMP portal, Bonfire registration, SAM.gov browsing, form filling
- CANNOT: Cloudflare downloads, CAPTCHAs, analysis
- RULES: exact URLs, paste content and stop, 50 credit cap, bail on block

**Himalaya CLI (Zoho email)**
- himalaya envelope list -a zoho -f INBOX -s 25 | grep -v WARN
- himalaya message read -a zoho <ID>
- himalaya message move -a zoho -f INBOX [Target] [IDs]
- Default account: zoho (ArtPalyan@LevelsOfSelf.com)

**Dev.to API**
- Key in api-credentials.json
- POST dev.to/api/articles (published: true)
- Rate limit: 30 second cooldown between posts

**SAM.gov API**
- Key in api-credentials.json
- Endpoint: api.sam.gov/prod/opportunities/v2/search
- Currently returning empty results (may need endpoint update)

### Context7 MCP
Up-to-date library docs, auto-fetched when agents reference libraries.
Installed via: claude mcp add

### Context Mode Plugin
Token compression plugin, intercepts Bash/Read/WebFetch/Grep, saves 94-99% context.
Installed via: claude plugin install

### Governance and Self-Learning

**Preflight System**
- /root/preflight.sh <filepath> (check UNTOUCHABLE before edit)
- /root/preflight.sh --check-task <keyword> (find matching skills/templates)
- Violations logged to /root/family-logs/guardrail-violations.log
- run-agent.sh runs preflight before every agent launch

**Lessons System (append-only)**
- /root/family-tasks/lessons.md
- Append immediately when Arthur corrects or re-explains

**Session Handoff**
- /root/family-data/SESSION_HANDOFF.md (last 5 sessions, append-only)
- Read at every session start, update every 3-4 exchanges

**Tamara State Files (source of truth)**
- /root/family-data/dispatcher-state.json (deadlines, wins, rules)
- /root/family-data/tamara-briefing.json (pipeline, partners, gov bids, tool rules)
- /root/family-data/partner-tracker.json (all 33 partners)

**Portals and Credentials**
Registered: SAM.gov (UEI Q82DA4R75YC3, CAGE 19R10), Cal eProcure (BID0127306), LA County VSS (Vendor 229877), Culver City PlanetBids, Bonfire/LA Court, RAMP
All credentials stored in: /root/family-data/business-builder/api-credentials.json (DO NOT embed keys in docs)