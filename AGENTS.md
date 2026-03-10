# AGENTS.md

## Purpose

- This repository is a plugin marketplace that ships one installable bundle in `plugins/`.
- Keep this file focused on shared project rules. Put personal preferences elsewhere.

## Repository Layout

- `.github/plugin/marketplace.json` is the marketplace manifest for GitHub Copilot CLI.
- `.claude-plugin/marketplace.json` mirrors the marketplace entry point for Claude-compatible tooling.
- `plugin.json` is a root compatibility manifest for direct installs; keep its `agents` and `skills` entries aligned with `plugins/`.
- `plugins/plugin.json` is the installable plugin manifest for Copilot direct installs.
- `plugins/.claude-plugin/plugin.json` is the installable plugin manifest for Claude-compatible tooling.
- `plugins/agents/<name>/` contains one agent bundle. Each bundle is folder-scoped and typically includes one primary `*.agent.md` file plus any subagents it invokes.
- `plugins/skills/<name>/SKILL.md` contains one reusable skill definition.
- `README.md` documents install and usage examples for any user-facing bundle added to the plugin.

## Editing Rules

- Preserve the marketplace layout. Keep installable content inside `plugins/` and do not move bundle content back to the repo root.
- When adding a new agent bundle:
  - Create a dedicated folder under `plugins/agents/`.
  - Keep the coordinator and subagents together in that folder.
  - Register the folder in `plugins/plugin.json` and the root `plugin.json`.
  - Update `README.md` if the bundle is user-invocable.
- When adding a new skill:
  - Create `plugins/skills/<name>/SKILL.md`.
  - Keep instructions concise and action-oriented.
- Whenever adding new agents or skills, update `README.md` examples to include them and if they are copied from existing ones, note the source and license.
- Prefer minimal, targeted edits. Do not reformat agent prompts unnecessarily.
- Preserve frontmatter keys and naming conventions used by existing `*.agent.md` files.

## Agent Authoring Conventions

- Keep agent instructions specific, structured, and brief.
- Make tool access explicit in frontmatter. Do not grant extra tools without a clear need.
- Distinguish clearly between read-only research agents and agents allowed to modify files.
- If an agent depends on subagents, make sure the referenced names match the subagent frontmatter exactly.
- Keep prompts self-contained; do not assume hidden repo knowledge beyond what this repository actually provides.

## Validation

- After changing marketplace or plugin metadata, verify `.github/plugin/marketplace.json`, `plugin.json`, `plugins/plugin.json`, and `plugins/.claude-plugin/plugin.json` parse as valid JSON.
- After adding or renaming an agent bundle, confirm the referenced directory and `*.agent.md` files exist.
- After changing user-facing agents or skills, update `README.md` examples and names to match the manifest.
- This repo currently has no dedicated automated test suite; use structural verification and manifest checks unless the repo gains tests later.

## Avoid

- Do not add repo instructions that are vague, aspirational, or not verifiable.
- Do not put personal workstation preferences in this file.
- Do not duplicate large prompt bodies in multiple places when one bundle-local file is the source of truth.
- Do not leave `README.md`, marketplace manifests, and plugin manifests out of sync with the actual plugin contents.

## Maintenance

- Make small atomic commits after each addition or change.
- DO NOT force push, keep main history clean and linear.
- Keep this file under roughly 200 lines. Split into nested instructions only if the repo grows enough to need path-specific overrides.
- If a subdirectory needs different rules later, add a closer `AGENTS.md` or `AGENTS.override.md` near that work instead of bloating this root file.
