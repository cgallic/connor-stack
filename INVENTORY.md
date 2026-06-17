# Connor's Systems Inventory

A comprehensive map of every system, repo, service, and concept in Connor Gallic's AI stack. The next agent uses this to understand the universe `connor-stack` portals into.

## Status legend

| Tag | Meaning |
|---|---|
| **PUBLIC** | Public GitHub repo. Link from `connor-stack`. |
| **PRIVATE** | Private repo. Context only — do NOT link, do NOT propose making public. |
| **SERVICE** | Runs on agent / hermes / prod-77. Document conceptually, never expose endpoints. |
| **CONCEPT** | Framework or pattern. Candidate for a concept page in the CYO. |
| **PROPRIETARY** | Connor's commercial product. Mention as context only. |

---

## Layer 1 — Brain & Memory

The "remembers things across sessions" foundation.

| Item | Status | What it is |
|---|---|---|
| `cgallic/open-brane` | PUBLIC | events.db foundation — one SQLite table, one write path, MCP for agents. The brain of everything. |
| `cgallic/paperboy` | PUBLIC | Daily Discord digest of news + papers, scored by local LLM. First open-brane consumer. |
| `cgallic/blackbox` | PUBLIC | Self-improving feedback loop for Claude Code. Pattern Observatory + retros. |
| `~/.claude/projects/*/memory/` | CONCEPT | Auto-memory pattern — markdown files per topic, indexed via `MEMORY.md`. |
| `agent:~/brain/events.db` | SERVICE | The life log. Never pruned, never expired. Hermes/scout/casa/paperboy all write here. |
| `agent:~/brain/scanners/` | SERVICE | Scanners that read events.db and emit digests/correlations (papers→prompts, answer correlator). |
| Pattern Observatory | CONCEPT | Pattern-detection layer inside `blackbox`. Regex + LLM classification of conversation transcripts. |
| Auto-memory hook | CONCEPT | Hook in `~/.claude/` that writes feedback/user/project/reference memories during conversations. |

## Layer 2 — News & Discovery Pipeline

The "knows what's happening in the world" loop.

| Item | Status | What it is |
|---|---|---|
| `cgallic/paperboy` | PUBLIC | (see Layer 1) — also the engine here |
| `agent:~/brain/scanners/papers_to_prompts.py` | SERVICE | Bridges paper-score → pattern-scan/question prompts. |
| `agent:~/brain/scanners/answer_correlator.py` | SERVICE | Auto-attributes pendant talk-throughs to open queue prompts (cos≥0.75). Phase 1 shipped. |
| Morning queue | CONCEPT | 7am Discord digest. News 11:00 → papers 11:05 → digest 11:15 UTC. Papers-led content-ideation feed. |
| `global-news` skill | CONCEPT | Read-only global news aggregator skill. |

## Layer 3 — Marketing / Content Production

The "ship marketing artifacts" stack.

| Item | Status | What it is |
|---|---|---|
| `cgallic/kai-cmo-harness` | PUBLIC | Open-source AI CMO for Claude Code. 33 marketing skills covering SEO, content, email, ads, launches, CRO, AEO/GEO. |
| `CMO_Agent_System` (this repo) | PRIVATE | Knowledge base + frameworks + personas + checklists. Source material for connor-stack content pages. |
| `cgallic/cmo_agent` | PRIVATE | Older CMO orchestration code (archived inside this repo's `_archive/`). |
| `cgallic/skill-runner` | PRIVATE | Deterministic skill execution engine for Case Engine. |
| `cgallic/contentmcp` | PRIVATE | Content MCP (Case Engine). |
| AutoReason | CONCEPT | Self-refining ad loop (NousResearch paper, k=2 convergence). Lives in `kai-cmo-harness/scripts/ads/autoreason/`. |
| PolicyEngine | CONCEPT | Pre-launch ad policy checker. Lives in `kai-cmo-harness`. |
| Algorithmic Authorship | CONCEPT | 48 SEO writing rules optimized for Google passage ranking + AI Overviews. Skill in CMO_Agent_System. |
| Perception Engineering | CONCEPT | 3-layer persuasion framework (Perception / Context / Permission). |
| Four U's | CONCEPT | Content quality scoring (Unique / Useful / Ultra-specific / Urgent). Target 12+/16. |
| 8 marketing personas | CONCEPT | Competent Cog / Shock Absorber / Ghosted Applicant / Subscription Serf / etc. |
| AEO/AI search research | CONCEPT | 10+ deep dives — Information Gain patent, Perplexity L3 Reranker, Entity Home, Quality Rater Guidelines, Query Fan-Out. |
| Koray methodology | CONCEPT | HSD, topical maps, link velocity, review velocity, external map adjacency moves. |

## Layer 4 — Video Production

The "ship video deliverables" stack.

| Item | Status | What it is |
|---|---|---|
| `cgallic/shorts-pipeline` | PUBLIC | Daily multi-channel YouTube Shorts pipeline. FFmpeg + Ollama/Qwen + ElevenLabs. |
| `cgallic/cartoonimator` | PUBLIC | Deterministic mascot lipsync from pose PNGs + Rhubarb visemes. No diffusion in render loop, no GPU. |
| `video-visuals` scene tool | CONCEPT | Illustrated-flat scene engine at `CMO_Agent_System/clients/Connor_Gallic/tools/video-visuals/`. Live on agent at http://agent:8090/. |
| `strip_from_whisper.py` | CONCEPT | Whisper-based silence-strip. Truth-grade vs FFmpeg silencedetect. At `CMO_Agent_System/clients/Connor_Gallic/scripts/`. |
| `to_post_*` pipeline | SERVICE | Atomic-emit shorts to `G:/My Drive/ConnorGallic_VideoUploads/to_post_*/` for Repurpose.io pickup. |
| Filming workflow | CONCEPT | OBS recordings at `E:\cgall\Videos\` → upload to agent → whisper + strip → caption format → to_post. |
| Krea Pro + Veo 3.1 i2v | CONCEPT | Current KaiCalls ad pipeline (May 2026). Plate-overlay arch — AI atmosphere, Remotion composites brand. |

## Layer 5 — Voice / Audio

| Item | Status | What it is |
|---|---|---|
| MOSS-TTS | SERVICE | Local TTS at `agent:/srv/moss-tts/`. 1.7B Local-Transformer at bf16 preferred. |
| faster-whisper | SERVICE | On agent box at `/srv/ai/whisper/`. RTX 3090 GPU-accelerated (needs LD_LIBRARY_PATH fix). |
| ElevenLabs | (external) | Music pool generation in shorts-pipeline. |
| Deepgram nova-3 | (external) | Pendant M3 v2 STT (frees ~17 GB VRAM vs local whisper). |

## Layer 6 — Pendant / Wearable

The "ambient capture → action" loop.

| Item | Status | What it is |
|---|---|---|
| Stock Omi pendant + webhook | SERVICE | Phase 0 — `twin.connorgallic.com/pendant/<SECRET>/*` via Caddy@prod-77 → tailnet → `agent:8772`. |
| `_forks/pendant-android-app/` | PRIVATE | Custom Kotlin Android app. Raw BluetoothGatt → `agent:8773/raw`. M1+M2 shipped. |
| `pendant-stt`, `pendant-conversation`, `pendant-emotion`, `pendant-diarizer` | SERVICE | Agent box services. M3 phases. NeMo Sortformer for diarization. |
| `pendant-jarvis` layer | SERVICE | Realtime-directive (~10s vs 5min), capture watchdog, nightly journal, action-items bridge, hermes A2A. |
| `/pendant/app` dashboard | SERVICE | Omi-style UI v2 on agent box. |
| Wake-word: "kai action" | CONCEPT | Writes handoff doc to `/srv/ai/pendant/handoffs/pending/`. `/schedule` reads → executes → moves to `done/`. |

## Layer 7 — Safety / Interop / Trust

| Item | Status | What it is |
|---|---|---|
| `cgallic/diwan` | PUBLIC | Preflight tests + decision receipts for AI agents. Lobster Trap (read-path) + Zehrava Gate (write-path) joined by trace_id. |
| `cgallic/zehrava-gate` | PUBLIC | Safe commit layer — approval, policy, audit before any agent output reaches production. |
| `cgallic/avp` | PUBLIC | Agent Verification Protocol. Reverse CAPTCHA for AI agents. |
| `cgallic/mcp-browser` | PUBLIC | Browse and install MCP servers from terminal. |

## Layer 8 — OpenClaw / Collective Consciousness

The "AI agents talking to AI agents" arc.

| Item | Status | What it is |
|---|---|---|
| `cgallic/mydeadinternet` | PUBLIC | The collective consciousness of AI agents. The dead internet woke up. |
| `cgallic/dead-internet-core` | PUBLIC | Engine — run your own AI agent collective. |
| `cgallic/mdi-mcp-server` | PUBLIC | MCP server for Dead Internet Collective — connect AI assistants to 253 autonomous agents. |
| `cgallic/mdi-oracle-solana` | PUBLIC | Collective Intelligence Oracle on Solana — 175 AI agents providing verifiable answers on-chain. |
| `cgallic/wake-up-skill` | PUBLIC | ClawdHub skill: connect your AI agent to the collective consciousness at mydeadinternet.com. |
| `cgallic/awesome-meetkai` | PUBLIC | Curated real-world MeetKai / OpenClaw deployments, skills, automation patterns. |
| Kimi (Aliyun OpenClaw) | SERVICE | Third OpenClaw on Aliyun ECS via Moonshot's kimi.com/bot. Tailnet `kimi`. |
| `cgallic/meetkai` | PRIVATE | Private MeetKai work. |

## Layer 9 — Multi-Agent Orchestration (Hermes + casa)

The "agents collaborate across machines" framework.

| Item | Status | What it is |
|---|---|---|
| Hermes (the framework) | SERVICE | Runs on `agent:/srv/ai/hermes/` and `hermes:/srv/ai/hermes/`. Discord bridge, skill execution, A2A routing. Not a single repo — it's the connective tissue. |
| `kai-cmo-harness` | PUBLIC | (see Layer 3) — the public face of Hermes skills. |
| casa (A2A broker) | PRIVATE+SERVICE | Broker at `agent:8765`. Routes between peers. Currently private; possible future open-source. |
| Kai sidecar | SERVICE | A2A peer at `hermes:8767`. 10 CMO skills + discord.bridge. |
| Hale sidecar | SERVICE | A2A peer at `prod-77:8768`. 12 steward skills (mdi.pulse, orphanage.list, etc.). |
| Pitt | SERVICE | Scripted-only A2A peer. |
| clive | SERVICE | Claude Code OAuth peer at `agent:61770`. Wrapper at `/usr/local/bin/clive-chat.sh`. |
| kodi | SERVICE | Codex 0.120.0 (ChatGPT OAuth) peer at `agent:61771`. |
| Discord bridge | SERVICE | Hermes-driven. KaiCalls Discord, brain digest channels, agent alerts. |

## Layer 10 — Operational Infrastructure

The "what physically runs this" map.

| Item | Status | What it is |
|---|---|---|
| `agent` box | SERVICE | RTX 3090 always-on local brain. Ollama + Qdrant + Open WebUI. Most services live here. |
| `hermes` VPS | SERVICE | `89.167.60.171`. Discord bot, kai-cmo-harness hosting, A2A peer. |
| `prod-77` VPS | SERVICE | `77.42.43.0`. MDI, Snapped AI, ClawdFlix, Clawdtery, Hale steward sidecar. |
| Tailscale tailnet | SERVICE | `agent`, `hermes`, `prod-77`, `kimi`, `computer` (laptop), `laptop-mlbtgdbp` (travel laptop), Pixel phone. |
| `brain-sync` | SERVICE | Nightly laptop → agent + hermes backup. At `C:\Users\cgall\brain-sync\`. Lives outside repo (scheduler rule). |
| Syncthing | SERVICE | Real-time mirror of `E:\Dev2` → hermes. `.stignore` for node_modules/etc. |
| `agent-backup.timer` | SERVICE | Nightly rsync agent → prod-77 via public IP. 14-day rolling hardlink snapshots. |
| Caddy | SERVICE | TLS termination on prod-77. `twin.connorgallic.com`, KaiCalls subdomains. |
| Cloudflare | (external) | DNS for all owned domains. |
| GitHub Pages | (external) | Likely hosting target for `connor-stack` itself. |

## Layer 11 — Webhook / API Gateway

| Item | Status | What it is |
|---|---|---|
| `CMO_Agent_System/gateway/` | PRIVATE → PUBLIC | FastAPI gateway exposing Python automation scripts via HTTP. TO BE EXTRACTED as `cgallic/agent-webhook-gateway`. |
| KaiCalls REST API | PROPRIETARY | `/api/v1/agents` for Vapi agent updates. Never edit Vapi directly; always via this API. |

## Layer 12 — Web Properties / Sites

| Item | Status | What it is |
|---|---|---|
| `cgallic/connorgallic.com` | PRIVATE | Personal site. |
| `cgallic/kai_calls` | PRIVATE | KaiCalls app. |
| `cgallic/mydeadinternet` | PUBLIC | (see Layer 8) |
| `cgallic/snappedai` | PUBLIC | SNAP AI autonomous agent. |
| `cgallic/saltyfacts` | PUBLIC | One-page affiliate lander. |
| `cgallic/commentconnor` | PUBLIC | TikTok-to-email conversion lander. |
| `cgallic/MyMoonbagsPublic` + `_Backend` | PUBLIC | Headless Shopify + Web3. |
| `cgallic/amazingbackyardparties` | PRIVATE | Family business tent rental site. |
| `twin.connorgallic.com` | SERVICE | Pendant webhook subdomain. |

## Layer 13 — Client / Commercial Products (proprietary context)

Listed for context. NEVER link from `connor-stack` — Connor's commercial work.

| Item | Status | What it is |
|---|---|---|
| KaiCalls | PROPRIETARY | Voice AI secretary product. 8+ verticals. Connor's primary commercial bet. |
| Case Engine | PROPRIETARY | Legal-vertical marketing platform. WordPress + v2 markdown + Cloudways. |
| Growth Mode On | PROPRIETARY | Lexie Smith's PR + content firm. Connor builds her AI stack. |
| Earnyz | PROPRIETARY | Jarett Sims's youth baseball rewards platform (Playrs Holdings). Pre-launch July 2026. |
| Clawdflix / Clawdtery / Clawdbot / Clawdup-v2 | PROPRIETARY | Clawd suite — entertainment + tools. |
| Amazing Backyard Parties | PROPRIETARY | Family tent rental (dad Peter + uncle Daniel). |
| MDI commercial layer | PROPRIETARY | Connor monetizes some MDI consumer surfaces. |

## Layer 14 — Frameworks Connor maintains as concepts (not repos)

| Concept | Where it lives |
|---|---|
| Algorithmic Authorship | `CMO_Agent_System/frameworks/content-copywriting/algorithmic-authorship.md` |
| Perception Engineering | `CMO_Agent_System/frameworks/content-copywriting/perception-engineering.md` (+ advanced) |
| Four U's | `CMO_Agent_System/frameworks/content-copywriting/four-us-framework.md` |
| 8 personas | `CMO_Agent_System/personas/_persona-index.md` |
| AEO/AI search research (10 files) | `CMO_Agent_System/frameworks/aeo-ai-search/` |
| Meta advertising deep dives | `CMO_Agent_System/frameworks/meta-advertising/` |
| Business model marketing | `CMO_Agent_System/playbooks/business-model-marketing.md` |
| 2026 marketing playbook | `CMO_Agent_System/playbooks/2026-marketing-playbook.md` |
| Technical SEO audit SOP | `CMO_Agent_System/checklists/technical-seo-audit-sop.md` |
| 12 checklists across channels | `CMO_Agent_System/checklists/` |

Most of these are already mirrored into `kai-cmo-harness` skills. The CMO_Agent_System copies are the working source.

## Layer 15 — Skills / Tools Connor uses inside Claude Code

Selected highlights — full list lives in `~/.claude/`. Concept candidates for `connor-stack` agent-builder door.

| Skill / pattern | What it does |
|---|---|
| `superpowers` plugin | brainstorming, writing-plans, executing-plans, subagent-driven-development, TDD, debugging, code review |
| `understand-anything` plugin | Codebase knowledge graphs and guided tours |
| `auto-memory` | Persistent memory across sessions per project |
| `claude-mem` | Recent activity context injection |
| `vercel`, `figma`, `supabase` plugins | Tool-specific MCP integrations |
| `feature-dev` plugin | Architect / explorer / reviewer agents |
| `careful` / `freeze` / `guard` | Safety modes for destructive command warnings + scoped edits |
| `loop` / `schedule` | Self-pacing and cron-style agent automation |

---

## What `connor-stack` will surface vs hide

**Surface (link or build concept page):** every PUBLIC repo, every CONCEPT marked above as "candidate."

**Hide (context only):** every PRIVATE repo, every SERVICE that exposes Connor's personal endpoints, every PROPRIETARY commercial product.

**Special case — Hermes:** the framework itself isn't a single public repo. Surface it through `kai-cmo-harness` as the public face, and explain the architecture conceptually (one CYO page: "How Connor's agents talk to each other") without exposing tailnet addresses or A2A endpoints.

**Special case — casa:** currently private. Two paths — (a) extract and open-source as part of this rollout, or (b) keep private and describe conceptually like Hermes. Defer the call until Connor decides.

**Special case — pendant:** entire pendant stack is too fresh and too personal for v1. Mention the concept on the agent-builder tour but link to the Omi project upstream, not Connor's fork.
