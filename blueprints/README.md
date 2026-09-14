# Blueprints

The actual Make.com scenario exports — not a description of the build, the build itself. Import either file directly into Make (**Scenarios → Create a new scenario → Import Blueprint**) to see every module, prompt, and field mapping exactly as configured.

- [`research-and-call-trigger.blueprint.json`](research-and-call-trigger.blueprint.json) — Scenario 1: watches for a qualified lead, researches the company, places the outbound call.
- [`call-result-and-followup.blueprint.json`](call-result-and-followup.blueprint.json) — Scenario 2: handles the end-of-call webhook, classifies the lead, generates the proposal, routes the notification.

See [`../docs/how-it-works.md`](../docs/how-it-works.md) for the module-by-module walkthrough.

## Before importing

These are sanitized exports — every account-specific identifier is replaced with a placeholder in angle brackets, and all connections need to be reattached. After import, replace:

| Placeholder | Where | What it is |
|---|---|---|
| `<AIRTABLE_BASE_ID>` / `<AIRTABLE_TABLE_ID>` | both files, Airtable modules | Your Lead Contacts base and table |
| `<VAPI_ASSISTANT_ID>` / `<VAPI_PHONE_NUMBER_ID>` | Scenario 1, Call Lead | Your Vapi assistant and outbound number |
| `<VAPI_STRUCTURED_OUTPUT_INTERESTED_ID>` / `<VAPI_STRUCTURED_OUTPUT_SUMMARY_ID>` | Scenario 2, interest filter + Update Lead | Your Vapi assistant's structured-output field IDs |
| `<GOOGLE_DOC_TEMPLATE_ID>` | Scenario 2, Proposal Generator | Your proposal Google Doc template |
| `<PRODUCT_TEAM_EMAIL>` / `<INTERNAL_BCC_EMAIL>` | Scenario 2, Notify Manager / Email Lead | Notification recipients |
| `<SLACK_CHANNEL_MARKETING_ID>` / `<SLACK_CHANNEL_TECH_ID>` / `<SLACK_CHANNEL_MIXED_ID>` / `<SLACK_CHANNEL_FOLLOWUP_ID>` | Scenario 2, Notify Team modules | Your Slack channel IDs |
| `<YOUR_BOOKING_LINK>` | Scenario 2, Email Lead | Your scheduling link |

Every `__IMTCONN__` connection (Airtable, OpenAI, Firecrawl, Google, Gmail, Slack) also needs reconnecting to your own accounts — Make clears these on import regardless, since credentials never travel with a blueprint. The Vapi API key is not in either file; the live scenario reads it at runtime from a Make data store (key `vapi-api-key`) so it never sits in the scenario body — see [Design notes](../docs/how-it-works.md#design-notes).
