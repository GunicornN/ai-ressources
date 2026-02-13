---
title: "Imagen3-MCP"
url: "https://github.com/hamflx/imagen3-mcp"
description: "📇 🏠 🪟 🍎 🐧 - A powerful image generation tool using Google's Imagen 3.0 API through MCP. Generate high-quality images from text prompts with advanced photography, artistic, and photorealistic controls."
sourceRepo: "hamflx/imagen3-mcp"
tags: ["MCP", "IA", "Cursor"]
date: 2026-02-13
language: "en"
stars: 53
forks: 12
---

# Imagen3-MCP

[English Version](#imagen3-mcp-english)

基于 Google 的 Imagen 3.0 的图像生成工具，通过 MCP（Model Control Protocol）提供服务。

## 效果

画一只奔跑的杰克罗素犬，长焦镜头，阳光透过狗狗的毛发，照片级画质

![奔跑的杰克罗素犬](./docs/Snipaste_2025-04-26_15-18-15.png)

画一个科技感十足的苹果

![科技感十足的苹果](./docs/Snipaste_2025-04-26_15-18-02.png)

## 安装要求

- 有效的 [Google Gemini API 密钥](https://aistudio.google.com/apikey)

## 安装步骤——Cherry Studio

1. 从 [GitHub Releases](https://github.com/hamflx/imagen3-mcp/releases) 下载最新版本的可执行文件
2. 将下载的可执行文件放置在系统中的任意位置，例如 `C:\bin\imagen3-mcp.exe`
3. 在 Cherry Studio 中配置：
   - Command 字段填写可执行文件路径，例如 `C:\bin\imagen3-mcp.exe`
   - 环境变量 `GEMINI_API_KEY` 中填写你的 Gemini API 密钥
   - [可选] 环境变量 `BASE_URL` 中填写代理地址，例如 `https://lingxi-proxy.hamflx.dev/api/provider/google`（这个地址可以解决 GFW 的问题，但是解决不了 Google 对 IP 的限制问题，因此还是得挂梯子）。
   - [可选] 环境变量 `SERVER_LISTEN_ADDR`：设置服务器监听的 IP 地址（默认为 `127.0.0.1`）。
   - [可选] 环境变量 `SERVER_PORT`：设置服务器监听的端口和图片 URL 使用的端口（默认为 `9981`）。
   - [可选] 环境变量 `IMAGE_RESOURCE_SERVER_ADDR`：设置图片 URL 中使用的服务器地址（默认为 `127.0.0.1`）。这在服务器运行在容器或远程机器上时很有用。

![配置](./docs/config.png)

## 安装步骤——Cursor

```json
{
  "mcpServers": {
    "imagen3": {
      "command": "C:\\bin\\imagen3-mcp.exe",
      "env": {
        "GEMINI_API_KEY": "<GEMINI_API_KEY>"
        // Optional environment variables:
        // "BASE_URL": "<PROXY_URL>",
        // "SERVER_LISTEN_ADDR": "0.0.0.0", // Example: Listen on all interfaces
        // "SERVER_PORT": "9981",
        // "IMAGE_RESOURCE_SERVER_ADDR": "your.domain.com" // Example: Use a domain name for image URLs
      }
    }
  }
}
```

## 许可证

MIT

---

# Imagen3-MCP (English)

An image generation tool based on Google's Imagen 3.0, providing services through MCP (Model Control Protocol).

## Examples

A running Jack Russell Terrier, telephoto lens, sunlight filtering through the dog's fur, photorealistic quality

![Running Jack Russell Terrier](./docs/Snipaste_2025-04-26_15-18-15.png)

A high-tech apple

![High-tech apple](./docs/Snipaste_2025-04-26_15-18-02.png)

## Requirements

- Valid [Google Gemini API key](https://aistudio.google.com/apikey)

## Installation Steps—Cherry Studio

1. Download the latest executable from [GitHub Releases](https://github.com/hamflx/imagen3-mcp/releases)
2. Place the downloaded executable anywhere in your system, e.g., `C:\bin\imagen3-mcp.exe`
3. Configure in Cherry Studio:
   - Fill in the Command field with the executable path, e.g., `C:\bin\imagen3-mcp.exe`
   - Enter your Gemini API key in the `GEMINI_API_KEY` environment variable
   - [Optional] Enter a proxy URL in the `BASE_URL` environment variable, e.g., `https://your-proxy.com`.
   - [Optional] Set the `SERVER_LISTEN_ADDR` environment variable: The IP address the server listens on (defaults to `127.0.0.1`).
   - [Optional] Set the `SERVER_PORT` environment variable: The port the server listens on and uses for image URLs (defaults to `9981`).
   - [Optional] Set the `IMAGE_RESOURCE_SERVER_ADDR` environment variable: The server address used in the image URLs (defaults to `127.0.0.1`). Useful if the server runs in a container or remote machine.

![Configuration](./docs/config.png)

## Installation Steps—Cursor

```json
{
  "mcpServers": {
    "imagen3": {
      "command": "C:\\bin\\imagen3-mcp.exe",
      "env": {
        "GEMINI_API_KEY": "<GEMINI_API_KEY>"
        // Optional environment variables:
        // "BASE_URL": "<PROXY_URL>",
        // "SERVER_LISTEN_ADDR": "0.0.0.0", // Example: Listen on all interfaces
        // "SERVER_PORT": "9981",
        // "IMAGE_RESOURCE_SERVER_ADDR": "your.domain.com" // Example: Use a domain name for image URLs
      }
    }
  }
}
```

## License

MIT
