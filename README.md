# Skills — Reusable Skills & Agents for AI Agents

A curated collection of reusable **skills** and **agent definitions** that can be composed to build capable AI-powered workflows.

This repository now follows the marketplace-style layout used by [`github/copilot-plugins`](https://github.com/github/copilot-plugins): the repo root publishes marketplace metadata, and the installable plugin lives in `plugins/`.

## What's in this repo?

| Path | Description |
|------|-------------|
| `.github/plugin/marketplace.json` | GitHub Copilot marketplace index |
| `.claude-plugin/marketplace.json` | Claude-compatible marketplace index |
| `plugins/` | Installable plugin bundle containing all skills and agent bundles |

## Install from a Marketplace

Add the repository as a marketplace:

```bash
copilot plugin marketplace add trungnt13/skills
```

Install the bundled plugin from that marketplace:

```bash
copilot plugin install trungnt13-skills@trungnt13
```

Claude Code uses the same marketplace layout. Add the marketplace and install the plugin with:

```bash
/plugin marketplace add trungnt13/skills
/plugin install trungnt13-skills@trungnt13
```

If your Claude Code git setup prefers HTTPS, use:

```bash
/plugin marketplace add https://github.com/trungnt13/skills.git
```

## Direct Plugin Install

For GitHub Copilot CLI, the repository still keeps a compatibility `plugin.json` at the root, so direct installs continue to work:

```bash
copilot plugin install trungnt13/skills
copilot plugin install trungnt13/skills:plugins
copilot plugin install /abs/path/to/skills
copilot plugin install /abs/path/to/skills/plugins
```

Verify installed plugins with:

```bash
copilot plugin list
```

The included agents are exposed with plugin-qualified names such as:

- `trungnt13-skills/deepdive`
- `trungnt13-skills/boris`
- `trungnt13-skills/consensus`
- `trungnt13-skills/git-commit-push`

Run an agent directly:

```bash
copilot --agent trungnt13-skills/deepdive -p "Explain how this codebase is structured."
copilot --agent trungnt13-skills/boris -p "Implement this change with a plan-first, verify-first workflow."
copilot --agent trungnt13-skills/consensus -p "Compare the likely root cause of this bug and give me one final answer."
copilot --agent trungnt13-skills/git-commit-push -p "Commit and push the current changes with a conventional commit message."
```

Or, inside an interactive Copilot CLI session:

```text
/agent
/skills list
```

## Concepts

### Skill
A **skill** is a single, focused capability an agent can invoke — e.g., _web search_, _code execution_, _file I/O_, _summarisation_.  
Skills are:
- **Stateless** – they accept inputs and return outputs with no side effects beyond their declared scope.
- **Composable** – they can be chained or parallelised inside a workflow.
- **Typed** – inputs and outputs are described with a schema (JSON Schema / OpenAPI).

### Agent
An **agent** is a goal-directed entity that plans and calls skills to accomplish tasks.  
Agents are defined by:
- A **system prompt** (persona, constraints, output format)
- A **skill list** (which tools it may use)
- An optional **memory** backend (short-term context, long-term vector store)
- An **orchestration strategy** (ReAct, Plan-and-Execute, reflection loop, …)

## Included Agents

### `deepdive`
A first-principles research bundle for tracing behavior, explaining architecture, and pressure-testing conclusions with verifier and adversary subagents.

### `boris`
A coding agent adapted from Boris Cherny's latest public Claude Code workflow guidance. It starts complex work with a plan, insists on verification, and performs a cleanup/simplification pass before finishing.

Source baseline: `https://howborisusesclaudecode.com/api/install` version `2.2.0` dated `2026-02-27`. See `plugins/agents/boris/SOURCES.md` for provenance and adaptation notes.

## Marketplace Naming

The install target `trungnt13-skills@trungnt13` comes from two different fields:

- Plugin name: `plugins/plugin.json` `name` = `trungnt13-skills`
- Marketplace owner: `.github/plugin/marketplace.json` `owner.name` = `trungnt13`

Examples:

- Change only `plugins/plugin.json` `name` to `skills` and installs become `skills@trungnt13`
- Change only `.github/plugin/marketplace.json` `owner.name` to `team` and installs become `trungnt13-skills@team`
- Change both and installs follow the new pair

### `consensus`
A read-only coordinator that gathers focused context, dispatches the same brief to GPT, Claude, and Gemini worker agents, and synthesizes one evidence-backed answer for analysis and debugging tasks.

### `git-commit-push`
A user-invocable git workflow agent for staging, drafting conventional commits, committing, and pushing with safety checks.

Source baseline: copied from `notes-research/.github/agents/git.agent.md` on `2026-03-10`. The source repository is another local repo owned by the same author and did not declare a separate license file at the repo root when copied.

## Included Skills

### `vscode`
Instructions for working effectively in VS Code-focused environments.

### `obsidian-markdown`
Create and edit Obsidian-flavored Markdown notes with wikilinks, embeds, callouts, and frontmatter.

### `obsidian-bases`
Create and edit Obsidian `.base` files with views, filters, formulas, and summaries.

### `json-canvas`
Create and edit Obsidian/JSON Canvas `.canvas` files with nodes, edges, groups, and connections.

### `obsidian-cli`
Operate against a running Obsidian instance from the command line, including vault and plugin-development workflows.

### `defuddle`
Extract clean markdown from standard web pages using Defuddle.

The Obsidian-related skills above are vendored from [`kepano/obsidian-skills`](https://github.com/kepano/obsidian-skills) and kept in their original skill-directory layout.

## License

MIT
