---
sidebar_position: 3
title: SDK Overview
---

# SDK Overview

llm.port provides official SDKs that extend the OpenAI client libraries with platform-specific capabilities. Every SDK wraps the standard OpenAI client, so existing code targeting the OpenAI API works without changes — just point it at your llm.port gateway.

## Supported languages

| Language | Package          | Wraps             |
| -------- | ---------------- | ----------------- |
| Python   | `llmport`        | `openai` (Python) |
| .NET     | `LLMPort.Client` | `OpenAI` (C#)     |

## What the SDKs add

Standard OpenAI operations (`chat.completions`, `embeddings`, `models`) work out of the box. The SDKs add typed resources for llm.port extensions:

- **Sessions** — create, list, update, delete conversations; retrieve message history and summaries
- **Projects** — organize sessions into project workspaces
- **Tools** — query available MCP tools and manage per-session tool policies
- **Memory** — store and retrieve user-scoped memory facts
- **Attachments** — upload, list, and manage file attachments at session and project level
- **PII** — read and override per-session PII policies
- **Services** — health checks and service discovery

## Authentication

All SDKs authenticate with the same API token used for direct gateway requests. Pass the token as the `api_key` parameter when constructing the client.

## Next steps

- [Python SDK](sdk-python.md) — installation, setup, and usage examples
- [.NET SDK](sdk-dotnet.md) — installation, setup, and usage examples
