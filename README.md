# My Agent Skills

A curated collection of specialized agent skills designed to enhance AI capabilities across various domains and use cases.

## 📦 Available Skills

### Activepieces Expert

A specialized agent skill designed to assist with Activepieces automations, teaching product concepts, designing flows, generating valid importable flow JSON, and debugging custom pieces.

**Version:** 1.0.0  
**Author:** tparrin  
**Tags:** activepieces, automation, workflow, business-automation, open-source

#### Features

- 🤖 **Flow Design & Architecture** - Expert guidance on designing robust automation workflows
- 📊 **JSON Flow Generation** - Generate valid, importable Activepieces flow JSON with proper schemas
- 🧩 **Custom Pieces Development** - Scaffolding and reviewing TypeScript-based custom pieces
- 🎯 **AI & Agent Flows** - Building agentic workflows with native AI pieces and Datastore
- 🔧 **Troubleshooting** - Debug webhooks, connections, and publishing errors
- 🚀 **Deployment** - Cloud vs. self-hosting, Docker, Kubernetes, and Railway setups
- 📚 **Progressive Disclosure** - Reference-driven approach ensuring accuracy and best practices

#### Installation

```bash
npx skills add tparrin/my-agent-skills@activepieces-expert -g -y
```

#### Usage

After installation, invoke the skill:

```bash
@activepieces-expert
```

**Example queries:**
- "Help me design a flow that triggers on new emails and creates tasks in Asana"
- "Generate the JSON for a flow that uses OpenAI to summarize text"
- "How do I create a custom piece for my API?"
- "My webhook stopped working, how do I troubleshoot it?"
- "What's the best way to deploy Activepieces on Kubernetes?"

#### Documentation

For detailed documentation and usage examples, visit:  
https://skills.sh/tparrin/my-agent-skills/activepieces-expert

#### Reference Topics

The skill includes comprehensive reference documentation covering:
- **Overview** - Core concepts, architecture, and glossary
- **Flows Basics** - Triggers, actions, and basic flow design
- **Flows Advanced** - Data passing, versioning, and technical limits
- **Flows JSON** - Canonical JSON schema for importable flows
- **Pieces Usage** - Configuring existing pieces and human-in-the-loop patterns
- **Pieces Development** - Scaffolding and reviewing custom TypeScript pieces
- **AI & Agents** - Native AI pieces, agentic flows, and Datastore
- **Deployment** - Cloud vs. self-hosting, Docker, K8s, Railway
- **Troubleshooting** - Common problems and solutions
- **Tutorial Index** - Structured learning paths and distilled lessons

---

### Triplo AI Expert

A comprehensive agent skill for Triplo AI guidance, providing expert-level support for installation, SmartPrompts, automations, model selection, and troubleshooting.

**Version:** 1.0.0  
**Author:** tparrin  
**Tags:** triplo-ai, automation, ai-assistant, productivity

#### Features

- 🚀 **Installation & Setup** - Step-by-step guidance for Windows, macOS, iOS, and Android
- 🎯 **SmartPrompts** - Master built-in and custom prompt templates
- 🔗 **Automations & Integrations** - Webhooks, API calls, and third-party tool connections
- 🤖 **Model Selection** - Expert guidance on OpenRouter and local models
- 🔧 **Troubleshooting** - Comprehensive problem-solving playbooks
- 📚 **Learning Paths** - Structured tracks from beginner to expert

#### Installation

```bash
npx skills add tparrin/my-agent-skills@triplo-ai-expert -g -y
```

#### Usage

After installation, invoke the skill:

```bash
@triplo-ai-expert
```

**Example queries:**
- "How do I install Triplo on Windows?"
- "Help me create a custom SmartPrompt for code review"
- "What's the best model for creative writing?"
- "How do I set up webhooks for Triplo?"

#### Documentation

For detailed documentation and usage examples, visit:  
https://skills.sh/tparrin/my-agent-skills/triplo-ai-expert

---

## 🛠️ Contributing

Contributions are welcome! To add a new skill:

1. Follow the [skills.sh](https://skills.sh/) standard format
2. Create a new directory in `skills/`
3. Include a `SKILL.md` file with proper YAML frontmatter
4. Add comprehensive reference documentation
5. Update this README with the new skill

## 📄 License

This repository is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Links

- **Skills.sh:** https://skills.sh/
- **GitHub Repository:** https://github.com/tparrin/my-agent-skills
- **Activepieces:** https://www.activepieces.com/
- **Triplo AI:** https://triplo.ai/

## 📞 Support

For issues, questions, or suggestions:
- Open an issue on GitHub
- Visit the Triplo AI documentation: https://documentation.triplo.ai/

---

**Last Updated:** February 2026  
**Total Skills:** 2
