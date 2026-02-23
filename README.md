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

#### 📜 Version History

**v1.0.0 (February 2026)**
- Initial release of Activepieces Expert skill
- Comprehensive reference documentation
- Progressive disclosure architecture
- Support for flow design, JSON generation, and custom pieces
- Removed Triplo AI references (February 23, 2026)

#### 💡 Real-World Use Cases

**1. Automated Lead Qualification**
- Trigger: New form submission from Typeform
- Action: Enrich lead data via Clearbit API
- Action: Score lead using OpenAI
- Action: Route to Salesforce or Slack based on score

**2. Social Media Content Pipeline**
- Trigger: Schedule (daily at 9 AM)
- Action: Fetch trending topics from RSS feeds
- Action: Generate social posts using OpenAI
- Action: Human approval via Slack
- Action: Post to Twitter/LinkedIn upon approval

**3. Customer Support Automation**
- Trigger: New support ticket from Zendesk
- Action: Categorize using AI
- Action: Check knowledge base for answers
- Action: Draft response
- Action: Send to human for review

---

## 🛠️ Contributing

We welcome contributions to improve the Activepieces Expert skill!

### How to Contribute

1. **Report Issues**: Found a bug or inaccuracy? Open an issue on GitHub
2. **Suggest Improvements**: Have ideas for new reference topics? Let us know
3. **Submit PRs**: Fix typos, add examples, or improve documentation

### Contribution Guidelines

- Follow existing documentation style and formatting
- Test any changes against actual Activepieces instances
- Update version number and changelog for significant changes
- Ensure all markdown links are valid
- Keep SKILL.md concise (<500 lines) and use progressive disclosure
- Place auxiliary documentation (README.md, CHANGELOG.md) in repository, not skill package

### Adding a New Skill

To add a new skill to this repository:

1. Follow the [skills.sh](https://skills.sh/) standard format
2. Create a new directory in the repository
3. Include a `SKILL.md` file with proper YAML frontmatter (name and description only)
4. Add comprehensive reference documentation in `references/` directory
5. Update this README with the new skill information

## 📄 License

This repository is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🔗 Links

- **Skills.sh:** https://skills.sh/
- **GitHub Repository:** https://github.com/tparrin/my-agent-skills
- **Activepieces:** https://www.activepieces.com/

## 📞 Support

For issues, questions, or suggestions:
- Open an issue on GitHub

---

**Last Updated:** February 23, 2026  
**Total Skills:** 1
