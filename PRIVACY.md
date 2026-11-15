# Privacy policy — Agenteca plugin for Claude Code

Effective date: 15 November 2026.

This policy covers the Agenteca plugin for Claude Code (this repository) and the programs it starts: the `@agenteca/mcp` MCP server and the `ahub` command line (`@agenteca/cli`, `@agenteca/core`). Questions: <agenteca@proton.me>.

## In short

Agenteca collects nothing. The plugin runs on your computer, has no account, no telemetry and no server of its own, and sends nothing to the Agenteca project.

## What runs, and where

- **Everything runs locally.** The MCP server is started on your computer by `npx -y @agenteca/mcp@0.1.0`. It calls the `ahub` command line, also on your computer.
- **Files it writes.** When you agree to an installation, update or removal, `ahub` writes or removes the package's files in your project (or in your home folder for a user-scope installation), plus `apm.yml` and `apm.lock.yaml`, and keeps a cache of the git repositories it read (`~/.cache/ahub`). It writes the list of registries you add to `~/.config/ahub/config.json`. These files stay on your computer.

## Network requests

The plugin makes no request to an Agenteca service. It only contacts:

| Destination | When | What it receives |
|---|---|---|
| The npm registry (`registry.npmjs.org`) | When `npx` downloads `@agenteca/mcp` and its dependencies | The names and versions of these packages, your IP address |
| The git hosts of the packages you name (for example GitHub) | When you search, inspect, install or update a package | The repository requested, your IP address, and the credentials of your own git configuration for private repositories |
| The catalogs (registries) you add yourself | When you search a catalog | Your search terms, your IP address |

These services handle that information under their own privacy policies. Agenteca does not receive it.

## Credentials

The plugin asks for no password, token or key. Access to private repositories relies on your existing git configuration; `ahub` does not read, store or send your credentials itself.

## Claude

What the plugin's tools return (catalog results, package contents, installation plans) becomes part of your conversation with Claude, and is handled under Anthropic's terms and privacy policy.

## Retention

Agenteca keeps no data, because it receives none. The local files above remain until you delete them.

## Children

The plugin is a developer tool and is not intended for people under 18.

## Changes

Changes to this policy are published in this repository, and its history shows every version.
