# AI and Agents in Activepieces

Activepieces brands itself as AI-first automation. This manifests in several ways.

## Native AI Pieces
- There are pieces for OpenAI, Anthropic, Google Gemini, local LLMs via Ollama, etc.
- These pieces usually offer actions like "Ask ChatGPT", "Generate Image", "Transcribe Audio".
- When passing data output into an AI prompt inside a JSON flow, leverage the `{{step_slug.data}}` expressions actively.

## Agent Orchestration (Agents as Flows)
You can configure a flow where an LLM is the "Brain" and other Activepieces act as its "Tools".
1. A flow receives a request (e.g., Slack Webhook trigger).
2. The flow routes the request to an Agent Action (e.g., OpenAI Assistant).
3. The LLM evaluates the prompt, decides it needs external data, and issues tool-calling events.
4. Activepieces handles mapping those tool calls dynamically to other specific pieces in the ecosystem (e.g., searching Google Drive, writing to a CRM) then returning the result to the LLM.
5. The LLM generates a final response sent back to the trigger channel.

## Activepieces Datastore
- The `Store` is extremely useful for keeping context between distinct flow runs (e.g., conversational memory for an AI bot).
- It is a simple key-value abstraction over Postgres. 
- You can Put, Get, and Delete values by Key.
