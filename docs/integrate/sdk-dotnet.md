---
sidebar_position: 5
title: .NET SDK
---

# .NET SDK

The `LLMPort.Client` package wraps the official OpenAI .NET SDK and adds typed resources for llm.port platform features.

## Requirements

- .NET 8.0 or later
- `OpenAI 2.*`

## Installation

```bash
dotnet add package LLMPort.Client
```

## Quick start

```csharp
using LLMPort.Client;

var client = new LLMPortClient(
    baseUrl: "http://localhost:4000/v1",
    apiKey: "your-api-key"
);

// Standard OpenAI chat completion
var chatClient = client.GetChatClient("assistant-default");
var response = await chatClient.CompleteChatAsync("Hello");
Console.WriteLine(response.Value.Content[0].Text);
```

## Resources

Access llm.port extensions through typed resource properties:

```csharp
// Sessions
var session = await client.Sessions.CreateAsync("proj-1", "assistant-default");
var sessions = await client.Sessions.ListAsync("proj-1");
var messages = await client.Sessions.MessagesAsync(session.Id);

// Projects
var project = await client.Projects.CreateAsync("My Project");
var projects = await client.Projects.ListAsync();

// Tools
var tools = await client.Tools.AvailableAsync();
var policy = await client.Tools.GetPolicyAsync("sess-1");

// Memory
var facts = await client.Memory.ListAsync();
await client.Memory.CreateAsync("User prefers concise answers");

// Attachments
await client.Attachments.UploadAsync("sess-1", fileStream, "report.pdf");
var attachments = await client.Attachments.ListAsync("sess-1");

// Services
var health = await client.Services.HealthAsync();
```

## Architecture

`LLMPortClient` creates two internal HTTP clients:

1. An `OpenAIClient` pointed at the llm.port gateway — handles standard OpenAI operations
2. An `HttpClient` for extension endpoints — handles sessions, tools, memory, and other platform APIs

Use `client.GetChatClient(model)` for OpenAI operations and the resource properties (`client.Sessions`, `client.Tools`, etc.) for llm.port extensions.
