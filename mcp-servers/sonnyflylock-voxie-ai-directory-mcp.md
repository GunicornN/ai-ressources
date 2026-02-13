---
title: "AI Directory MCP Server"
url: "https://github.com/sonnyflylock/voxie-ai-directory-mcp"
description: "📇 ☁️ - AI Phone Number Directory providing access to AI services via webchat. Query Voxie AI personas and third-party services like ChatGPT, with instant webchat URLs for free interactions."
sourceRepo: "sonnyflylock/voxie-ai-directory-mcp"
tags: ["MCP", "IA", "Claude", "OpenAI"]
date: 2026-02-13
language: "en"
forks: 1
---

# AI Directory MCP Server

MCP (Model Context Protocol) server for the Voxie AI Phone Number Directory. Allows AI assistants to query information about AI services and get webchat URLs to interact with them.

## Installation

```bash
cd mcp-server
npm install
```

## Usage with Claude Desktop

Add to your Claude Desktop config (`claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "ai-directory": {
      "command": "node",
      "args": ["C:/Users/es/textmei-frontend/mcp-server/index.js"]
    }
  }
}
```

## Access Modes

### Public Mode (Default)
By default, the server runs in **public mode** which only exposes webchat URLs for Voxie services. This is the mode used when publishing to npm.

### Full Access Mode
For partners or internal use, set the environment variable to expose SMS/voice numbers:

```json
{
  "mcpServers": {
    "ai-directory": {
      "command": "node",
      "args": ["C:/Users/es/textmei-frontend/mcp-server/index.js"],
      "env": {
        "VOXIE_FULL_ACCESS": "true"
      }
    }
  }
}
```

## Available Tools

### `list_ai_services`
List all AI services or filter by provider type.
- `provider`: "all", "voxie", or "third-party"

### `get_ai_service`
Get details about a specific service by ID.
- `id`: Service ID (e.g., "voxie-us", "chatgpt-us")

### `find_ai_services_by_country`
Find services available in a specific country.
- `country`: Country name or partial match

### `chat_with_ai`
Get a webchat URL to chat with a Voxie AI persona (recommended).
- `persona`: "voxie", "rhodey", "soarie", "mia", or "wallie"

## Available Resources

- `ai-directory://services/all` - All services
- `ai-directory://services/voxie` - Voxie AI personas
- `ai-directory://services/third-party` - Third-party services

## API Endpoint

The directory is also available as a REST API at:
- `https://voxie.network/api/ai-directory`

Query parameters:
- `id` - Get specific service
- `provider` - Filter by "voxie" or "third-party"
- `country` - Filter by country name
- `channel` - Filter by "sms", "voice", or "webchat"

## Publishing to npm

```bash
npm publish --access public
```

The public npm package only exposes webchat URLs, protecting your SMS/voice costs.
