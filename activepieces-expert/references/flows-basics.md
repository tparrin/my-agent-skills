# Flow Basics

A Flow is a structured sequence of operations defined as a graph. It consists of a series of "Steps".

## Triggers vs Actions

1. **Triggers:** Every flow starts with exactly ONE trigger. It defines *when* the flow runs.
   - **Polling Triggers**: The engine checks an external service every X minutes (e.g., checking for new emails).
   - **Webhook Triggers**: The flow runs instantly when it receives an HTTP payload at a specific URL.
   - **Schedule Triggers**: Runs on a cron expression (e.g., every day at 8 AM).
   - **App Events**: Triggered by specific events in connected third-party SaaS using their native webhook capabilities.

2. **Actions:** The steps that perform work after the trigger fires.
   - Action steps can make API calls, transform data, or run code.
   - They execute sequentially. 
   - A step can fail the flow, or it can be configured with Error Handling to continue upon failure.

## Basic Flow Topology

Flows are primarily vertical and linear, but they support standard control structures:
- **Linear**: Step 1 ➝ Step 2 ➝ Step 3
- **Branching (Router/Conditions)**: A step evaluates a condition and splits the flow into a "True" branch and a "False" branch. Inside the JSON, branches have their own `nextAction` chains.
- **Loops**: Iterates over an array of items. Inside the loop, a sub-chain of actions is executed for each item. 

## Flow Execution Context
When a flow executes, it generates a "Run". Each step in the run produces an output (usually a JSON object). Subsequent steps reference these previous outputs dynamically.
