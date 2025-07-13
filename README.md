# Byte History

**Byte History** is an autonomous platform that generates and publishes a daily programming or technology milestone using artificial intelligence.

## Overview

This repository serves as the monorepo and integration point for the Byte History platform, orchestrating the following components as submodules:

- **Worker**: Generates a new milestone daily using Gemini (Google Generative AI) and stores it in a PostgreSQL database.
- **API**: Exposes the latest milestone through a REST API, with caching, access control, and OpenAPI documentation.
- **Website**: Minimalist web interface that displays the daily milestone to end users.

## Architecture

```text
┌────────────┐      1. GitHub Actions (cron)
│   Worker   │ ──────────────────────────────┐
└────────────┘                               │
      │                                      │
      ▼                                      │
┌──────────────┐   2. Store milestone   ◄────┘
│  PostgreSQL  │◄────────────────────────────┐
└──────────────┘                             │
      │                                      │
      ▼                                      │
┌────────────┐   3. API exposes milestone    │
│    API     │───────────────────────────────┘
└────────────┘
      │
      ▼
┌────────────┐
│   Web      │
└────────────┘
```

**Flow**:

1. The **Worker** runs daily (00:00 ART) via GitHub Actions and generates a milestone using Gemini.
2. The milestone is stored in the PostgreSQL database (Supabase).
3. The **API** exposes the latest milestone via `/api/tech-milestones`, with caching and rate limiting.
4. The **Website** consumes the API and displays the milestone to users.

## Deployment

| Component                                                                             | Platform              |
| ------------------------------------------------------------------------------------- | --------------------- |
| [API](https://byte-history-api.onrender.com/swagger-ui.html)                          | Render                |
| [Website](https://byte-history-site.vercel.app/)                                      | Vercel                |
| [Worker](https://github.com/ZairBulos/byte-history-worker/actions/workflows/main.yml) | GitHub Actions (cron) |

## Getting Stated

To work with all components, clone this repository with submodules:

```sh
git clone --recurse-submodules https://github.com/ZairBulos/byte-history.git
```

For setup and development instructions, see the README in each submodule.

## License

This project is licensed under the [MIT License](./LICENSE).
