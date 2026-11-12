# Incident communication

How Sail tells customers about outages and maintenance. The public record is https://status.savewithsail.com, backed by issues in this repository.

## Components

| Component | Slug (issue label) | Checked by |
|---|---|---|
| App | `app` | `https://app.savewithsail.com` returns 200 |
| Platform API | `platform-api` | `GET https://live.savewithsail.com/api/v1/merchants?limit=1` with a monitoring key returns 200 |
| Benefit Connect API | `benefit-connect-api` | `https://live.sail-platform.com/api/v1/` returns 200 |

Each component is checked about every 5 minutes. A response slower than 5 seconds shows as degraded.

## What happens automatically

When a check fails, Upptime opens an issue titled "🛑 <Component> is down", labelled `status` and the component's slug, and posts to `#platform-ops-prod`. When the check passes again, Upptime closes the issue. Every new issue is locked as soon as it's opened, so only Sail's team can comment.

## What the person on point does

**Post when** customers are affected for more than about 5 minutes. That includes outages Upptime can't see: a broken feature, wrong data, or a slow integration.

1. **Acknowledge within 15 minutes.** On Upptime's issue, comment what customers see and that you're investigating. If there's no issue yet, open one with the **Incident** template and add the slug label for each affected component.
2. **Update at least every 30 minutes** until it's resolved, even when nothing has changed ("Still investigating; next update by 14:30 UTC").
3. **Resolve.** Post a final comment saying what happened in customer terms and when service recovered, then close the issue. If Upptime already closed it, add the comment anyway.

Comments on the issue appear on the status page as updates. Edit the issue title as the situation changes, e.g. `[Investigating]`, then `[Identified]`, then `[Resolved]`.

## Scheduled maintenance

Open an issue with the **Scheduled maintenance** template at least 48 hours before customer-visible work. Fill in `start`, `end` (UTC) and `expectedDown` with the slugs of affected components. Close it when the work is done.

## Rules

These issues are **public and permanent**. GitHub keeps edit history, so a later edit doesn't remove anything.

- No customer or partner names, emails, user IDs, or any customer data.
- No internal hostnames, IP addresses, AWS resource names, stack traces, or log excerpts.
- No security details. For a security incident, say only that a service is affected; disclosure follows the security incident process, not this page.
- Describe impact in customer terms, not causes you haven't confirmed.

## Access

The engineering team has **Triage** access to `sail-team/status`, which allows commenting on locked issues and applying labels. Upptime runs as the `sail-status-bot` GitHub App.

## Evidence (SOC 2, GOV-6)

The closed `status` and `maintenance` issues are the record that incidents were communicated, with timestamps for each update. This document is the procedure.
