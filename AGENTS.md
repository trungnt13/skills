# AGENTS.md

## Purpose

- This repository is a plugin marketplace that ships multiple installable plugins in `plugins/`.
- Keep this file focused on shared project rules. Put personal preferences elsewhere.

## Repository Layout

- `.github/plugin/marketplace.json` is the marketplace manifest for GitHub Copilot CLI.
- `.claude-plugin/marketplace.json` mirrors the marketplace entry point for Claude-compatible tooling.
- `plugin.json` is a root compatibility manifest for direct installs of the aggregate bundle; keep it aligned with `plugins/trungnt13-skills/`.
- `plugins/<plugin>/plugin.json` is the installable Copilot manifest for one marketplace plugin.
- `plugins/<plugin>/.claude-plugin/plugin.json` is the installable Claude manifest for the same plugin.
- `plugins/trungnt13-skills/` is the aggregate bundle that exposes all bundled agents and skills.
- `plugins/trungnt13-skills/agents/` and `plugins/trungnt13-skills/skills/` should symlink to the individually installable plugin content instead of copying it.
- `plugins/trungnt13-skills/` must always stay up to date with the individually installable plugins that belong in the aggregate bundle.
- `plugins/<agent-name>/agents/<agent-name>/` contains an individually installable agent bundle.
- `plugins/<skill-name>/skills/<skill-name>/SKILL.md` contains an individually installable skill bundle.

## Marketplace And Install

- Marketplace add:
  - `copilot plugin marketplace add trungnt13/skills`
  - `/plugin marketplace add trungnt13/skills`
- Aggregate install:
  - `copilot plugin install trungnt13-skills@trungnt13`
  - `/plugin install trungnt13-skills@trungnt13`
- Individual installs:
  - `copilot plugin install deepdive@trungnt13`
  - `copilot plugin install git-commit-push@trungnt13`
  - `copilot plugin install obsidian-markdown@trungnt13`
- Direct install paths:
  - `copilot plugin install trungnt13/skills`
  - `copilot plugin install trungnt13/skills:plugins/trungnt13-skills`
  - `copilot plugin install trungnt13/skills:plugins/deepdive`
  - `copilot plugin install trungnt13/skills:plugins/obsidian-markdown`

## Published Plugins

- Aggregate bundle: `trungnt13-skills`
- Agent plugins: `deepdive`, `boris`, `consensus`, `git-commit-push`
- Skill plugins: `vscode`, `obsidian-markdown`, `obsidian-bases`, `json-canvas`, `obsidian-cli`, `defuddle`

## Naming

- Install target format is `<plugin-name>@<marketplace-owner>`.
- `plugin-name` comes from `plugins/<plugin>/plugin.json` `name`.
- `marketplace-owner` comes from `.github/plugin/marketplace.json` `owner.name`.
- Example: `deepdive@trungnt13`.

## Editing Rules

- Preserve the marketplace layout. Keep installable content inside `plugins/` and do not move bundle content back to the repo root.
- When adding a new agent bundle:
  - Create a dedicated plugin folder under `plugins/<agent-name>/`.
  - Keep the coordinator and subagents together in that folder.
  - Register the plugin in `.github/plugin/marketplace.json`.
  - If the bundle should be part of the aggregate install, add the corresponding symlink under `plugins/trungnt13-skills/agents/` and register it in the aggregate manifests.
  - Keep the aggregate bundle up to date in the same change; do not leave the individual plugin and aggregate plugin out of sync.
  - Update `AGENTS.md` if the bundle is user-invocable.
- When adding a new skill:
  - Create a dedicated plugin folder under `plugins/<skill-name>/`.
  - Keep instructions concise and action-oriented.
  - If the skill belongs in the aggregate install, add the corresponding symlink under `plugins/trungnt13-skills/skills/` and register it in the aggregate manifests.
  - Keep the aggregate bundle up to date in the same change; do not leave the individual plugin and aggregate plugin out of sync.
- Whenever adding new agents or skills, update `AGENTS.md` examples to include them and if they are copied from existing ones, note the source and license.
- Prefer minimal, targeted edits. Do not reformat agent prompts unnecessarily.
- Preserve frontmatter keys and naming conventions used by existing `*.agent.md` files.

## Agent Authoring Conventions

- Keep agent instructions specific, structured, and brief.
- Make tool access explicit in frontmatter. Do not grant extra tools without a clear need.
- Distinguish clearly between read-only research agents and agents allowed to modify files.
- If an agent depends on subagents, make sure the referenced names match the subagent frontmatter exactly.
- Keep prompts self-contained; do not assume hidden repo knowledge beyond what this repository actually provides.

## Validation

- After changing marketplace or plugin metadata, verify `.github/plugin/marketplace.json`, `plugin.json`, and every touched `plugins/<plugin>/plugin.json` plus `plugins/<plugin>/.claude-plugin/plugin.json` parse as valid JSON.
- After adding or renaming an agent bundle, confirm the referenced directory and `*.agent.md` files exist.
- After adding or renaming an agent or skill that belongs in the aggregate bundle, confirm the `plugins/trungnt13-skills/` symlink exists and resolves to the intended source plugin directory.
- After changing user-facing agents or skills, update `AGENTS.md` examples and names to match the manifest.
- This repo currently has no dedicated automated test suite; use structural verification and manifest checks unless the repo gains tests later.

## Avoid

- Do not add repo instructions that are vague, aspirational, or not verifiable.
- Do not put personal workstation preferences in this file.
- Avoid unnecessary prompt drift across the aggregate plugin and individually installable plugins. Prefer symlinks from the aggregate bundle to the per-plugin source of truth instead of copying prompt bodies.
- Do not leave `AGENTS.md`, marketplace manifests, and plugin manifests out of sync with the actual plugin contents.

## Maintenance

- Make small atomic commits after each addition or change.
- DO NOT force push, keep main history clean and linear.
- Keep this file under roughly 200 lines. Split into nested instructions only if the repo grows enough to need path-specific overrides.
- If a subdirectory needs different rules later, add a closer `AGENTS.md` or `AGENTS.override.md` near that work instead of bloating this root file.
