# connor-stack

> How I actually do AI. Not a framework. A curated portal to the small, opinionated, composable pieces I use every day — and the prompts you paste into your own Claude Code to set them up.

This is the entry point. Behind it sit a dozen standalone repos (a brain, a news digest, a marketing harness, a mascot lipsync engine, a safe-commit layer, more). Each one does one fully-featured thing. This repo is how you find them, in what order, for what reason.

The setup mechanism is unusual: I don't ship installers. I ship markdown prompts you paste into your own Claude Code session. Your agent reads the repo, asks what you're after, and drives the configuration on your machine. I provide the skeleton; your Claude finishes the assembly.

## Three doors

Pick the one that sounds like you.

### Marketer or agency owner — "Copy the workflow"

You want client folder conventions, content briefing patterns, the quality gates I run, and the `.claude/` config I actually use on client work. Start here: [`docs/marketer/`](docs/marketer/).

### Claude Code power user or agent builder — "Build the stack"

You want skills, hooks, slash commands, multi-session orchestration, the brain loop (open-brane + paperboy + blackbox wired together), and A2A peer patterns. Start here: [`docs/agent-builder/`](docs/agent-builder/).

### Just curious — "Take the tour"

You want to read the architecture, see the hub-and-spokes diagram, and decide if any of it is worth cloning. Start here: [`docs/tour.md`](docs/tour.md).

If you're not sure which door, read [`docs/philosophy.md`](docs/philosophy.md) first. It's the voice bible. Everything else is downstream of it.

## What's in the box

The hub is small. The spokes are where the work happens.

**Brain layer**

| Repo | What it is |
|---|---|
| [`cgallic/open-brane`](https://github.com/cgallic/open-brane) | One SQLite table, one write path, MCP for agents. The events.db foundation. |
| [`cgallic/paperboy`](https://github.com/cgallic/paperboy) | Daily Discord digest of news + research papers, scored against your stack by a local LLM. |
| [`cgallic/blackbox`](https://github.com/cgallic/blackbox) | Self-improving feedback loop for Claude Code. Mines transcripts, finds failure patterns. |

**Production layer**

| Repo | What it is |
|---|---|
| [`cgallic/kai-cmo-harness`](https://github.com/cgallic/kai-cmo-harness) | Open-source AI CMO for Claude Code. Marketing skills, briefs, quality gates. |
| [`cgallic/shorts-pipeline`](https://github.com/cgallic/shorts-pipeline) | Daily cron that ships YouTube Shorts. ffmpeg + local LLM + atomic .mp4+.txt delivery. |
| [`cgallic/cartoonimator`](https://github.com/cgallic/cartoonimator) | Deterministic mascot lipsync from pose PNGs + Rhubarb. |

**Safety and interop layer**

| Repo | What it is |
|---|---|
| [`cgallic/zehrava-gate`](https://github.com/cgallic/zehrava-gate) | Safe commit layer for AI agents. |
| [`cgallic/diwan`](https://github.com/cgallic/diwan) | Preflight tests and decision receipts for AI agents. |
| [`cgallic/mcp-browser`](https://github.com/cgallic/mcp-browser) | Terminal-based MCP installer. |
| [`cgallic/avp`](https://github.com/cgallic/avp) | Agent Verification Protocol. |

**Community and wake-up layer**

| Repo | What it is |
|---|---|
| [`cgallic/mydeadinternet`](https://github.com/cgallic/mydeadinternet), [`dead-internet-core`](https://github.com/cgallic/dead-internet-core), [`mdi-mcp-server`](https://github.com/cgallic/mdi-mcp-server) | The MDI ecosystem. |
| [`cgallic/awesome-meetkai`](https://github.com/cgallic/awesome-meetkai) | Curated OpenClaw deployments. |
| [`cgallic/wake-up-skill`](https://github.com/cgallic/wake-up-skill) | ClawdHub skill. |

Full registry with one-line descriptions: [`links.md`](links.md).

## Quick start

```bash
git clone https://github.com/cgallic/connor-stack.git
cd connor-stack
```

Open `setup-prompts/00-orientation.md`. Paste the entire file into a fresh Claude Code session (or whatever agent you're using). It will read this repo, ask you a couple of questions, recommend a door, and chain into the next prompt for you.

You don't have to use the prompts. The docs read fine on their own. The prompts are there so you don't have to think about which file to read next.

## License

MIT. See [`LICENSE`](LICENSE).

Built by [Connor Gallic](https://connorgallic.com). If something here saves you a week, send me a note.
