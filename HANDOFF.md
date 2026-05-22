# `connor-stack` — Agent Handoff

You're a fresh Claude Code session inside `E:\Dev2\connor-stack`. This file gets you fully oriented. Read it top to bottom before touching anything else.

---

## What this repo is

A public, choose-your-own-adventure portal at `cgallic/connor-stack` (not yet pushed to GitHub) that documents **how Connor Gallic uses AI** — through his actual proofs of concept, not as prescriptive playbook.

It's a hub. Working subsystems (brain, news digest, marketing skills, shorts pipeline, etc.) live in their own existing public repos. This repo connects them with a guided experience the visitor explores, then forks pieces of into their own setup.

**Three audiences:**
- **A — Solo marketers / agency owners** copy client folder patterns, content workflows
- **B — Claude Code power users / agent builders** copy the orchestration patterns, brain loop, skills/hooks
- **C — Curious readers** take a tour of how it all fits

**Core design philosophy:** "Their Claude finishes the setup." We ship structured prompts + concept demos. The visitor pastes one into their own Claude and it drives configuration locally. We provide skeleton + inspiration, not a fat installer.

---

## Where the work currently stands

### Done
- Repo skeleton at `E:\Dev2\connor-stack` (git init, MIT LICENSE, .gitignore, one bootstrap commit on `main`)
- Spec doc: `E:\Dev2\CMO_Agent_System\docs\superpowers\specs\2026-05-22-connor-stack-design.md` (authoritative; reflects all decisions including spoke list and out-of-scope items)
- Voice anchor — three markdown files written by a subagent earlier in this conversation:
  - `README.md` (581 words) — three-door GitHub landing
  - `docs/philosophy.md` (1,311 words) — "How Connor Does AI" essay
  - `docs/tour.md` (688 words) — architecture tour with ASCII hub+spokes diagram

**These three files have NOT been reviewed by Connor yet.** Read them first to understand voice, but assume they may need rework once we know the new shape.

### Pivoted (mid-conversation, before any HTML work)
The repo is no longer a markdown docs collection. It's a **choose-your-own-adventure HTML experience** hosted at a URL (probably GitHub Pages, possibly a custom domain).

Why: Connor wants the visitor to feel like they're exploring proofs of concept that "wrap them in a giant hug with AI" — interactive, personal, not prescriptive. Markdown docs read as "Connor is telling you the One True Way." HTML CYO reads as "Connor is showing you what he built; remix it."

The voice anchor markdown still has value:
- `philosophy.md` → likely repurposes as the long-form "Connor's actual thinking" page behind a CYO branch
- `README.md` → reframes to a GitHub-renders fallback that points visitors to the live site
- `tour.md` → likely becomes one of the HTML pages

### Cut from v1
- `ralph-wiggum-marketer` plugin (deprecated, per Connor)
- KaiCalls / Case Engine internals (proprietary)
- Pendant / Jarvis layer (too fresh, too Connor-specific)
- Fat installers / one-command runtime (out of scope — visitor's Claude finishes setup)

---

## The choose-your-own-adventure shape (rough)

```
index.html  [interview video embed + intro]
  "How I built an AI that fits MY life.
   Here are the pieces. Make them fit yours."

  → I want to ship better client work       (Marketer path)
  → I want to build the machine that         (Agent-builder path)
    builds the machine
  → I'm just curious what someone's          (Tour path)
    actually running

Each concept page is its own HTML artifact:
  - Concept name + the "why" Connor built it
  - Working demo / screenshot / interactive piece
  - Actual code or config snippet (copy button)
  - "Make it yours" — fork the spoke, paste this prompt into your Claude
  - Cross-links to siblings (CYO branching, not linear)
```

Each concept page ships with an embedded markdown prompt block ("paste this into your Claude") that drives a personalized version locally. No chat widget on the site; the visitor's own Claude does the personalization.

---

## Spokes — the components this repo points at

### Already-public (link, don't vendor)

| Repo | One-line |
|---|---|
| `cgallic/open-brane` | events.db brain foundation, MCP for agents |
| `cgallic/paperboy` | news/papers Discord digest, daily |
| `cgallic/kai-cmo-harness` | open-source AI CMO for Claude Code (marketing skills) |
| `cgallic/blackbox` | self-improving feedback loop for Claude Code |
| `cgallic/diwan` | preflight tests / decision receipts |
| `cgallic/zehrava-gate` | safe commit layer for AI agents |
| `cgallic/cartoonimator` | deterministic mascot lipsync |
| `cgallic/mcp-browser` | terminal-based MCP installer |
| `cgallic/shorts-pipeline` | daily multi-channel YouTube Shorts pipeline |
| `cgallic/mydeadinternet`, `dead-internet-core`, `mdi-mcp-server`, `mdi-oracle-solana` | MDI ecosystem |
| `cgallic/awesome-meetkai` | curated OpenClaw deployments |
| `cgallic/avp` | Agent Verification Protocol |
| `cgallic/wake-up-skill` | ClawdHub skill |

### To create (only one remaining)

- `cgallic/agent-webhook-gateway` — extracted from `E:\Dev2\CMO_Agent_System\gateway\` (FastAPI service exposing the Python automation scripts as HTTP endpoints)

---

## Authoritative references

Read these when you need source material or to verify decisions:

| Source | What's there |
|---|---|
| `E:\Dev2\CMO_Agent_System\docs\superpowers\specs\2026-05-22-connor-stack-design.md` | The locked spec — purpose, audience, architecture, success criteria |
| `E:\Dev2\CMO_Agent_System\CLAUDE.md` | Frameworks, personas, channels, checklists, knowledge-base structure (source material for "marketer door" concept pages) |
| `C:\Users\cgall\.claude\projects\E--Dev2-CMO-Agent-System\memory\` | Connor's persistent memory — preferences, project state, infra map, voice rules |
| `E:\Dev2\connor-stack\docs\philosophy.md` | The voice-anchor essay written this session (use as voice reference) |
| `https://github.com/cgallic/paperboy` | Voice reference — one-line README hook style |
| `https://github.com/cgallic/open-brane` | Voice reference — punchy, concrete |
| `https://github.com/cgallic/shorts-pipeline` | Voice reference — recently shipped, full layered README |

---

## Connor's voice — non-negotiables

From memory + observed patterns. Do not violate.

- **No emojis** in any repo file
- **No AI-tell phrases**: "in conclusion", "it's worth noting", "leverage", "robust", "seamless", "ecosystem", "fragmentation"
- **No "It's not X. It's Y." constructions** (Connor banned this in his short-form scripts)
- **No rhetorical setup-payoff arcs** or three-beat rhythms — they read as AI
- **No bulleted "Why this matters" sections** that read as marketing copy
- **Punchy one-line pitches** in the open-brane / paperboy style — contrast old-thing / new-thing or pain / fix
- **First person is fine** in essays where it earns trust (philosophy doc)
- **Concrete nouns over abstractions**: `events.db`, `~/.claude/projects/`, `ffmpeg`, `Rhubarb` — name real tools
- **Short sentences, fragments OK**, mix into short paragraphs
- **ASCII diagrams in fenced code blocks**, not Mermaid

---

## Open questions Connor hasn't answered yet

When you have a coherent design proposal, raise these with him before building further:

1. **Hosting** — GitHub Pages on `cgallic.github.io/connor-stack` is the zero-effort default. Or a custom domain (`connorstack.com`, `connor.codes`, something else)?
2. **HTML aesthetic** — pull from the `frontend-design` skill (distinctive, production-grade, anti-generic-AI), or match a specific reference site?
3. **Interview video** — does it get recorded before launch (blocks ship) or after (placeholder for now)?
4. **License on new spokes** — assume MIT to match existing repos unless Connor says otherwise.

---

## Suggested next steps (in order)

1. **Read the voice anchor** — open `README.md`, `docs/philosophy.md`, `docs/tour.md`. Get the voice in your head.
2. **Get Connor's call on the open questions above** — at minimum hosting + aesthetic, since they shape the build.
3. **Sketch the CYO map** — list every HTML page that needs to exist, the branching structure, what each page demonstrates. One markdown table is enough.
4. **Build the entry page (`index.html`)** as a single-page proof of concept first. Get Connor's reaction before generating the rest.
5. **Fan out concept pages in parallel** once entry page is approved — subagent per page, each agent reads this HANDOFF + the spec + the approved entry page as voice/structure anchor.
6. **Extract `agent-webhook-gateway`** into `E:\Dev2\agent-webhook-gateway\` as a side task while content is being built.
7. **Write `setup-prompts/`** — the markdown prompts visitors paste into their own Claude. These are the "wrap them in a giant hug" pieces.
8. **Write `links.md`** last, once every spoke has been confirmed real and reachable.
9. **`gh repo create cgallic/connor-stack --public`** + push when content is solid.

---

## What this repo is NOT

- A turnkey product ("clone, run, done")
- A prescriptive "the right way to do AI" playbook
- A monorepo containing all of Connor's code
- A managed service
- A Discord community / paid course / support tier

It is: **a curated portal of proofs of concept that demonstrate how one person uses AI in their life, designed for others to remix.**
