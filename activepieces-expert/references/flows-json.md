Activepieces allows exporting flows as `.json` files. These files can be imported directly back into the platform. You will be asked to generate these JSON files from natural language descriptions.

## Table of Contents
- [Document Structure (v18)](#document-structure)
- [Metadata Guidelines](#metadata-guidelines)
- [Graph Guidelines (trigger and nextAction)](#graph-guidelines-trigger-and-nextaction)
- [Canonical Expression Syntaxes](#canonical-expression-syntaxes)
- [Placeholders & Connection Mapping](#placeholders--connection-mapping)
- [Flow Generation Example Shape](#flow-generation-example-shape)

## Document Structure
An Activepieces exported flow object has two main parts in the modern schema (v18+):
1. **Metadata**: Top-level keys such as `name`, `type` (`"SHARED"`), `pieces` (array of piece modules).
2. **`flows` array**: An array containing a single flow configuration object starting with `trigger`, and ending with `valid: true` and `schemaVersion: "18"`.
> **CRITICAL RULE**: Do not use the deprecated 'template' wrapper. Always use the `flows` array.

## Metadata Guidelines
- **`pieces`**: An array of string IDs representing every piece used in the flow (e.g., `["@activepieces/piece-schedule", "@activepieces/piece-http", "@activepieces/piece-openai"]`). Ensure it is comprehensive.
- **`name`**: The display name of the flow.

## Graph Guidelines (`trigger` and `nextAction`)
The flow starts with the `trigger`. The next step is nested inside the `trigger` under the key `nextAction`. Each step can have another `nextAction`.

**Common Fields:**
- `name`: An internal step slug. Useful for referencing this step's output later. Use snake_case (e.g., `trigger`, `step_1_format_date`).
- `displayName`: The human-readable name shown in the UI.
- `type`: Either `PIECE_TRIGGER` or `PIECE` (for actions). Webhooks are `WEBHOOK`. Loops use `LOOP_ON_ITEMS`. Branches use `BRANCH`.
- `settings`: The core configuration object.

**Settings Object (for type `PIECE` or `PIECE_TRIGGER`):**
- `pieceName`: The explicit ID of the piece (e.g., `@activepieces/piece-supabase`).
- `pieceVersion`: MUST BE A VALID VERSION STRING like `"~0.1.4"` or `"~0.4.0"`. Default to `"~0.1.0"` if unsure. NEVER use bracket variables like `{{PIECE_VERSION_LATEST}}` as it causes the UI loader to render a blank piece!
- `input`: The configuration arguments required by the piece.
- `propertySettings`: If an input property (like authentication, sender name, or table name) dynamically depends on user environments or contains a placeholder, **it MUST be registered here** as `{"type": "MANUAL"}` (see Placeholders section).
- `actionName` (or `triggerName`): The specific action slug within the piece you are calling. Example: Native Supabase uses `new_row`, not `trigger`.

## Canonical Expression Syntaxes
**Referencing Outputs**
You must wrap JSON paths inside `{{ }}`. Do NOT invent fields.
- Example: `"{{trigger.body.text}}"` or `"{{step_2.id}}"`

**Loops (`LOOP_ON_ITEMS`)**
- `type`: `"LOOP_ON_ITEMS"`
- `settings`: Contains an `items` array expression: `"{{step_list.items}}"`.
- The loop itself contains a `firstLoopAction` key, which is the start of a `nextAction` chain running *inside* the loop.

## Placeholders & Connection Mapping
When generating a `.json` for a user to import, they will need to provide auth connection details via the platform's Vault.
- Always use explicit placeholder syntax like `{{YOUR_CONNECTION_HERE}}` so they know exactly where to select their configuration.
- **CRITICAL**: If you put a placeholder in `input`, you MUST bind it in `propertySettings` as `MANUAL`.

Example mapping a dynamic `auth` and `table_name` field:
```json
"input": {
  "auth": "{{SUPABASE_CONNECTION}}",
  "table_name": "accounts"
},
"propertySettings": {
  "auth": { "type": "MANUAL" },
  "table_name": { "type": "MANUAL" }
}
```

## Flow Generation Example Shape
```json
{
  "name": "Daily Summary Flow",
  "type": "SHARED",
  "pieces": [
    "@activepieces/piece-schedule",
    "@activepieces/piece-openai",
    "@activepieces/piece-slack"
  ],
  "flows": [
    {
      "trigger": {
        "name": "trigger",
        "displayName": "Daily Schedule",
        "type": "PIECE_TRIGGER",
        "valid": true,
        "settings": {
          "pieceName": "@activepieces/piece-schedule",
          "triggerName": "cron_expression",
          "pieceVersion": "~0.1.0",
          "input": {
            "cronExpression": "0 8 * * *"
          }
        },
        "nextAction": {
          "name": "step_1_openai",
          "displayName": "Generate Summary",
          "type": "PIECE",
          "valid": true,
          "settings": {
            "pieceName": "@activepieces/piece-openai",
            "actionName": "ask_assistant",
            "pieceVersion": "~0.1.0",
            "input": {
              "connectionId": "{{CONNECTION_ID_OPENAI}}",
              "prompt": "Give me a summary of today."
            },
            "propertySettings": {
              "connectionId": { "type": "MANUAL" }
            }
          },
          "nextAction": {
            "name": "step_2_slack",
            "displayName": "Send to Slack",
            "type": "PIECE",
            "valid": true,
            "settings": {
               "pieceName": "@activepieces/piece-slack",
               "actionName": "send_channel_message",
               "pieceVersion": "~0.1.0",
               "input": {
                   "connectionId": "{{CONNECTION_ID_SLACK}}",
                   "channelId": "{{CHANNEL_ID}}",
                   "text": "{{step_1_openai.response}}"
               },
               "propertySettings": {
                  "connectionId": { "type": "MANUAL" },
                  "channelId": { "type": "MANUAL" }
               }
            }
          }
        }
      },
      "valid": true,
      "schemaVersion": "18"
    }
  ]
}
```
