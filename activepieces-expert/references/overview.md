# Activepieces Overview

Activepieces is an open-source, AI-first business automation tool designed to connect apps, build AI agents, and automate workflows. It serves as an alternative to tools like Zapier and Make, but with a stronger focus on open ecosystem components (pieces) and human-in-the-loop AI orchestration.

## Key Product Concepts

- **Flows**: The core automation unit. A vertical graph starting with a single **Trigger** followed by a chain of **Actions**. Flows pass data from upstream steps to downstream steps using JSON paths.
- **Pieces**: The building blocks of flows (connectors). They represent integrations with third-party SaaS, internal tools, or utility functions (e.g., Google Sheets, OpenAI, HTTP, Code). Pieces are distributed as TypeScript npm packages.
- **AI-First & Agents**: Activepieces is uniquely positioned to handle AI automation. It supports pieces acting as "Tools" for external agents (like Claude or Custom GPTs) and has native agent capabilities to orchestrate multi-step LLM reasoning directly inside flows.
- **Human-in-the-Loop**: The ability for a flow to pause execution and wait for human approval (e.g., reviewing an AI-generated email before sending it).
- **Datastore**: A native lightweight key-value store built into Activepieces, useful for keeping state across different flow runs (e.g., remembering the last processed ID).

## Why Activepieces is Different
- **Open Source / Self-Hostable**: Can be run entirely on-premise or in private clouds for data sovereignty.
- **Code-Friendly**: While visually driven, it treats developers as first-class citizens. You can write generic TypeScript pieces or drop in JavaScript snippets directly into a flow.
- **Extensible Catalog**: Anyone can write and publish a piece. The community library is vast.
