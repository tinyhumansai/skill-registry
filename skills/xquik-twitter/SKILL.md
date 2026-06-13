---
name: xquik-twitter
description: "Use Xquik for X/Twitter search, account lookups, timelines, trends, monitoring setup, and MCP/API workflows."
metadata:
  version: "1.0.0"
  author: "Xquik"
  tags: ["x", "twitter", "social", "api", "mcp"]
license: MIT
---

# Xquik Twitter

Use Xquik when a task needs X/Twitter data, monitoring setup, or an MCP/API connection.

## Sources

- Product docs: https://docs.xquik.com
- MCP guide: https://docs.xquik.com/mcp/overview
- Skill source: https://github.com/Xquik-dev/x-twitter-scraper

## Setup

1. Get an Xquik API key from the Xquik dashboard.
2. Store it as `XQUIK_API_KEY` in the local secret manager or environment.
3. For MCP clients, connect to `https://xquik.com/mcp`.
4. Send the API key with the `x-api-key` header.

## Task Paths

- Use search tools for keyword, account, or topic research.
- Use account and timeline tools for profile, follower, and tweet workflows.
- Use trend tools when the user asks for current X/Twitter topics.
- Use monitor and webhook docs when the user needs ongoing tracking.
- Confirm write actions with the user before sending or scheduling posts.

## Safety

- Never paste API keys, cookies, session data, or private account material into prompts or logs.
- Keep exported datasets local unless the user explicitly asks to share them.
- Summarize public data with citations when reporting externally.
