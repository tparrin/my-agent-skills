# Activepieces Pieces Usage

Users will often ask you how to configure specific pieces (connectors like Google Sheets, OpenAI, HubSpot, Salesforce).

## General Configuration Logic

Every piece consists of:
1. **Triggers**: Events starting the flow.
2. **Actions**: Operations running within the flow.

### Authentication (Connections)
Most SaaS pieces require authentication, known in Activepieces as a "Connection". This is usually OAuth2 or an API Key.
As an agent, you **cannot** test these connections directly. When generating flow JSON, simply insert a placeholder like `{{CONNECTION_ID}}` and remind the user they must add the connection via the Activepieces UI.

## Human-in-the-Loop Pieces

A very common pattern is inserting a delay or an approval step in the middle of a flow.

1. **Wait / Delay Action**: Pauses execution for a specified amount of time.
2. **Approval Action**: Native (or via webhooks). The flow pauses entirely and sends an approval URL (e.g., to Slack or Email). A human clicks "Approve" or "Reject", then the flow resumes.
   - When modeling this in JSON, look for branching downstream that checks the `{{approval_step.status}}` (e.g., `APPROVED` or `REJECTED`).

## Common Configurations
- HTTP Request Piece: The swiss army knife. Use this when a specific piece doesn't exist. Supports custom headers, body payloads, auth types, and methods.
- Code Piece: Evaluates generic JavaScript/TypeScript snippets directly in the flow context. Extremely useful for complex object transformations that standard mappers struggle with.
