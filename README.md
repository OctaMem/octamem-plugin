<p align="center">
  <img src="assets/logo.png" alt="OctaMem" width="96" />
</p>

<h1 align="center">OctaMem Plugin</h1>

<p align="center">
  Persistent memory for Claude Code and Codex.
</p>

<p align="center">
  <a href="https://octamem.com">Website</a> ·
  <a href="https://octamem.com/docs">Documentation</a> ·
  <a href="https://platform.octamem.com">Dashboard</a> ·
  <a href="https://octamem.com/contact">Support</a>
</p>

---

## Overview

AI coding assistants start every session without context. Project conventions, architecture
decisions and personal preferences have to be explained again each time.

OctaMem gives Claude Code and Codex a persistent memory that you own. Information you save in one
session is available in later sessions, on other machines, and in every other application connected
to the same memory, including Claude, ChatGPT, Cursor and the OctaMem web and desktop apps.

This repository contains the official OctaMem plugin and plugin marketplace for Claude Code and
Codex. The plugin connects to the hosted OctaMem MCP server at `https://mcp.octamem.com/mcp`.
No local services are required.

## Features

- **Persistent memory.** Facts, notes, preferences and decisions are retained across sessions,
  projects and machines.
- **Shared across tools.** The same memory is available in Claude Code, Codex, Claude, ChatGPT,
  Cursor and the OctaMem applications.
- **Secure sign-in.** Connections use OAuth 2.1 with PKCE. There are no API keys to copy or store in
  configuration files.
- **Scoped access.** Each connection is limited to the single memory you select when connecting.
- **User control.** Connected applications can be reviewed and disconnected at any time from the
  OctaMem dashboard. Access ends immediately when a connection is removed.

## Requirements

- An OctaMem account. You can create one at [platform.octamem.com](https://platform.octamem.com)
  during the first connection.
- Claude Code or the Codex CLI or app.

## Installation

### Claude Code

```bash
claude plugin marketplace add OctaMem/octamem-plugin
claude plugin install octamem@octamem
```

Start `claude`, run `/mcp`, select `plugin:octamem:octamem` and choose **Authenticate**. Sign in to
OctaMem in the browser window that opens, select a memory and choose **Allow**.

### Codex

```bash
codex plugin marketplace add OctaMem/octamem-plugin
codex plugin add octamem@octamem
codex mcp login octamem
```

The login command opens a browser window. Sign in to OctaMem, select a memory and choose **Allow**.

### Without the plugin

The MCP server can also be added directly.

Claude Code:

```bash
claude mcp add --transport http octamem https://mcp.octamem.com/mcp
```

Codex (`~/.codex/config.toml`):

```toml
[mcp_servers.octamem]
url = "https://mcp.octamem.com/mcp"
```

Then authenticate with `/mcp` in Claude Code or `codex mcp login octamem` in Codex.

## Usage

Once connected, ask the assistant in plain language. It decides when to read from or write to
memory.

```text
Remember that we deploy the backend with GitHub Actions to ECS in eu-west-1.
How do we deploy the backend?
Which OctaMem memory am I connected to?
```

To make memory use automatic in a project, add the following to the project's `CLAUDE.md` or
`AGENTS.md`:

```markdown
At the start of a task, search OctaMem for relevant context.
Save important decisions and conventions to OctaMem.
```

## Tools

| Tool | Description | Access |
|---|---|---|
| `search_memory` | Searches the connected memory for facts, notes and context relevant to a query. | Read |
| `save_memory` | Saves a fact, note or decision so it can be recalled later. | Write (no deletion) |
| `get_memory_info` | Returns the name and usage of the connected memory. | Read |

## How it works

1. The assistant connects to the hosted OctaMem MCP server.
2. On first use, you sign in to OctaMem in the browser and select the memory to connect.
3. The assistant receives an access token that is valid only for that memory.
4. Tokens are refreshed automatically. Removing the connection in the OctaMem dashboard revokes
   access immediately.

## Managing connections

| Task | How |
|---|---|
| View connected applications | [platform.octamem.com](https://platform.octamem.com) → Settings → Connected apps |
| Switch to a different memory | Disconnect the application, then authenticate again and select another memory |
| Use two memories in Claude Code | Add the server twice under different names, for example `octamem-work` and `octamem-personal` |
| Update the plugin | `claude plugin update octamem` or `codex plugin marketplace upgrade` |
| Remove the plugin | `claude plugin uninstall octamem` or `codex plugin remove octamem@octamem` |

## Frequently asked questions

**Where is my data stored?**
Your memory is stored in your OctaMem account. A connection can access only the memory you selected,
and you can revoke it at any time. See the [Privacy Policy](https://octamem.com/legal/privacy) and
[Security](https://octamem.com/security) pages for details.

**Does the assistant see my OctaMem password or API keys?**
No. Sign-in happens on platform.octamem.com. The assistant receives a scoped token only.

**The assistant did not use my memory.**
The assistant decides when to call tools. Ask it explicitly, for example "check my OctaMem memory",
or add the instructions shown under Usage to your project.

**I already use an OctaMem API key setup.**
Existing API key setups continue to work. The plugin is the recommended option for new
installations.

## Repository structure

```text
.claude-plugin/marketplace.json     Claude Code marketplace
.agents/plugins/marketplace.json    Codex marketplace
plugins/octamem/                    Plugin (Claude Code and Codex manifests, MCP configuration)
```

## Support

- Email: [support@octamem.com](mailto:support@octamem.com)
- Contact: [octamem.com/contact](https://octamem.com/contact)
- Issues: [github.com/OctaMem/octamem-plugin/issues](https://github.com/OctaMem/octamem-plugin/issues)

## License

Released under the [MIT License](LICENSE).
