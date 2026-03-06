# Skills — Reusable Skills & Agents for AI Agents

A curated collection of reusable **skills** and **agent definitions** that can be composed to build capable AI-powered workflows.

## What's in this repo?

| Path | Description |
|------|-------------|
| `skills/` | Individual skill implementations (tools, functions, prompts) |
| `agents/` | Composed multi-agent workflows |

## Use as a GitHub Copilot CLI plugin

This repository can be installed directly as a Copilot CLI plugin and will expose the skills in `skills/` plus the agent bundles in `agents/`.

Install from GitHub:

```bash
copilot plugin install trungnt13/skills
```

Install from a local checkout:

```bash
copilot plugin install /abs/path/to/skills
```

Verify that the plugin loaded:

```bash
copilot plugin list
```

The included agents are exposed with plugin-qualified names such as:

- `trungnt13-skills/deepdive`
- `trungnt13-skills/boris`
- `trungnt13-skills/consensus`

Run an agent directly:

```bash
copilot --agent trungnt13-skills/deepdive -p "Explain how this codebase is structured."
copilot --agent trungnt13-skills/boris -p "Implement this change with a plan-first, verify-first workflow."
copilot --agent trungnt13-skills/consensus -p "Compare the likely root cause of this bug and give me one final answer."
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

Source baseline: `https://howborisusesclaudecode.com/api/install` version `2.2.0` dated `2026-02-27`. See `agents/boris/SOURCES.md` for provenance and adaptation notes.

### `consensus`
A read-only coordinator that gathers focused context, dispatches the same brief to GPT, Claude, and Gemini worker agents, and synthesizes one evidence-backed answer for analysis and debugging tasks.

## License

MIT
