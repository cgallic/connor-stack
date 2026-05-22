# connor-stack

A curated portal to the small, opinionated, composable pieces I use every day — and the prompts you paste into your own Codex Gemini or Claude Code session to set them up.

## Live Interactive Portal

The full system map, philosophy, interactive dashboards (such as the AI CMO Simulator and Brain Loop timeline console), and setup guides are available on the live site:

**[cgallic.github.io/connor-stack](https://cgallic.github.io/connor-stack)**

## The Core Concept

Connor's environment is built on three core pillars:
1. Always-On Agents: Three always-on agents (including Beast running on a remote Hermes VPS) coordinate notifications, run background tasks, and monitor system health.
2. Lightweight Harness: These agents run with OpenClaw or Hermes serving strictly as a thin harness/message-transport layer.
3. Code Generation: Codex Gemini acts as the primary codebase pair-programmer, writing, editing, and verifying files.

This repository acts as the central hub. The pieces that perform the actual work (the spokes) are standalone, open-source repositories catalogued in the registry.

## Quick Start (Local Setup)

If you are setting this up inside a terminal session:

1. Clone the repository:
   ```bash
   git clone https://github.com/cgallic/connor-stack.git
   cd connor-stack
   ```

2. Load the orientation prompt:
   Open [00-orientation.md](setup-prompts/00-orientation.md) under the `setup-prompts/` directory. Paste the entire file content into a fresh Codex Gemini or Claude Code session. The agent will evaluate your environment, recommend the appropriate path, and help you configure the files.

## License

MIT. See [LICENSE](LICENSE).

Built by Connor Gallic.
