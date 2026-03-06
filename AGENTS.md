# AGENTS.md

## Purpose

- This repository is a GitHub Copilot CLI plugin that ships reusable agent bundles in `agents/` and skills in `skills/`.
- Keep this file focused on shared project rules. Put personal preferences elsewhere.

## Repository Layout

- `plugin.json` is the plugin manifest. Keep its `agents` and `skills` entries aligned with the filesystem.
- `agents/<name>/` contains one agent bundle. Each bundle is folder-scoped and typically includes one primary `*.agent.md` file plus any subagents it invokes.
- `skills/<name>/SKILL.md` contains one reusable skill definition.
- `README.md` documents install and usage examples for any user-facing bundle added to the plugin.

## Editing Rules

- Preserve the existing folder-based plugin structure. Do not register a new agent directly as a root file in `plugin.json`; register its directory.
- When adding a new agent bundle:
  - Create a dedicated folder under `agents/`.
  - Keep the coordinator and subagents together in that folder.
  - Register the folder in `plugin.json`.
  - Update `README.md` if the bundle is user-invocable.
- When adding a new skill:
  - Create `skills/<name>/SKILL.md`.
  - Keep instructions concise and action-oriented.
- Prefer minimal, targeted edits. Do not reformat agent prompts unnecessarily.
- Preserve frontmatter keys and naming conventions used by existing `*.agent.md` files.

## Agent Authoring Conventions

- Keep agent instructions specific, structured, and brief.
- Make tool access explicit in frontmatter. Do not grant extra tools without a clear need.
- Distinguish clearly between read-only research agents and agents allowed to modify files.
- If an agent depends on subagents, make sure the referenced names match the subagent frontmatter exactly.
- Keep prompts self-contained; do not assume hidden repo knowledge beyond what this repository actually provides.

## Validation

- After changing plugin metadata, verify `plugin.json` parses as valid JSON.
- After adding or renaming an agent bundle, confirm the referenced directory and `*.agent.md` files exist.
- After changing user-facing agents or skills, update `README.md` examples and names to match the manifest.
- This repo currently has no dedicated automated test suite; use structural verification and manifest checks unless the repo gains tests later.

## Current Project Facts

- The plugin name is `trungnt13-skills`.
- Current user-facing agent bundles are `deepdive`, `boris`, and `consensus`.
- The current skill tree contains `skills/vscode/SKILL.md`.

## Avoid

- Do not add repo instructions that are vague, aspirational, or not verifiable.
- Do not put personal workstation preferences in this file.
- Do not duplicate large prompt bodies in multiple places when one bundle-local file is the source of truth.
- Do not leave `README.md` and `plugin.json` out of sync with the actual plugin contents.

## Maintenance

- Keep this file under roughly 200 lines. Split into nested instructions only if the repo grows enough to need path-specific overrides.
- If a subdirectory needs different rules later, add a closer `AGENTS.md` or `AGENTS.override.md` near that work instead of bloating this root file.
