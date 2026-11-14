# agenteca-claude-code

The Agenteca plugin for **Claude Code**. It adds the `/hub` command and declares the `agenteca` MCP server, so you can search, inspect, install, update and remove AI agent packages without leaving the tool.

Agenteca is a catalog and manager for agent packages: skills, agents, commands, hooks and MCP servers, installed from git repositories into Claude Code, Codex, GitHub Copilot and Cursor. Packages follow the OpenAPM format.

## Install

In Claude Code:

```
/plugin marketplace add agenteca/agenteca-claude-code
```

```
/plugin install agenteca@agenteca
```

## Use

| Command | What it does |
|---|---|
| `/hub search <words>` | Search the catalog |
| `/hub info <package>` | Show what a package contains before installing it |
| `/hub install <package>` | Install, after showing the plan and getting your agreement |
| `/hub update [package]` | Update |
| `/hub remove <package>` | Remove the package and its files |
| `/hub list`, `/hub outdated` | Installed packages, available updates |

The skill is named `hub` inside the `agenteca` plugin, so its full name is `/agenteca:hub`. The short form `/hub` works as long as no other command uses that name.

## What this plugin runs, fetches and writes

Nothing here is hidden; this section lists all of it.

- **It starts one local program.** The MCP server is launched with `npx -y @agenteca/mcp@0.1.0`: `npx` downloads that exact version of the [`@agenteca/mcp`](https://github.com/agenteca/agenteca-mcp) package, and its dependencies `@agenteca/cli` and `@agenteca/core`, from the npm registry. All three are open source under Apache-2.0.
- **It fetches git repositories you name.** When you search, inspect or install a package, the `ahub` command reads the catalog and clones the package's repository with `git`. No code from a package is executed during installation.
- **It writes files in your project, after you agree.** Installing a package writes that package's agents, skills, commands, hooks and MCP server entries into your project (for example under `.claude/`), plus `apm.yml` and `apm.lock.yaml`. Every write is listed in a plan first, and a file you edited by hand is never overwritten without a separate agreement.
- **It sends no telemetry.** The plugin, the MCP server and the CLI collect nothing and call no Agenteca service. The only network traffic is to npm (to fetch the packages above) and to the git hosts and catalogs you point it at.
- **It reads no credentials.** Access to private repositories relies on your existing git configuration.
- **It has no hooks.** The plugin itself contains one skill and one MCP server declaration.

Each package is scanned before installation (invisible Unicode, download-and-execute commands, and similar patterns). A package with a critical finding cannot be installed from the agent. The scan catches known tricks; it does not prove a package is safe, so read what you install.

## What is in this repository

| File | Role |
|---|---|
| `.claude-plugin/plugin.json` | Plugin manifest |
| `.claude-plugin/marketplace.json` | One-plugin marketplace, for direct installation from this repository |
| `.claude-plugin/icon.png` | Listing icon |
| `skills/hub/SKILL.md` | The `/hub` skill |
| `.mcp.json` | MCP server declaration |

## Status

Version 0.1.0. `@agenteca/mcp` is not on npm yet: until it is, the MCP server declared here will not start. Checked: `claude plugin validate . --strict` passes and `scripts/validate.mjs` passes. Not checked: a real installation through `/plugin marketplace add`, and running `/hub` in a session.

## Development

```bash
node scripts/validate.mjs
```

## License

Apache-2.0.
