---
title: "mcpmcp-server"
url: "https://github.com/glenngillen/mcpmcp-server"
description: "☁️ 📇 🍎 🪟 🐧 - A list of MCP servers so you can ask your client which servers you can use to improve your daily workflow."
sourceRepo: "glenngillen/mcpmcp-server"
tags: ["MCP", "IA", "Claude"]
date: 2026-02-13
language: "en"
stars: 26
forks: 11
---

# mcpmcp-server

Discover, setup, and integrate MCP servers with your favorite clients. Unlock the full potential of AI in your daily workflow.

## Installation/usage:

Update the configuration of your MCP client to the following: 

```json
{
  "mcpServers": {
    "mcpmcp": {
      "command": "npx",
      "args": ["-y", "mcp-remote@latest", "https://mcpmcp.io/mcp"]
    }
  }
}
```

(**note:** this config definitely works for Claude Desktop on macOS. If you need variations for other apps or platforms check the [homepage](https://mcpmcp.io/#install)
