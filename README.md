# Skills — Reusable Skills & Agents for AI Agents

A curated collection of reusable **skills** and **agent definitions** that can be composed to build capable AI-powered workflows.

## What's in this repo?

| Path | Description |
|------|-------------|
| `skills/` | Individual skill implementations (tools, functions, prompts) |
| `agents/` | Composed multi-agent workflows |

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

## License

MIT
