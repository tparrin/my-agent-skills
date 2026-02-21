# Advanced Flow Concepts

## Passing Data (Expressions)

Activepieces allows dynamic variable insertion from previous steps. In the UI, this is the "Data to Insert" panel. In the underlying JSON, data passing is represented by expressions wrapped in double curly braces `{{ }}`.

- **Syntax:** `{{step_slug.path.to.property}}`
- **`step_slug`:** This is the internal `name` of the step (e.g., `trigger`, `step_1`, `format_date`).
- Example: If a trigger named `trigger` outputs a body containing `user_id`, a later HTTP action can use the URL `https://api.example.com/users/{{trigger.body.user_id}}`.

**Rules for Expressions:**
- You must use exact JSON paths.
- Arrays can be accessed via indices: `{{step_1.items[0].name}}`.
- Always verify that the step slug used in the expression *actually exists* earlier in the graph.

## Versioning & Publishing

- Flows have a Draft state and a Published state.
- Editing a flow changes the Draft. Executions in production run against the last Published version.
- When an agent generates or modifies flow JSON, it is generating the draft graph (the `version.template` object).

## Technical Limits

When designing flows, be aware of standard operational limits (these vary by hosting plan, but generally):
- **Execution Time limits**: Extremely long-running loops might time out. Prefer batch processing or splitting flows if execution takes many minutes.
- **Payload Size Limits**: Passing enormous JSON payloads (e.g., > 10MB) between steps can degrade performance or hit limits depending on the infrastructure (Redis/Postgres queues).
- **Loops**: While looping is supported, high-volume iterations (say, 50,000 items) are better handled in native code steps or batch endpoints rather than 50,000 individual Activepieces step executions to save on task counts and execution time.
