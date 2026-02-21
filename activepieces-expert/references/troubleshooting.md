# Troubleshooting Activepieces

When users present errors or unexpected behavior in their flows, rely on these common heuristics before suggesting deep code changes.

## 1. Webhook Triggers Not Firing
If an App Webhook trigger isn't firing when an event occurs in the target app:
- Verify the connection has properly authorized the webhook scopes.
- Check if the flow is actually Published (webhooks and polling only work on Published flows, drafts won't trigger automatically).
- Check the Activepieces logs for `4XX` or `5XX` HTTP errors during the payload reception.

## 2. Polling Trigger Delays
If a user complains that a polling trigger is slow (e.g., waiting 10 minutes):
- Explain that polling intervals are governed by their hosting plan (Cloud) or their `SCHEDULE_POEL_INTERVAL` (Self-hosted).
- It is not instantaneous by design.

## 3. Empty or `undefined` Expressions
If a downstream step throws an error about missing data:
- `{{step_name.path.to.value}}`: Did they spell `step_name` exactly as it appears in the JSON `name` property?
- Did the upstream step actually output that payload in this specific Run? Sometimes HTTP endpoints return arrays instead of objects.
- In JSON mapping, suggest they use `firstLoopAction` or explicitly check array length `[0]` if dealing with lists.

## 4. Loop Performance
- Activepieces loop items are processed individually. If a user tries to loop over 50,000 rows, it will be incredibly slow and likely exhaust their task quota or timeout.
- Solution: Suggest writing a custom Code Piece or HTTP batch endpoint to process data in bulk instead of mapping a 50K item array to 50K Activepieces actions.

## 5. Publishing Failures
- "Failed to publish flow": Usually means the JSON `template` structure is invalid, a required `input` field on a piece is missing, or an expression `{{ }}` references a step name that does not exist in the graph.
