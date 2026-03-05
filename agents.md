# Agents

A catalogue of reusable agent definitions.  Each entry describes the agent's purpose, the skills it relies on, and configuration hints.

---

## Template

```
### <Agent Name>
**Description:** One-sentence summary of what the agent does.
**Skills:** comma-separated list of required skills
**Orchestration:** ReAct | Plan-and-Execute | Reflection | Custom
**System Prompt:** path or inline text
**Notes:** optional caveats, model recommendations, memory requirements
```

---

## Agents

### Research Agent
**Description:** Searches the web, reads sources, and synthesises a structured research report.  
**Skills:** `web_search`, `web_fetch`, `summarise`, `write_file`  
**Orchestration:** Plan-and-Execute  
**System Prompt:** `prompts/research_agent.md`  
**Notes:** Works best with a long-context model (≥ 32 k tokens). Outputs Markdown by default.

---

### Code Review Agent
**Description:** Reviews a pull request diff and surfaces bugs, security issues, and style violations.  
**Skills:** `read_file`, `grep`, `static_analysis`, `write_comment`  
**Orchestration:** ReAct  
**System Prompt:** `prompts/code_review_agent.md`  
**Notes:** Intentionally conservative — only reports high-confidence issues to keep signal-to-noise ratio high.

---

### Data Analysis Agent
**Description:** Loads structured data (CSV, JSON, SQL), runs exploratory analysis, and produces charts and insights.  
**Skills:** `read_file`, `execute_python`, `plot`, `summarise`  
**Orchestration:** Plan-and-Execute  
**System Prompt:** `prompts/data_analysis_agent.md`  
**Notes:** Requires a sandboxed code-execution environment. Outputs a Jupyter-compatible notebook alongside the summary.

---

### DevOps Agent
**Description:** Monitors CI/CD pipelines, triages failing builds, and suggests or applies fixes.  
**Skills:** `run_shell`, `read_file`, `write_file`, `git`, `web_search`  
**Orchestration:** ReAct  
**System Prompt:** `prompts/devops_agent.md`  
**Notes:** Scope-limit the `run_shell` skill to a sandboxed environment before deploying in production.

---

### Documentation Agent
**Description:** Reads source code and generates or updates documentation (READMEs, docstrings, API references).  
**Skills:** `read_file`, `write_file`, `glob`, `grep`, `summarise`  
**Orchestration:** Plan-and-Execute  
**System Prompt:** `prompts/documentation_agent.md`  
**Notes:** Pass `--dry-run` to preview changes before writing to disk.

---

### Q&A Agent
**Description:** Answers natural-language questions over a document corpus using retrieval-augmented generation.  
**Skills:** `vector_search`, `read_file`, `summarise`  
**Orchestration:** ReAct  
**System Prompt:** `prompts/qa_agent.md`  
**Notes:** Requires a pre-built vector index. Use `skills/index_documents` to build one from source files.

---

## Skill Reference

| Skill | Description |
|-------|-------------|
| `web_search` | Query a search engine and return ranked results |
| `web_fetch` | Fetch and parse the content of a URL |
| `read_file` | Read a file from the local filesystem |
| `write_file` | Write or overwrite a file on the local filesystem |
| `grep` | Search file contents with regex patterns |
| `glob` | Find files matching a path pattern |
| `run_shell` | Execute a shell command in a sandboxed environment |
| `execute_python` | Run Python code and capture stdout / artefacts |
| `git` | Interact with a Git repository (status, diff, commit, …) |
| `summarise` | Condense a long text into key points |
| `plot` | Generate a chart from tabular data |
| `vector_search` | Semantic similarity search over an embedded corpus |
| `write_comment` | Post a comment to a PR, issue, or code review thread |
| `static_analysis` | Run a linter or static analyser and return findings |
