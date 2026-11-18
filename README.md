# Mavery Automation Workflow Lab

A learning and portfolio repository for **n8n business automation**, **Claude AI integrations**, and reliable API workflows.

> Status: Planning / setup. No workflows have been implemented or tested yet.

## Goals

- Build practical, reproducible demonstrations for Fiverr services.
- Learn n8n triggers, expressions, data mapping, webhooks, APIs, and error handling.
- Publish sanitized workflow exports, sample payloads, screenshots, and verification notes.
- Keep customer data, API keys, OAuth tokens, and production credentials out of Git.

## Planned projects

| Project | Planned workflow | Status |
| --- | --- | --- |
| 01 — Lead Capture | Webhook → validation → deduplication → Google Sheets → notification | Planned |
| 02 — Claude Email Assistant | Email input → Claude classification/summary → draft reply → human approval | Planned |
| 03 — CRM Support | Customer inquiry → routing → CRM update → team notification | Planned |

## Repository layout

```text
workflows/
  01-lead-capture/
  02-claude-email-assistant/
  03-crm-support/
docs/
samples/
scripts/
```

Each project will eventually contain a workflow export, README, sample input/output, and test evidence.

## First milestone: Lead Capture MVP

**Acceptance criteria** (not yet complete):

1. A webhook accepts a documented sample lead payload.
2. Invalid or incomplete leads are rejected or routed for review.
3. Duplicate submissions are handled without creating duplicate records.
4. Valid new leads are written to a test Google Sheet.
5. A notification is generated for successful processing.
6. Test cases and sanitized workflow JSON are committed after manual review.

## Getting started

1. Install or access an n8n instance (Cloud or self-hosted).
2. Create a dedicated test Google Sheet and a test notification destination.
3. Build and test the workflow with fictional data.
4. Export workflow JSON **without credentials or sensitive values**.
5. Document setup, screenshots, tests, limitations, and cleanup steps.

See [docs/roadmap.md](docs/roadmap.md) for milestones.

## Security

Never commit `.env` files, tokens, API keys, client records, webhook secrets, or private customer data. Use n8n credential storage and test-only accounts. Treat exported workflow JSON as sensitive until reviewed: it may include webhook paths, endpoints, identifiers, or embedded sample data.

## License

No license selected yet. Do not assume third-party reuse rights until one is added.
