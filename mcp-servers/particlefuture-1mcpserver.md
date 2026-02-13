---
title: "[1 MCP Server](https://mcp.1mcpserver.com/) 🚀"
url: "https://github.com/particlefuture/1mcpserver"
description: "🐍 ☁️ 🏠 🍎 🪟 - MCP of MCPs. Automatic discovery and configure MCP servers on your local machine."
sourceRepo: "particlefuture/1mcpserver"
tags: ["MCP", "IA", "Claude", "Cursor"]
date: 2026-02-13
language: "en"
stars: 40
forks: 9
---

# [1 MCP Server](https://mcp.1mcpserver.com/) 🚀

[![Website](https://img.shields.io/badge/Website-mcp.1mcpserver.com-blue?style=flat-square&logo=google-chrome)](https://mcp.1mcpserver.com/)

> **MCP of MCPs** — automatically discover and configure MCP servers on your machine (remote or local).

After setup, you can usually just say:

> “I want to perform . Call the `deep_search` tool and follow the outlined steps.”

The goal is that you only install **this** MCP server, and it handles the rest (searching servers, selecting servers, configuring servers, etc.).

### Demo video 🎥: [https://youtu.be/W4EAmaTTb2A](https://youtu.be/W4EAmaTTb2A) 

## Quick Setup
Choose **one** of the following:

1. **Remote** (simplest & fastest ⚡💨)
2. **Local (prebuilt)** — **Docker**, **uvx**, or **npx**
3. **Local (from source)** — run this repo directly

### 1) Remote 🌍⚡💨

Use the hosted endpoint (recommended for the simplest setup).

**Docs + guided setup:** [https://mcp.1mcpserver.com/](https://mcp.1mcpserver.com/)

#### Configure your MCP client

Add the following entry to your client config file:

* **Cursor**: `./.cursor/mcp.json`
* **Gemini CLI**: `./gemini/settings.json` (see Gemini docs)
* **Claude Desktop**:
  * macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
  * Windows: `%APPDATA%\Claude\claude_desktop_config.json`
* **Codex**: 
  * macOS: `~/.codex/config.toml`
  * Windows: `%USERPROFILE%\.codex\config.toml`

**Remote config (JSON):**

```json
{
  "mcpServers": {
    "1mcpserver": {
      "url": "https://mcp.1mcpserver.com/mcp/",
      "headers": {
        "Accept": "text/event-stream",
        "Cache-Control": "no-cache"
      }
    }
  }
}
```

If you already have other servers configured, just merge this entry under `mcpServers` For example:

```json
{
  "mcpServers": {
    "1mcpserver": {
      "url": "https://mcp.1mcpserver.com/mcp/",
      "headers": {
        "Accept": "text/event-stream",
        "Cache-Control": "no-cache"
      }
    },
    "file-system": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "."]
    }
  }
}
```

**Tip:** If your client supports it, move the config file into your **home directory** to apply globally.

---

### 2) Local (prebuilt) 💻

Use this when you want everything local, or when your MCP client only supports **STDIO**.

#### 2A) Docker 🐳
```bash
 docker run -p 8080:8080 ghcr.io/particlefuture/1mcpserver:latest
```
Running on other host ports: 
```bash
 docker run -p <FREE_HOST_PORT_NUM>:8080 ghcr.io/particlefuture/1mcpserver:latest
```
Running with stdio instead of streamable-http (You might see some delays when trying to connect): 
```bash
run --rm -i ghcr.io/particlefuture/1mcpserver:latest --local
```

```json
{
  "mcpServers": {
    "1mcpserver": {
      "url": "https://mcp.1mcpserver.com/mcp/"
    }
  }
}
```

#### 2B) npx 📦
```bash
npx -y @1mcpserver/1mcpserver
```

---

### 3) Local (from source) 🧩

Clone this repo and run directly.

```bash
git clone https://github.com/particlefuture/MCPDiscovery.git
cd MCPDiscovery
uv sync
uv run server.py --local
```

```json
{
  "mcpServers": {
    "1mcpserver": {
      "command": "/path/to/uv",
      "args": [
        "--directory",
        "<PATH_TO_CLONED_REPO>",
        "run",
        "server.py",
        "--local"
      ]
    }
  }
}
```

> If your client supports remote `url` servers, you can use the **Remote** setup instead.

#### Optional: grant file-system access 📁

If you want your LLM to have file-system access, add an MCP filesystem server and point it at the directory you want to allow:

```json
{
  "mcpServers": {
    "file-system": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "~/"]
    }
  }
}
```

---

## Architecture 🧠

There are two search modes:

### Quick Search ⚡

For explicit requests like: “I want an MCP server that handles payments.”

Returns a shortlist of relevant MCP servers.

### Deep Search 🌊

For higher-level or complex goals like: “Build a website that analyzes other websites.”

The LLM breaks the goal into components/steps, finds MCP servers for each part, and if something is missing, it asks whether to:

* ignore that part,
* break it down further, or
* implement it ourselves.

Deep Search stages:

1. **Planning** — identify servers, keys, and config changes
2. **Testing** — verify servers (via `test_server_template_code`)
3. **Acting** — execute the workflow using the configured servers

---

## Change Log 🕒

* July 31 2025: Upgrade to 0.2.0. Added agentic planning.
* Dec 12 2025: Support for Gemini + Codex
* Dec 13 2025: Easier local setup with docker and npm. 

## Future 🔮

* Better demo videos (new domain, narrated walkthrough)
* Model Context Communication Protocol (MCCP): standard server-to-server messaging
* Avoid calling tools with an `internal_` prefix unless instructed
* Improve MCP server database schema: server, description, url, config json, extra setup (docker/api key/etc)

## Credits 🙏

Data sources:

* wong2/awesome-mcp-servers
* metorial/mcp-containers
* punkpeye/awesome-mcp-servers
* modelcontextprotocol/servers

Published to:

* [https://mcpservers.org/](https://mcpservers.org/)
* [https://glama.ai/mcp/servers](https://glama.ai/mcp/servers)

## Troubleshooting 🧰

* If using a venv and you get `ModuleNotFoundError` even after installing: delete the venv and recreate it.

Please create an issue or directly contact me zjia71@gatech.edu if you encounter ANY issue of frustration. I really hope the setup is as smooth as possible!!

## Star History
[![Star History Chart](https://api.star-history.com/svg?repos=particlefuture/1mcpserver&type=Date)](https://star-history.com/#particlefuture/1mcpserver&Date)
