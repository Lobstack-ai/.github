<div align="center">

<img src="public/lobstack-logo.png" alt="Lobstack" width="80" />

# Lobstack

### Infrastructure for AI Agents That Actually Work

Deploy autonomous AI agents on dedicated cloud infrastructure — with persistent memory, 700+ tool integrations, and multi-channel access. Live in 90 seconds. No DevOps required.

[![Website](https://img.shields.io/badge/Website-lobstack.ai-000?style=flat-square&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHdpZHRoPSIxNiIgaGVpZ2h0PSIxNiI+PHJlY3Qgd2lkdGg9IjE2IiBoZWlnaHQ9IjE2IiByeD0iMyIgZmlsbD0iI2U4NDE0MiIvPjwvc3ZnPg==)](https://lobstack.ai)
[![Docs](https://img.shields.io/badge/Docs-lobstack.ai%2Fdocs-333?style=flat-square)](https://lobstack.ai/docs)
[![License](https://img.shields.io/badge/License-Proprietary-e84142?style=flat-square)]()
[![Powered by](https://img.shields.io/badge/Powered%20by-OpenClaw-blue?style=flat-square)](https://github.com/openclaw/openclaw)

[**Get Started**](https://lobstack.ai) · [Documentation](https://lobstack.ai/docs) · [Report Bug](https://github.com/Lobstack-ai/lobstack/issues) · [Request Feature](https://github.com/Lobstack-ai/lobstack/issues)

</div>

---

## What is Lobstack?

Lobstack is the managed cloud platform for AI agents. Every agent gets its own **dedicated virtual machine** with persistent memory, real tool integrations, and multi-channel access — deployed in 90 seconds from a web dashboard or CLI.

Built on [**OpenClaw**](https://github.com/openclaw/openclaw), the open-source AI agent orchestration framework. Lobstack wraps OpenClaw into a product anyone can use — no terminal, no Docker, no infrastructure headaches.

```
lobstack deploy --model claude-opus --region us-east
```

> **Open-source engine. Managed cloud layer.** OpenClaw is the engine. Lobstack is the car. You can build from parts if you want, or drive off the lot in 90 seconds.

---

## Why Lobstack?

| | **Lobstack** | **DIY Setup** | **Other Platforms** |
|---|:---:|:---:|:---:|
| Dedicated VM per agent | Yes | Yes | **No** |
| Persistent agent memory | Yes | **No** | **No** |
| 700+ skill integrations | Yes | **No** | **No** |
| Multi-model (16 models) | Yes | Yes | Partial |
| 5 global regions | Yes | Yes | **No** |
| Deploy in < 2 minutes | Yes | **No** | Yes |
| No DevOps required | Yes | **No** | Yes |
| Omnichannel (Web, Telegram, Discord, Slack, API) | Yes | **No** | **No** |
| White-label options | Yes | Yes | **No** |
| Starts at $29/mo | Yes | **No** | **No** |

---

## Core Features

### Dedicated Infrastructure
Every agent runs on its own isolated cloud VM with dedicated CPU, RAM, and NVMe SSD. No shared compute, no cold starts, no noisy neighbors. Your agent gets its own machine.

### Persistent Memory
Agents retain preferences, context, and conversation history across sessions. Every interaction makes them sharper. Not "remembers last 10 messages" — remembers everything, permanently.

### 700+ Skill Integrations
Pre-built integrations with Gmail, GitHub, Slack, Discord, Twitter, Notion, Stripe, Calendar, Jira, Linear, and hundreds more. One-click install from the skills marketplace, or build your own.

### 16 AI Models, Hot-Swappable
Claude Opus 4.6, Claude Sonnet 4.5, GPT-5.2, GPT-5, GPT-5 Mini, GPT-5 Nano, GPT-4o, Gemini 2.5 Pro, and more. Switch models anytime — your agent keeps its memory, config, and skills.

### Multi-Channel Access
One agent, every channel. Web chat, Telegram, Discord, Slack, and REST API — all sharing the same memory and context. Your agent doesn't care where the message comes from.

### Visual Workflow Builder
Build automated multi-step workflows with cron triggers, webhook triggers, and manual execution. Drag-and-drop steps, template library, real-time execution tracking.

### 13,000+ MCP Servers
Connect to the Model Context Protocol ecosystem. Filesystem access, database queries, API integrations — all through the standardized MCP protocol.

### 20 Pre-Built Agent Templates
Ready-to-deploy templates for Customer Support, Sales, DevOps, Research, Content Creation, HR, Legal, Finance, Healthcare, Education, and more. One-click apply with full configuration.

### Global Deployment
Five regions across three continents: US-East (Virginia), US-West (Oregon), EU-Central (Frankfurt), EU-North (Helsinki), Asia-Pacific (Singapore). Deploy agents closest to your users.

### Enterprise-Grade Security
gVisor sandbox per agent, Istio mTLS, AES-256 encryption at rest, TLS 1.3 in transit, HashiCorp Vault for secrets management, full audit logging. SOC 2 Type II compliant.

---

## How It Works

```
Sign Up → Pick a Plan → Choose AI Model + Region → Deploy → Start Automating
```

1. **Sign Up** — Authenticate via Google, email magic link, or GitHub OAuth
2. **Pick a Plan** — Four tiers from $29/mo. Each includes a dedicated VM, persistent memory, and full skill access
3. **Deploy** — Select your AI model, choose a region, and hit deploy. Your agent is live in ~90 seconds
4. **Manage** — Full web dashboard: chat with your agent, install skills, build workflows, browse files, view logs, tweak config

---

## Use Cases

| Use Case | What It Does | Who It's For |
|---|---|---|
| **Customer Support** | Answers tickets 24/7 using your docs. Escalates when needed. | Startups, SaaS |
| **Personal Assistant** | Manages email, calendar, tasks. Remembers your preferences. | Founders, Executives |
| **DevOps Monitor** | Monitors servers, runs diagnostics, sends alerts with context. | Engineering Teams |
| **Sales Development** | Researches leads, crafts personalized outreach, manages follow-ups. | Sales Teams |
| **Social Media Manager** | Drafts content, posts on schedule, monitors engagement. | Creators, Marketing |
| **Content Creator** | Writes blogs, newsletters, threads. Maintains your voice. | Writers, Marketers |
| **Research Analyst** | Monitors news, competitors, and trends. Delivers daily briefings. | Strategy, Product |
| **Recruiting Assistant** | Screens resumes, schedules interviews, keeps candidates warm. | HR, Hiring Managers |
| **E-Commerce Ops** | Tracks inventory, adjusts pricing, analyzes customer behavior. | Online Retailers |
| **Financial Analyst** | Monitors markets, tracks portfolio, generates reports. | Finance Teams |

See all 20 templates and use cases at [lobstack.ai/docs/use-cases](https://lobstack.ai/docs/use-cases).

---

## Pricing

| Plan | Server | Price | Highlights |
|---|---|---|---|
| **Starter** | 4 GB RAM / 2 CPUs / 80 GB SSD | $29/mo | Everything you need to start |
| **Pro** | 4 GB RAM / 2 CPUs / 80 GB SSD | $59/mo | Custom system prompts, multi-region, priority support |
| **Performance** | 8 GB RAM / 4 CPUs / 160 GB SSD | $99/mo | API access, webhooks, higher limits |
| **Enterprise** | Custom | Contact us | SSO, SLA, white-label, dedicated support |

AI models are add-ons starting at +$4/mo. See full pricing at [lobstack.ai/pricing](https://lobstack.ai/pricing).

---

## Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | Next.js 16, React 19, Tailwind CSS 4, Framer Motion |
| **Backend** | Next.js API Routes, Supabase (PostgreSQL + Auth + Realtime) |
| **Payments** | Stripe Subscriptions |
| **Agent Runtime** | OpenClaw (open-source), MCP Protocol |
| **Infrastructure** | Dedicated VMs (Hetzner, DigitalOcean, Vultr), 5 global regions |
| **Security** | gVisor, Istio mTLS, AES-256, HashiCorp Vault, SOC 2 |

---

## Roadmap

- [x] One-click agent provisioning with multi-cloud support
- [x] Web dashboard (chat, skills, memory, sandbox, workflows, settings)
- [x] 16 AI models from Anthropic, OpenAI, Google, xAI
- [x] 700+ skill integrations + 13,000+ MCP server ecosystem
- [x] Visual workflow builder with triggers and templates
- [x] 20 pre-built agent templates across 9 categories
- [x] Multi-channel: Web, Telegram, Discord, Slack, API
- [x] Persistent memory with auto-extraction
- [x] Global deployment across 5 regions
- [x] Supabase Auth (Google, Email, GitHub OAuth)
- [x] Stripe subscription billing
- [ ] Open-source Skills + Tooling SDK
- [ ] Mobile app (iOS / Android)
- [ ] Custom skill marketplace
- [ ] Team / organization accounts
- [ ] Agent-to-agent communication
- [ ] Bring your own API key (BYOK)

---

## Documentation

Full documentation at **[lobstack.ai/docs](https://lobstack.ai/docs)**:

- [Quickstart](https://lobstack.ai/docs/quickstart) — Deploy your first agent in 90 seconds
- [Concepts](https://lobstack.ai/docs/concepts) — Agents, skills, memory, workflows
- [Architecture](https://lobstack.ai/docs/architecture) — System diagrams and data flows
- [Dashboard Guide](https://lobstack.ai/docs/dashboard) — Full dashboard walkthrough
- [Skills & Integrations](https://lobstack.ai/docs/skills) — Browse 700+ integrations
- [AI Models](https://lobstack.ai/docs/models) — All 16 supported models
- [Workflows](https://lobstack.ai/docs/workflows) — Automation builder guide
- [API Reference](https://lobstack.ai/docs/api) — REST API documentation
- [Security](https://lobstack.ai/docs/security) — Infrastructure and compliance details
- [Use Cases](https://lobstack.ai/docs/use-cases) — Real-world recipes and examples
- [Changelog](https://lobstack.ai/docs/changelog) — What's new in every release

---

## License

Proprietary — (c) 2026 Lobstack AI. All rights reserved.

This repository is public for transparency. The source code is not licensed for redistribution, modification, or self-hosting. The underlying agent runtime, [OpenClaw](https://github.com/openclaw/openclaw), is open-source and available separately.

---

<div align="center">

**Built by the Lobstack team**

[Website](https://lobstack.ai) · [Documentation](https://lobstack.ai/docs) · [GitHub](https://github.com/Lobstack-ai) · [Twitter](https://x.com/lobstackai)

</div>
