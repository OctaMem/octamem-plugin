<p align="center">
  <img src="assets/logo.png" alt="OctaMem" width="120" />
</p>

<h1 align="center">OctaMem for Claude Code &amp; Codex</h1>

<p align="center">
  <strong>Long-term memory for Claude — remember once, recall everywhere.</strong>
</p>

<p align="center">
  <a href="https://octamem.com">Website</a> ·
  <a href="https://platform.octamem.com">Dashboard</a> ·
  <a href="#-quick-start">Quick start</a> ·
  <a href="#-tools">Tools</a> ·
  <a href="mailto:support@octamem.com">Support</a>
</p>

<p align="center">
  <img alt="Claude Code plugin" src="https://img.shields.io/badge/Claude%20Code-plugin-D97757" />
  <img alt="MCP" src="https://img.shields.io/badge/MCP-remote%20server-4B5563" />
  <img alt="OAuth 2.1" src="https://img.shields.io/badge/auth-OAuth%202.1%20%2B%20PKCE-2563EB" />
  <img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-16A34A" />
</p>

---

Every Claude Code session starts from zero. You explain your stack, your conventions, your
decisions — again. **OctaMem gives Claude a persistent memory you own**, so what you teach it today
is there in every session tomorrow, and in every other tool connected to the same memory.

```text
You:     Remember that we deploy the backend with GitHub Actions to ECS in eu-west-1.
Claude:  Saved to your OctaMem memory.

— a week later, new session —

You:     How do we deploy the backend?
Claude:  From your memory: GitHub Actions builds the image and deploys to ECS in eu-west-1.
```

## ✨ Why OctaMem

- **🧠 Memory that persists** — facts, notes, preferences and decisions survive across sessions,
  projects and machines.
- **🔁 One memory, every tool** — the same memory works in Claude Code, Claude.ai, Claude Desktop,
  ChatGPT, Cursor and the OctaMem web & desktop apps.
- **🔐 Secure one-click connect** — sign in with your OctaMem account (email, Google, Microsoft or
  Apple). No API keys to copy, no secrets in config files.
- **🗂️ You choose the memory** — pick which memory to connect (personal, work, a shared team
  memory). Keep projects separate by connecting different memories.
- **👀 Full control** — see every connected app and disconnect it any time from
  **Settings → Connected apps**. Disconnecting stops access immediately.
- **⚡ Zero setup** — a hosted remote MCP server. Nothing to run locally.

## 🚀 Quick start

**1. Install the plugin**

```bash
claude plugin marketplace add OctaMem/octamem-plugin
claude plugin install octamem@octamem
```

**2. Connect your memory**

Start `claude`, run `/mcp`, choose **octamem → Authenticate**. Your browser opens — sign in to
OctaMem (or create a free account), pick a memory and click **Allow**.

**3. Use it**

Just talk to Claude:

```text
Remember that I prefer TypeScript and pnpm for new projects.
What do you remember about our API conventions?
Which OctaMem memory am I connected to?
```

> **Prefer no plugin?** Add the server directly:
> `claude mcp add --transport http octamem https://mcp.octamem.com/mcp`, then `/mcp` → Authenticate.

## 🧩 Codex

The same repo is a Codex plugin marketplace.

**Plugin (Codex app / CLI)**

```bash
codex plugin marketplace add OctaMem/octamem-plugin
```

Then open the **Plugins** directory in Codex, choose the **OctaMem** source, install **OctaMem**, and
sign in when prompted (pick a memory, click **Allow**).

**Or add the server directly**

```bash
codex mcp add octamem --url https://mcp.octamem.com/mcp
codex mcp login octamem
```

or in `~/.codex/config.toml`:

```toml
[mcp_servers.octamem]
url = "https://mcp.octamem.com/mcp"
```

then run `codex mcp login octamem` to sign in.

## 🛠 Tools

| Tool | What it does | Access |
|---|---|---|
| `search_memory` | Searches your memory for facts, notes and past context relevant to a question | Read-only |
| `save_memory` | Saves a fact, note or decision so it can be recalled later | Write (never deletes) |
| `get_memory_info` | Shows which memory is connected and its usage | Read-only |

Claude decides when to use them. To be explicit, say *"check my memory"* or *"save this to OctaMem"*.

## 💡 Use cases

- **Project context** — architecture, deploy steps, environment quirks, "why we did it this way".
- **Personal preferences** — languages, frameworks, code style, review checklists.
- **Team knowledge** — connect a shared team memory so everyone's Claude knows the same conventions.
- **Cross-tool continuity** — save in Claude Code, recall in ChatGPT or the OctaMem app (and back).
- **Long-running work** — pick up a multi-day task without re-explaining where you left off.

### Make memory automatic in a project

Add this to your project's `CLAUDE.md`:

```markdown
At the start of a task, search OctaMem for relevant context.
Save important decisions and conventions to OctaMem.
```

## ⚙️ How it works

```text
Claude Code ──▶ OctaMem MCP server (mcp.octamem.com/mcp) ──▶ your OctaMem memory
     ▲                       │
     └── OAuth 2.1 + PKCE ───┘  sign in once at platform.octamem.com, pick a memory, Allow
```

1. Claude Code connects to the hosted OctaMem MCP server.
2. The first time, you sign in to OctaMem in your browser and choose which memory to connect.
3. Claude Code receives a token for **that memory only** — it can read and save to it, nothing else
   in your account.
4. Tokens refresh automatically; disconnect from **Connected apps** to revoke access instantly.

## 🔄 Managing your connection

| I want to… | Do this |
|---|---|
| See what's connected | [platform.octamem.com](https://platform.octamem.com) → Settings → **Connected apps** |
| Switch to another memory | Disconnect, then `/mcp` → octamem → **Authenticate** and pick another |
| Use two memories at once | `claude mcp add --transport http octamem-work https://mcp.octamem.com/mcp` (and another name for the second) |
| Update the plugin | `claude plugin update octamem` |
| Remove it | `claude plugin uninstall octamem` |

## ❓ FAQ

**Is my data private?**
Your memory belongs to your OctaMem account. A connection can only access the one memory you chose,
and you can revoke it at any time. Claude never sees your OctaMem password or API keys.

**Do I need an OctaMem account?**
Yes — sign up at [platform.octamem.com](https://platform.octamem.com) during the first connect.

**Does it work outside Claude Code?**
Yes. The same memory is available in Claude.ai and Claude Desktop (Settings → Connectors),
ChatGPT, Cursor, and the OctaMem web and desktop apps.

**Claude didn't use my memory — why?**
Claude chooses when to call tools. Ask explicitly ("check my OctaMem memory") or add the
`CLAUDE.md` snippet above.

**I already use an OctaMem API key setup.**
It keeps working. The plugin is the simpler, more secure option for new setups.

## 🤝 Support

- 📧 [support@octamem.com](mailto:support@octamem.com)
- 🌐 [octamem.com](https://octamem.com)
- 🐛 Issues: [github.com/OctaMem/octamem-plugin/issues](https://github.com/OctaMem/octamem-plugin/issues)

## 📄 License

[MIT](LICENSE) © OctaMem
