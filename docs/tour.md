# The tour

## What you're looking at

A hub-and-spoke layout. `connor-stack` (this repo) is the hub: a portal, a philosophy doc, some templates, and a set of setup prompts. Everything that actually *does* work is a separate repo — a spoke — linked from here. The hub teaches the patterns. The spokes ship the patterns.

No spoke depends on this repo. Some spokes depend on each other (paperboy reads from open-brane's schema, for example). Most run standalone.

## The diagram

```
                                  ┌─────────────────────┐
                                  │                     │
                                  │   connor-stack      │
                                  │   (this repo)       │
                                  │                     │
                                  │   docs / templates  │
                                  │   setup-prompts     │
                                  │                     │
                                  └──────────┬──────────┘
                                             │
                  ┌──────────────────────────┼──────────────────────────┐
                  │                          │                          │
                  ▼                          ▼                          ▼
        ┌─────────────────┐        ┌─────────────────┐        ┌─────────────────┐
        │   BRAIN LAYER   │        │ PRODUCTION LAYER│        │  SAFETY LAYER   │
        └─────────────────┘        └─────────────────┘        └─────────────────┘
                  │                          │                          │
       ┌──────────┼──────────┐               │                          │
       │          │          │               │                          │
       ▼          ▼          ▼               ▼                          ▼
   open-brane  paperboy  blackbox      kai-cmo-harness            zehrava-gate
       │          │                    shorts-pipeline            diwan
       │          │                    cartoonimator              mcp-browser
       │          │                                                avp
       │          │
       │          │  paperboy WRITES to open-brane's
       │          │  events.db schema (canonical adapter pattern)
       │          ▼
       │     ┌─────────────┐
       └────►│  events.db  │◄──── more adapters (gdrive, claude, git, ...)
             │  (SQLite,   │
             │   append-   │
             │   only)     │
             └─────────────┘

                                  ┌─────────────────────┐
                                  │  COMMUNITY / WAKE   │
                                  └─────────────────────┘
                                             │
                  ┌──────────────────────────┼──────────────────────────┐
                  │                          │                          │
                  ▼                          ▼                          ▼
            mydeadinternet            awesome-meetkai              wake-up-skill
            dead-internet-core
            mdi-mcp-server
```

The only "real" data flow shown is paperboy → open-brane, because that's the one that genuinely runs in production right now and is worth understanding before you wire anything else. Everything else is each-spoke-on-its-own.

## Spokes by layer

### Brain layer

The persistence and feed system. If you're going to copy one layer, copy this one — every other layer reads better when there's a brain underneath it.

| Repo | One line |
|---|---|
| [`cgallic/open-brane`](https://github.com/cgallic/open-brane) | One SQLite events table, one write path, an MCP server. Every adapter normalizes into it. |
| [`cgallic/paperboy`](https://github.com/cgallic/paperboy) | Daily Discord digest of news + research papers. Local LLM scores each item against your stack. |
| [`cgallic/blackbox`](https://github.com/cgallic/blackbox) | Mines Claude Code transcripts weekly for behavioral failure patterns. Tells you which rules you keep breaking. |

### Production layer

The "do real work" layer. These ship deliverables — blog posts, ad creative, mascot videos, voice content.

| Repo | One line |
|---|---|
| [`cgallic/kai-cmo-harness`](https://github.com/cgallic/kai-cmo-harness) | Open-source AI CMO for Claude Code. Marketing skills, briefs, content briefs, quality gates. |
| [`cgallic/shorts-pipeline`](https://github.com/cgallic/shorts-pipeline) | Daily cron. ffmpeg slices 6-second windows from long takes, local LLM writes overlays, atomic .mp4 + .txt delivery. |
| [`cgallic/cartoonimator`](https://github.com/cgallic/cartoonimator) | Deterministic mascot lipsync. Pose PNGs plus Rhubarb phoneme alignment, no model inference at render time. |

### Safety and interop layer

The boring-but-critical layer. Stops you from shipping garbage, gives you a common protocol for tool installs, and lets agents verify each other.

| Repo | One line |
|---|---|
| [`cgallic/zehrava-gate`](https://github.com/cgallic/zehrava-gate) | Safe commit layer. Blocks dangerous operations from AI agents before they hit git. |
| [`cgallic/diwan`](https://github.com/cgallic/diwan) | Preflight tests and decision receipts. Make agents show their work before they run it. |
| [`cgallic/mcp-browser`](https://github.com/cgallic/mcp-browser) | Terminal-based MCP installer. Browse, install, configure. |
| [`cgallic/avp`](https://github.com/cgallic/avp) | Agent Verification Protocol. |

### Community and wake-up layer

Curated lists, hub deployments, and a couple of opinionated skills. Read these if you're already deep in the rest.

| Repo | One line |
|---|---|
| [`cgallic/mydeadinternet`](https://github.com/cgallic/mydeadinternet) | The MDI hub. |
| [`cgallic/dead-internet-core`](https://github.com/cgallic/dead-internet-core) | The shared core for MDI deployments. |
| [`cgallic/mdi-mcp-server`](https://github.com/cgallic/mdi-mcp-server) | MCP server for MDI integrations. |
| [`cgallic/awesome-meetkai`](https://github.com/cgallic/awesome-meetkai) | Curated list of OpenClaw deployments. |
| [`cgallic/wake-up-skill`](https://github.com/cgallic/wake-up-skill) | ClawdHub skill. |

## Where to go next

If the diagram made sense and you want the reasoning behind the shape — read [`philosophy.md`](philosophy.md). That's where the principles are. The "why" lives there.

If you want to start using something — pick a door from the [main README](../README.md) and follow the setup prompt for that door. The prompts know which spokes are relevant for which audience and will walk you through cloning and configuring them in order.

If you want every spoke described in one line, no diagrams, no narrative — that's [`links.md`](../links.md).
