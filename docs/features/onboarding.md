---
sidebar_position: 10
title: Onboarding
---

# Onboarding

llm.port includes a guided onboarding experience that helps new users set up their environment and learn the platform. The onboarding system has two phases: a **Product Tour** introducing key concepts and a **Guided Setup** that walks through configuration tasks.

## How it starts

Onboarding triggers automatically on first login. Users are guided through:

1. **Profile selection** — choose a usage profile that tailors the experience
2. **Module recommendations** — suggested platform modules based on the selected profile
3. **Product Tour** — an 8-slide overview of platform capabilities
4. **Guided Setup** — interactive step-by-step configuration tasks

Onboarding can also be started manually from the **Help** menu (?) → **Guided Setup**, or reset via **Help** → **Reset Guides**.

## Profiles

The profile determines which modules are recommended and how many setup tasks are presented.

| Profile        | Icon | Description                                           | Setup tasks |
| -------------- | ---- | ----------------------------------------------------- | ----------- |
| **Private**    | 🏠   | Single-user local deployment                          | 4 tasks     |
| **Team**       | 👥   | Small team with shared models                         | 7 tasks     |
| **Enterprise** | 🏢   | Organization-wide deployment with auth and governance | 8 tasks     |

## Module recommendations

After selecting a profile, the system recommends platform modules. Default recommendations vary by profile:

| Module          | Private    | Team       | Enterprise |
| --------------- | ---------- | ---------- | ---------- |
| PII Guard       | ✅ default | ✅ default | ✅ default |
| RAG Lite        | —          | ✅ default | ✅ default |
| MCP Registry    | —          | —          | ✅ default |
| Skills Registry | —          | —          | ✅ default |
| Auth Providers  | —          | —          | ✅ default |

Users can add or remove modules from the recommendations before proceeding.

## Product Tour

The Product Tour is a dialog-based slideshow with 8 slides covering platform highlights. It provides an overview before hands-on setup begins.

## Guided Setup

The Guided Setup is an interactive tour that highlights specific UI elements and guides users through configuration tasks. It uses step-by-step instructions overlaid on the actual interface.

### Orientation phase

All profiles start with a 12-step orientation that walks through the main navigation areas:

- Sidebar sections (Chat, Models, Observability, RAG, MCP Tools, Skills, PII, Settings)
- Key actions in each section
- How to navigate between areas

### Task phase

After orientation, the tour presents profile-specific configuration tasks:

**Private profile (4 tasks):**

- Pull a model
- Configure basic settings
- Start a conversation
- Review PII defaults

**Team profile (7 tasks):**

- Everything in Private, plus:
- Set up team model access
- Configure RAG
- Review MCP tools

**Enterprise profile (8 tasks):**

- Everything in Team, plus:
- Configure authentication providers
- Set up organization-level governance

## Progress tracking

Tour progress is persisted per user. If a user leaves mid-tour, they can resume from where they left off. The system tracks which steps have been completed and which remain.

## Restarting the tour

Users can restart the onboarding experience at any time:

1. Click the **?** help icon in the navigation bar
2. Select **Guided Setup** to resume, or **Reset Guides** to start over from profile selection
