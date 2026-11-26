# AGENTS.md

Guidance for coding agents working in this repository.

## What this repo is

Public documentation for YAMM MCP, and the YAMM plugin package. The repository root is the plugin package `yamm`, installed by the Claude Code marketplace (`.claude-plugin/marketplace.json`) and the Codex marketplace (`.agents/plugins/marketplace.json`) from `./`. `docs/plugin.md` describes the layout.

The MCP server source is **not** in this repo and is not open source.

## Rules

- **Never edit the package files directly**: `plugin.json`, `mcp.json`, `.claude-plugin/plugin.json`, `assets/` and `skills/`. They are synced from an internal repo on each release, and direct edits are overwritten by the next one.
- **Versioning**: this repo only carries clean release versions (`X.Y.Z`).
- **Plugin renames/removals** must go through a top-level `renames` map in `.claude-plugin/marketplace.json` so existing installs migrate instead of erroring.
- **Keep code out of this repo.** The repository root is the plugin folder that plugin directories scan.
- **Don't add a root `.codex-plugin/plugin.json`.** Codex reads `plugin.json`.
- **Don't add a root `.mcp.json`.** Claude Code loads a repository-root `.mcp.json` as a project-scoped MCP server for everyone who opens this repo, duplicating the plugin's `yamm` server. The Claude manifest declares the server inline instead.
- **Never add `command`-based (stdio/npx) MCP servers.** The plugin connects only to the hosted server over HTTPS.

## MCP configuration

`mcp.json` (`type: "streamable-http"`, read by Codex and other Agent Plugins clients) and the inline `mcpServers` block in `.claude-plugin/plugin.json` (`type: "http"`) declare the same server, `https://mcp.yamm.com/mcp`. They must always agree.
