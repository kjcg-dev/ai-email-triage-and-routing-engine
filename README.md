# AI Email Triage and Routing Engine

Turn a chaotic inbox into an organized triage system. This Make.com automation reads every incoming email, uses an AI agent to instantly classify it, then routes it down the correct path — drafting a contextual reply, logging it for tracking, and alerting the team on Slack when something needs urgent attention.

## How it works

The automation watches a Gmail inbox (`google-email:triggerWatchNewEmails`) for new messages and passes the full email content to an AI Agent module (`ai-local-agent:RunLocalAIAgent`). The AI operates on a defined system prompt and returns structured JSON (`json:ParseJSON`) classifying the message into one of several categories — Customer Inquiry, Support/Issue, Sales Pitch, or Spam.

A router (`builtin:BasicRouter`) then sends each category down its own path: logging the inquiry to Google Sheets (`google-sheets:addRow`) and creating a draft reply (`google-email:createADraft`) ready for human review before sending. Messages flagged as urgent pass through a second, nested router that posts a real-time alert to the relevant Slack channel (`slack:CreateMessage`), ensuring nothing time-sensitive sits unnoticed in a shared inbox.

Drafts are created rather than auto-sent by design — this keeps a human in the loop for anything customer-facing while still eliminating the manual work of reading, sorting, and triaging every incoming email.

## Use case

Built for businesses receiving a high volume of mixed inquiries — sales, support, and general questions — where manually sorting each one wastes time and urgent issues risk getting buried. The AI classification removes the sorting bottleneck while keeping a human reviewing every reply before it goes out.

## Tech stack

- Make.com (AI Agent module + nested routing)
- Gmail API (trigger + draft creation)
- Google Sheets (categorized logging)
- Slack API (urgent alerts)

## Author

Kevin Gracias — Automation Specialist
