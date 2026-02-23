# Activepieces JSON Flows Schema

Activepieces allows exporting flows as `.json` files. These files can be imported directly back into the platform. You will be asked to generate these JSON files from natural language descriptions.

## Table of Contents

- [Document Structure](#document-structure)
- [Metadata Guidelines](#metadata-guidelines)
- [Graph Guidelines](#graph-guidelines-trigger-and-nextaction)
- [Step Structure](#step-structure-actiontrigger)
- [Canonical Expression Syntaxes](#canonical-expression-syntaxes)
- [Placeholders](#placeholders)
- [Flow Generation Example](#flow-generation-example-shape)

## Document Structure
An Activepieces exported flow object has two main parts:
1. **Metadata**: Top-level keys such as `name`, `description`, `created`, `updated`, `tags`, and a `pieces` array.
2. **`template` (or `version`) object**: The actual flow graph, which contains a single `trigger` object.

## Metadata Guidelines
- **`pieces`**: An array of string IDs representing every piece used in the flow (e.g., `["@activepieces/piece-schedule", "@activepieces/piece-http", "@activepieces/piece-openai"]`). Ensure it is comprehensive.
- **`name`**: The display name of the flow.

## Graph Guidelines (`trigger` and `nextAction`)

The flow starts with the `trigger`. The next step is nested inside the `trigger` under the key `nextAction`. Each step can have another `nextAction`.

### Step Structure (Action/Trigger)

**Common Fields:**
- `name`: An internal step slug. Useful for referencing this step's output later. Use snake_case (e.g., `trigger`, `step_1_format_date`, `loop_items`).
- `displayName`: The human-readable name shown in the UI.
- `type`: Either `PIECE_TRIGGER` or `PIECE` (for actions). Webhooks are `WEBHOOK`. Loops use `LOOP_ON_ITEMS`. Branches use `BRANCH`.
- `settings`: The core configuration object.

**Settings Object (for type `PIECE` or `PIECE_TRIGGER`):**
- `pieceName`: The ID of the piece (e.g., `@activepieces/piece-slack`).
- `pieceVersion`: Pin to a specific version or leave as variable (use string). Usually denote with `"{{PIECE_VERSION_LATEST}}"`.
- `pieceType`: Often `"OFFICIAL"` or `"CUSTOM"`.
- `packageType`: Set to `"REGISTRY"`.
- `input`: The configuration arguments for the piece.
- `actionName` (or `triggerName`): The specific action slug within the piece you are calling.

## Canonical Expression Syntaxes

**Referencing Outputs**
You must wrap JSON paths inside `{{ }}`. Do NOT invent fields.
- Example: `"{{trigger.body.text}}"` or `"{{step_2.id}}"`

**Loops (`LOOP_ON_ITEMS`)**
- `type`: `"LOOP_ON_ITEMS"`
- `settings`: Contains an `items` array expression: `"{{step_list.items}}"`.
- The loop itself contains a `firstLoopAction` key, which is the start of a `nextAction` chain running *inside* the loop.

## Placeholders
When generating a `.json` for a user to import, they will need to provide auth connection details.
- Always use explicit placeholder syntax like `{{CONNECTION_ID_FOR_OPENAI}}` so they know exactly where to paste their configuration.
- Do NOT guess project IDs or secret tokens. 

## Flow Generation Example Shape

```json
{
  "name": "Daily Summary Flow",
  "description": "Triggered daily, fetches data and summarizes.",
  "pieces": ["@activepieces/piece-schedule", "@activepieces/piece-openai", "@activepieces/piece-slack"],
  "template": {
    "trigger": {
      "name": "trigger",
      "displayName": "Daily Schedule",
      "type": "PIECE_TRIGGER",
      "settings": {
        "pieceName": "@activepieces/piece-schedule",
        "triggerName": "cron_expression",
        "pieceVersion": "{{PIECE_VERSION_LATEST}}",
        "input": {
          "cronExpression": "0 8 * * *"
        }
      },
      "nextAction": {
        "name": "step_1_openai",
        "displayName": "Generate Summary",
        "type": "PIECE",
        "settings": {
          "pieceName": "@activepieces/piece-openai",
          "actionName": "ask_assistant",
          "pieceVersion": "{{PIECE_VERSION_LATEST}}",
          "input": {
            "connectionId": "{{CONNECTION_ID_OPENAI}}",
            "prompt": "Give me a summary of today."
          }
        },
        "nextAction": {
          "name": "step_2_slack",
          "displayName": "Send to Slack",
          "type": "PIECE",
          "settings": {
             "pieceName": "@activepieces/piece-slack",
             "actionName": "send_channel_message",
             "pieceVersion": "{{PIECE_VERSION_LATEST}}",
             "input": {
                 "connectionId": "{{CONNECTION_ID_SLACK}}",
                 "channelId": "{{CHANNEL_ID}}",
                 "text": "{{step_1_openai.response}}"
             }
          }
        }
      }
    }
  }
}
```
