# How I do AI

I keep watching smart people build elaborate agent systems that collapse the second they touch real work. A multi-step planner. A vector store. A retrieval-augmented synthesizer. An orchestrator. A "memory layer." Eight microservices behind a custom protocol. By month three they're back to pasting things into ChatGPT.

The bug isn't the LLM. The bug is the architecture they wrapped around it.

This repo is the architecture I actually use. It's not big. It's not impressive at a glance. The pieces are boring on purpose. But it works on a Tuesday, it works on a flight, and it works six months from now when I've forgotten everything about how I built it. That's the bar.

## The thesis

Small, opinionated, composable pieces beat one big agent. Always. Every time.

A "big agent" — by which I mean any single program that tries to plan, retrieve, decide, write, and ship — is a load-bearing wall in a building you're still designing. You can't move it without bringing the roof down. You can't see inside it. You can't reason about why it did the thing it did three weeks ago.

A bunch of small scripts that each do one thing, log what they did, and hand off via plain files? That you can move. That you can read. That you can rebuild in an afternoon if you have to.

The whole repo is downstream of this one bet.

## Principles I actually follow

### 1. Memory belongs in plain text, not in your context window

The single biggest unlearned lesson of the last three years of AI work: **context windows are not memory**. They're a scratchpad. They evaporate when the session ends. They get compacted. They lie to you.

Real memory lives in files you can `grep`. For me that's two things:

- `events.db` — one append-only SQLite table that every adapter writes to and every agent reads from. Calendar, Drive, Stripe, git commits, Claude sessions, pendant transcripts. All one schema. See [`cgallic/open-brane`](https://github.com/cgallic/open-brane).
- `~/.claude/projects/<project>/memory/MEMORY.md` — the auto-memory file Claude Code maintains per project. I let it accumulate, I review it weekly, I move the heavy stuff into topic files when it gets long.

If I delete my context window right now, the brain doesn't lose anything. If I delete the brain, the context window can't recover anything. That asymmetry tells you where the truth lives.

### 2. One repo per fully-featured thing. Don't conglomerate.

I used to keep everything in one monorepo. It felt tidy. It wasn't. When the marketing harness needed to ship, the brain refactor blocked it. When the shorts pipeline broke, I was four directories deep in client work to find it.

Now each fully-featured thing is its own repo. `open-brane` is one repo. `paperboy` is one repo. `shorts-pipeline` is one repo. `kai-cmo-harness` is one repo. They link to each other through `links.md` and through `import` statements that point at GitHub URLs in the docs.

The test for "does this deserve its own repo" is short: **could a stranger clone it, run it, and get value in under an hour, without the rest of my world?** If yes, separate repo. If no, it's a script in something larger.

This repo — connor-stack — exists because the *portal* itself is a fully-featured thing. The portal is the product. The spokes are the implementation.

### 3. Skills, hooks, and slash commands beat monolithic system prompts

Most "AI workflow" advice is "write a better system prompt." I think that's backwards.

A long system prompt is a single load-bearing wall again. Every new behavior fights every other behavior. The first time you have to debug "why did it skip the test step today but not yesterday" you'll wish you'd split it.

Claude Code gives you three real composition primitives: **skills** (markdown files the agent loads on demand), **hooks** (deterministic shell commands the harness runs before or after a tool call), and **slash commands** (named entrypoints that load a specific skill). Use them. A skill for "write a blog post in Connor's voice" is twelve files I can edit individually. A 4,000-word system prompt that tries to do the same thing is one file I'm afraid to touch.

If you've never written one: start with a slash command that wraps a skill that has three rules. Ship that. Add the fourth rule next week.

### 4. The user's Claude finishes the setup. Don't ship fat installers.

I've shipped enough Python installers in my life. Every one of them broke on someone's machine in a way I couldn't reproduce.

The new pattern: I ship structured markdown prompts. You paste one into your Claude Code. **Your** agent reads my repo, asks **you** what you're trying to do, picks the right files, and configures them on **your** machine. If your environment is weird, your Claude figures it out. If you change your mind halfway, your Claude adapts.

This shifts the integration surface from "my code talking to your system" to "your agent talking to your system." That surface is enormous now, and growing. I'm leaning into it.

It also means the docs ARE the install. Anything I have to explain in the README is something the setup prompt has to handle. That tension keeps both honest.

### 5. The brain ingests the world. Agents act on what the brain noticed.

I don't have one agent that watches everything. I have a brain that watches everything, and a small number of agents that act on what the brain noticed.

Concretely: `paperboy` doesn't tell me about a paper because I asked. It tells me because it ingested arXiv overnight, scored the paper against my `research-interests.md`, the score crossed 7/10, and it landed in my morning Discord post.

The agent in the loop doesn't have to be smart. It has to be **fed**. The intelligence is in the ingest and the scoring, not in the agent reading the output. That's why so many agent demos feel impressive in the demo and useless in real life — they're starving.

### 6. Subagents for parallel work, not for everything

There's a temptation, once you have subagents, to use them for everything. Don't.

Subagents are great for parallel work where there's no shared state. Three tutorials, written by three subagents, simultaneously: yes. Three steps of one tutorial, each its own subagent: no — they'll lose track of each other and you'll spend more time stitching than writing.

The rule I use: **if two pieces of work would be fine running on two different days of the week, they're fine as parallel subagents. Otherwise keep them in one session.**

## What this repo is, and isn't

This repo is a curated portal. It links out. It teaches patterns. It hands you setup prompts.

It is not:

- A framework. There's nothing to import.
- A library. There's nothing to install.
- A SaaS. There's nothing to subscribe to.
- A complete system. The complete systems are the spokes.

If you want to copy one piece — fine. If you want to copy the whole stack — also fine, that's what the setup prompts are for. If you want to read the philosophy and never clone a single repo — that might actually be the highest-value path, because then you'll go build your own version of this, opinionated for your own work, and that will serve you better than any of my code ever could.

I built this because I kept losing the thread between sessions, between projects, between machines. The stack you see in `tour.md` is what I built to stop losing it. It's not the right answer for everyone. But it's a working answer for one person, and I think the shape of it generalizes.

The shape is: small parts, plain files, one write path, agents finish the setup, brain feeds the agents, repo per real thing.

Build yours.
