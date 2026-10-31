# Deploy and Host Nakama on Railway

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/new/template/nakama-ai-agents?referralCode=sLjDXb&utm_medium=integration&utm_source=button&utm_campaign=nakama-ai-agents)

[Nakama](https://github.com/ahmadrosid/nakama) is an AI agent platform built for teams. You chat with agents in a dashboard that feels like ChatGPT, and each agent has its own prompt, tools, skills, memory and MCP servers, plus channels in Telegram, WhatsApp, Discord and Slack. One server holds many organizations with invites and roles, and agents are isolated from each other. It's the same class of tool as OpenClaw or Hermes Agent, made for a team instead of one operator. This template runs a pinned Nakama release with your admin account created on first boot.

## About Hosting Nakama

One container with a volume. Nakama keeps everything in SQLite on the volume: users, organizations, agents, chats, memory, files and installed skills.

On first boot the server creates your admin account from `NAKAMA_SEED_ADMIN_EMAIL` and `NAKAMA_SEED_ADMIN_PASSWORD`, so the setup page is closed before anyone else can reach it. API keys and channel tokens you save in Nakama are encrypted with `NAKAMA_SECRETS_KEY`, generated when you deploy.

## Common Use Cases

- A shared AI assistant for a team, with per-agent tools and memory
- Agents that answer in your Telegram, Slack, Discord or WhatsApp
- Scheduled automations: daily reports, inbox triage, research digests
- A self-hosted alternative to OpenClaw or Hermes Agent with multi-user access

## Dependencies for Nakama Hosting

- An API key for a model provider (OpenAI, Anthropic, OpenRouter, Google and others), entered in Nakama after login.

### Deployment Dependencies

- [Nakama on GitHub](https://github.com/ahmadrosid/nakama)
- [Nakama docs](https://ahmadrosid.github.io/nakama/)

### Implementation Details

**First use:**

1. Enter your email as `NAKAMA_SEED_ADMIN_EMAIL` when you deploy.
2. Open the Nakama service's domain once it's green.
3. Log in with your email and `NAKAMA_SEED_ADMIN_PASSWORD` from the Variables tab, pick your model provider and paste its API key.
4. Change your password in Settings, then invite your team.

**Channels:** connect Telegram, Slack, Discord or WhatsApp per agent under the agent's Channels tab.

**Custom domain:** after adding one, set `NAKAMA_WEB_PUBLIC_URL` to it so OAuth callbacks and shared links use it.

Notes and limits:

- Keep `NAKAMA_SECRETS_KEY` safe and never change it: saved API keys and tokens can't be decrypted without it. Nakama can rotate it if you set the new key as `NAKAMA_SECRETS_KEY_NEXT` for one start.
- The seed variables only matter on first boot. Changing them later does not change the login.
- Use Railway's volume backups. Nakama's own scheduled backups need a second volume, which a Railway service can't have.
- The in-app Update button needs a Docker socket and isn't available here. Each template update pins a newer Nakama release.
- About 200 MB idle. Give the service more memory if agents run coding tools or many channels.

## Why Deploy Nakama on Railway?

Railway is a singular platform to deploy your infrastructure stack. Railway will host your infrastructure so you don't have to deal with configuration, while allowing you to vertically and horizontally scale it.

By deploying Nakama on Railway, you are one step closer to supporting a complete full-stack application with minimal burden. Host your servers, databases, AI agents, and more on Railway.
