# My Agent Skills

A curated collection of specialized, highly-optimized AI Agent skills for modern development workflows.

[![Skills.sh](https://img.shields.io/badge/Available%20on-skills.sh-blue?style=flat-square)](https://skills.sh)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)

## 🌟 Available Skills

### `activepieces-expert`

The complete brain for building on [Activepieces](https://www.activepieces.com/) – the open-source, AI-first business automation tool. 

This skill empowers your AI coding assistant (like Claude Code, Cursor, or Copilot) to:
- **Design & Critique:** Architect elegant automation flows and agents from natural language requirements.
- **Generate JSON:** Emit valid, importable Activepieces flow JSON directly into your clipboard or files.
- **Build Custom Pieces:** Scaffold and debug custom TypeScript pieces using the `@activepieces/pieces-framework`.
- **Troubleshoot:** Diagnose common real-world SaaS connection issues, webhook failures, and loop limitations.
- **Deploy:** Advise on self-hosting, Docker Compose setups, and cloud deployments.

## 🚀 Installation

These skills are distributed via the [skills.sh](https://skills.sh) open registry. You can install them globally to your AI agent environment using the `npx skills` CLI.

```bash
npx skills add tparrin/my-agent-skills@activepieces-expert -g -y
```

## 💻 Usage

Once installed, simply invoke the skill in your chat interface or CLI:

**Cursor / Windsurf:**
> `@activepieces-expert help me design a flow that posts to Slack when a new Stripe customer is created`

**Claude Code:**
> `/activepieces-expert generate the typescript code for a custom piece that connects to my internal API`

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/tparrin/my-agent-skills/issues).

## 📝 License

Distributed under the MIT License.
