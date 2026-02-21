# Activepieces Tutorial Index & Distilled Lessons

This index contains distilled lessons from the Activepieces Automation School and community tutorials. Use this when users ask for conceptual guidance or "best practices" on how to orchestrate flows.

## 1. The "Human in the Loop" Pattern
- **Lesson**: Don't let AI run wild. If an AI generates a draft email or tweet, route the flow to a "Wait for Approval" piece. 
- **Execution**: Send the draft text to Slack/Discord with an Approve/Reject button. The flow pauses. Once clicked, the flow resumes, checks the `status` condition, and either posts the tweet or halts.

## 2. Using the Code Piece for Data Shaping
- **Lesson**: While Activepieces has data mapping pieces, complex nested JSON transformations are often easier in a Code piece.
- **Execution**: Drop in a Code step. Pass the upstream `{{trigger.body}}` into the Code step's `inputs` object. Write vanilla TS to `.map()`, `.filter()`, and `.reduce()` the data, then return the clean object.

## 3. Daily Summary / Digest Pattern
- **Lesson**: Avoid triggering an action for *every single item* (which costs tasks/credits). Instead, batch them.
- **Execution**: 
  1. Trigger 1 (Webhook): Webhook receives items throughout the day and pushes them to the **Datastore** (appending to a list).
  2. Trigger 2 (Schedule): Runs at 5 PM daily. Reads the list from the Datastore, formats it into an HTML email or Slack block, sends the digest, and then clears the Datastore list.

## 4. Connecting Custom Internal APIs
- **Lesson**: You don't always need to build a Custom TypeScript piece for internal tools.
- **Execution**: Use the `HTTP` piece with "Custom API Call". It handles Bearer tokens and generic JSON bodies perfectly well. Only build a custom TypeScript piece if non-technical users in the company will be using Activepieces and need a drag-and-drop UI with pre-defined dropdowns.
