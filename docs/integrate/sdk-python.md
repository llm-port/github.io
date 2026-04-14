---
sidebar_position: 4
title: Python SDK
---

# Python SDK

The `llmport` package extends `openai.OpenAI` with typed resources for llm.port platform features. All standard OpenAI operations work unchanged.

## Requirements

- Python ≥ 3.12
- `openai ≥ 1.50`

## Installation

```bash
pip install llmport
```

## Quick start

```python
from llmport import LLMPortClient

client = LLMPortClient(
    base_url="http://localhost:4000/v1",
    api_key="your-api-key",
)

# Standard OpenAI chat completion
response = client.chat.completions.create(
    model="assistant-default",
    messages=[{"role": "user", "content": "Hello"}],
)
print(response.choices[0].message.content)
```

## Async client

```python
from llmport import AsyncLLMPortClient

client = AsyncLLMPortClient(
    base_url="http://localhost:4000/v1",
    api_key="your-api-key",
)

response = await client.chat.completions.create(
    model="assistant-default",
    messages=[{"role": "user", "content": "Hello"}],
)
```

## Resources

### Sessions

```python
# Create a session
session = client.sessions.create(project_id="proj-1", model="assistant-default")

# List sessions
sessions = client.sessions.list(project_id="proj-1")

# Get message history
messages = client.sessions.messages(session.id)

# Get a summary
summary = client.sessions.summary(session.id)

# Check capacity
capacity = client.sessions.capacity()
```

### Projects

```python
project = client.projects.create(name="My Project")
projects = client.projects.list()
client.projects.update(project.id, name="Renamed")
client.projects.delete(project.id)
```

### Tools

```python
# List available MCP tools
tools = client.tools.available()

# Get session tool policy
policy = client.tools.get_policy(session_id="sess-1")

# Update tool policy
client.tools.update_policy(session_id="sess-1", overrides=[
    {"tool_id": "searxng_search.web_search", "enabled": False}
])
```

### Memory

```python
facts = client.memory.list()
client.memory.create(content="User prefers concise answers")
client.memory.delete(fact_id="mem-1")
```

### Attachments

```python
# Upload to session
attachment = client.attachments.upload(
    session_id="sess-1",
    file=open("report.pdf", "rb"),
)

# Upload to project
client.attachments.upload_to_project(
    project_id="proj-1",
    file=open("spec.md", "rb"),
)

# List and stats
attachments = client.attachments.list(session_id="sess-1")
stats = client.attachments.stats()
```

### PII policies

```python
# Read current session PII policy
policy = client.pii.get_session_policy(session_id="sess-1")

# Override session policy (clamped to tenant floor)
client.pii.update_session_policy(
    session_id="sess-1",
    egress_mode="local_only",
    presidio_enabled=True,
)

# Clear overrides (revert to tenant defaults)
client.pii.clear_session_policy(session_id="sess-1")
```

### Services

```python
health = client.services.health()
services = client.services.list()
```

## Error handling

```python
from llmport.exceptions import (
    LLMPortError,
    AuthenticationError,
    PermissionError,
    NotFoundError,
    RateLimitError,
)

try:
    client.sessions.get("nonexistent")
except NotFoundError:
    print("Session not found")
except RateLimitError:
    print("Too many requests")
except LLMPortError as e:
    print(f"API error: {e}")
```

## Exception hierarchy

| Exception             | HTTP status |
| --------------------- | ----------- |
| `AuthenticationError` | 401         |
| `PermissionError`     | 403         |
| `NotFoundError`       | 404         |
| `ValidationError`     | 422         |
| `RateLimitError`      | 429         |
| `InternalServerError` | 5xx         |
