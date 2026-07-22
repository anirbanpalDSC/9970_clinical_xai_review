# Token Minimization Playbook (Claude Code / Codex)

Source: Slavik Shynkarenko, "3 Simple Techniques to Reduce Token Consumption in Claude Code and Codex," AutoScout24 Tech Blog, June 22, 2026.
https://tech.autoscout24.com/blog/posts/3-techniques-to-reduce-token-consumption-claude-code-codex/

Install/usage details below were cross-checked against each tool's own repo/docs where the article didn't spell them out in full (links noted per section). Verify versions before rollout — CLI flags on fast-moving tools change.

---

## How to use this playbook

Try the three techniques in order. Each is independent, so stop after any one if it already gives you what you need. Budget ~15 min for Technique 1, ~20 min for Technique 2, ~15 min for Technique 3.

- [ ] Technique 1: Trim tool/output noise
- [ ] Technique 2: Give the agent a code map
- [ ] Technique 3: Route tasks to the right model
- [ ] Set up measurement (cache-hit ratio, cost per merged PR)

---

## Technique 1 — Stop feeding the model noise

Goal: strip routine command output (git status, test runs, builds) down to the signal, and stop paying for filler prose in responses.

### 1a. RTK — trim tool output

Repo: https://github.com/rtk-ai/rtk

**Install** (pick one):
```bash
# Homebrew (recommended)
brew install rtk

# Quick install script (Linux/macOS)
curl -fsSL https://raw.githubusercontent.com/rtk-ai/rtk/refs/heads/master/install.sh | sh

# Cargo
cargo install --git https://github.com/rtk-ai/rtk
```
Pre-built binaries (macOS/Linux/Windows) are also on the [releases page](https://github.com/rtk-ai/rtk/releases).

**Verify:**
```bash
rtk --version
rtk gain      # running tally of tokens saved
```

**Wire into Claude Code** (installs a `PreToolUse` hook that transparently rewrites Bash commands, e.g. `git status` → `rtk git status`):
```bash
rtk init -g
```
Restart Claude Code afterward for the hook to take effect.

**Wire into Codex** (instruction-based — patches `AGENTS.md` so Codex prefers `rtk <command>` for noisy shell output; there's no native hook mechanism):
```bash
rtk init -g --codex
```

Other supported agents, if relevant to your team: `--copilot` (GitHub Copilot), `--gemini` (Gemini CLI), `--agent cursor`, `--agent windsurf`, `--agent cline`.

**Useful flags:**
- `-g` — enables the auto-rewrite hook (needed for the transparent behavior above)
- `-u, --ultra-compact` — more aggressive compact output
- `-v, --verbose` — more detail when debugging RTK itself

**Discover what to wrap next:**
```bash
rtk discover
```
Mines your transcripts for noisy commands you haven't wrapped yet.

**Uninstall:**
```bash
rtk init -g --uninstall
```

Expect ~60–90% reduction on dev-loop output (git status, test runs, builds) per the article's field data.

---

### 1b. Caveman — trim the model's own prose

Repo: https://github.com/JuliusBrussee/caveman

**Install** (one-command, detects installed agents):
```bash
# macOS, Linux, WSL, Git Bash
curl -fsSL https://raw.githubusercontent.com/JuliusBrussee/caveman/main/install.sh | bash

# Windows PowerShell 5.1+
irm https://raw.githubusercontent.com/JuliusBrussee/caveman/main/install.ps1 | iex
```
Requires Node ≥18. Takes ~30s; safely skips agents you don't have.

**Agent-specific alternatives** if you only want it for one tool:
```bash
# Claude Code plugin marketplace
claude plugin marketplace add JuliusBrussee/caveman

# Gemini CLI
gemini extensions install https://github.com/JuliusBrussee/caveman

# Cursor / Windsurf / Cline / Codex
npx skills add JuliusBrussee/caveman -a cursor
```
(Full per-agent matrix is in the repo's `INSTALL.md`.)

**Usage:**
- Activate: type `/caveman` or say "talk like caveman" (Claude Code auto-enables it once installed)
- Set intensity: `/caveman [lite|full|ultra|wenyan]` — persists for the session
- `/caveman-stats` — session token usage + lifetime savings
- `/caveman-compress <file>` — permanently rewrite a memory file (e.g. CLAUDE.md) to cut input tokens
- `/caveman-commit` — terse conventional commit messages
- `/caveman-review` — one-line PR review comments
- Deactivate: say "normal mode"

Not everyone wants the blunt style — see the softer alternative below if you'd rather keep normal tone but cut filler.

### 1c. Manual output controls (no tool install needed)

Add to `CLAUDE.md` / `AGENTS.md`:
```
## Output style
- Reply in unified diff form. No full-file rewrites unless asked.
- No preamble, no trailing summary of what you just did.
- For research questions, answer in 10 lines or fewer unless I ask for depth.
```

Hard caps:
- Claude Code: set `CLAUDE_CODE_MAX_OUTPUT_TOKENS` (env var) to cap response length.
- Codex: set `model_verbosity = "low"` in config to make GPT-5-family models terse.
- If you use MCP tools, check their own response-size limits too — an overly generous tool response can flood context before the model acts.

---

## Technique 2 — Give the agent a map, not a phone book

Goal: replace "grep six files, read them top to bottom" with a structured query against a pre-built model of the repo. Pick **one** category that matches your pain point; don't stack all of them at once.

### Category A: Structural / call-graph tools ("how does this code connect?")

- **code-review-graph** — MCP server with a persistent, incremental graph, auto-rebuilds on save. This is the tool the article's author uses daily. The article does not provide a repository link, so no install command is given here — search for it directly if you want to try it, and confirm you're pulling the legitimate project before installing.
- **Serena** — LSP-backed, gives the agent precise go-to-definition / find-references.
  Repo: https://github.com/oraios/serena
  ```bash
  # Prereq: install `uv` package manager first
  uv tool install -p 3.13 serena-agent
  serena init                    # sets up language-server backend
  # serena init -b JetBrains     # optional: JetBrains backend instead
  ```
  Then configure a launch command in your MCP client (Claude Code, Codex, Claude Desktop, VSCode/Cursor, etc.) per the [client setup guide](https://oraios.github.io/serena/02-usage/030_clients.html).
  ⚠️ The repo explicitly warns: do **not** install Serena via an MCP/plugin marketplace — those versions are outdated. Use the `uv tool install` method above.

- **Aider's repo map** — ranked structural summary of a large project, used automatically by Aider itself (not a standalone MCP tool). Docs: https://aider.chat/docs/repomap.html
- **Glean** (Meta) — heavy-duty option for serious scale. https://glean.software/ (evaluate only if you're operating at an org-wide/monorepo scale — likely overkill for a single project).

### Category B: Semantic search tools ("where is the code that means this?")

- **Claude Context** — embeddings-based semantic search over your codebase.
  Repo: https://github.com/zilliztech/claude-context
  Prereqs: Node.js ≥ 20, an OpenAI API key, and a Zilliz Cloud vector DB endpoint (free tier available).
  ```bash
  claude mcp add claude-context \
    -e OPENAI_API_KEY=sk-your-openai-api-key \
    -e MILVUS_ADDRESS=your-zilliz-cloud-public-endpoint \
    -e MILVUS_TOKEN=your-zilliz-cloud-api-key \
    -- npx @zilliz/claude-context-mcp@latest
  ```
  Usage once configured:
  ```bash
  cd your-project-directory
  claude
  # then ask Claude: "Index this codebase"
  # then: "Check the indexing status"
  # then query naturally: "Find functions that handle user authentication"
  ```
  Also supports Cursor, Gemini CLI, Qwen Code, VS Code, and others via the same env vars in their respective MCP config files.

### Category C: Repo-packing tools ("give me the whole thing, cleanly packaged")

- **Repomix** — flattens a repo into a single AI-optimized file, respects `.gitignore`, counts tokens.
  Repo: https://github.com/yamadashy/repomix
  ```bash
  # No install needed
  npx repomix@latest

  # Or install globally
  npm install -g repomix     # or: yarn global add repomix / bun add -g repomix / brew install repomix

  # Run
  repomix                    # writes repomix-output.xml

  # Optional: generate a config file to customize behavior
  repomix --init
  ```

### Make the graph the default move, not the fallback

Whichever tool you pick, add a nudge to `CLAUDE.md` / `AGENTS.md` so the agent reaches for it before grepping:
```
## Code exploration
Before any Grep/Glob/Read, call the code graph / semantic search tool:
- semantic_search / find-references to locate functions/classes by intent
- impact-radius query before edits with a wide blast radius
- change-detection + review-context for code review
Fall back to Grep/Read only when the tool cannot answer.
```
(Adjust the tool-specific function names to whichever of Serena / Claude Context / code-review-graph you installed.)

---

## Technique 3 — Use the right model for the job

Goal: stop running every task on the frontier model. Route high-volume/low-ambiguity work to small models; reserve frontier models for multi-file changes, migrations, and anything where a wrong call is expensive.

### Routing map (from the article; specific model names will drift — keep the split)

| Tier | Models (example) | Use for |
|---|---|---|
| Small/fast | Claude Haiku, GPT `*-mini` | Triage, simple tests, doc edits, log classification, single-file refactors |
| Frontier/coding-specialist | Claude Sonnet/Opus, GPT-5-class | Multi-file changes, hard reviews, migrations, high-stakes calls |

### Claude Code: subagents

Create a subagent file (e.g. `.claude/agents/triage.md`) pinned to a cheap model with a tight output budget:
```markdown
---
name: triage
description: Classify an issue or test failure into a known bucket
model: haiku
tools: Read, Grep
---
You triage. Reply in 120 tokens or fewer with: bucket, confidence, next step.
```
Orchestrate with a capable model, delegate bounded, well-defined sub-tasks to the cheap specialist.

### Codex: custom agents (TOML)

Place under `~/.codex/agents/` or `.codex/agents/`:
```toml
name = "docs_researcher"
description = "Verify APIs, options, and version-specific behaviour before documentation edits."
model = "gpt-5.4-mini"
model_reasoning_effort = "medium"
sandbox_mode = "read-only"
developer_instructions = """
Use docs and local evidence before making claims.
Return concise answers with links or file references.
Do not edit application code.
"""
```
Can override: model, reasoning effort, sandbox mode, tools, MCP servers, instructions.

### Codex: profiles (manual routing at the task boundary)

`~/.codex/cheap.config.toml`:
```toml
model = "gpt-5.4-mini"
model_reasoning_effort = "low"
model_verbosity = "low"
```

`~/.codex/frontier.config.toml`:
```toml
model = "gpt-5.5"
model_reasoning_effort = "high"
model_verbosity = "medium"
```

Select per task:
```bash
codex --profile cheap "regenerate the changelog"
codex --profile frontier "plan the auth migration"
```

### Don't forget reasoning effort

Even within one model family, dial reasoning effort down for shallow tasks and up for hard ones — it's a separate lever from model choice and saves tokens on its own.

---

## Measurement — make it a habit, not a one-off cleanup

Track over time, not just once:
- **Cache-hit ratio** on your Claude Code / Codex sessions
- **Cost per merged AI-assisted PR**, month over month
- `rtk gain` (if RTK installed) for a running token-savings tally
- `/caveman-stats` (if Caveman installed) for session + lifetime savings

If both trends move in the right direction, scale what's working. If not, roll back the specific technique that isn't paying off — these are independent levers, not a package deal.

---

## Suggested rollout order for a first trial

1. **Day 1 (15 min):** Install RTK, run `rtk init -g` (or `--codex`), restart your agent, do a normal dev session, check `rtk gain`.
2. **Day 1 (10 min):** Add the `## Output style` block to `CLAUDE.md`/`AGENTS.md`; set `CLAUDE_CODE_MAX_OUTPUT_TOKENS` or `model_verbosity = "low"`.
3. **Day 2 (20 min):** Pick one Technique 2 tool matching your actual pain point (call-graph confusion → Serena; "where is this?" hunts → Claude Context; occasional whole-repo dump → Repomix) and wire it in with the exploration nudge.
4. **Day 3 (15 min):** Set up one Claude Code subagent (or Codex profile) for a repetitive low-stakes task you do often (e.g. triage, changelog generation) and route it to a cheap model.
5. **Ongoing:** Watch cache-hit ratio and cost/PR weekly; keep what moves the needle.
