# Tracker Schema

The canonical schema for Mark-Lite’s Google Sheets trackers. Mark-Lite reads this at the start of every run.

This schema is **IMMUTABLE**. Mark-Lite cannot add columns, rename columns, or restructure. If the live tracker does not match this schema, Mark-Lite MUST stop and escalate.

## Tracker Files

Two separate Google Sheets, one per region:

- **Mark-Lite Northants Outreach Tracker**
- **Mark-Lite Warwickshire Outreach Tracker**

Both trackers share the same 5-tab structure. Column order below is authoritative — the sheets follow this exact order left-to-right.

> **Regional differences:** Northants Companies has two extra columns at the end (Size Fit, Reply Outcome) that Warwickshire does not have. Northants Opportunities has two extra columns (Trade Confidence, Job Size) that Warwickshire does not have. Daily_Batches differs slightly (Northants uses Size Fit; Warwickshire uses Tier). All other columns are identical across both regions.

---

## Tab 1: Companies

Master prospect records.

| Column | Type | Description |
|---|---|---|
| Company Name | text | Company name |
| Tier | text | A / B / blank (prospect quality tier) |
| Trade | text | Primary trade (Groundworks / Brickwork / Scaffolding / Civil Engineering / Electrical / HVAC / Roofing / Drainage) |
| Website | URL | Primary website URL |
| Employee Count | number | Number of employees (if known) |
| Address | text | Registered or trading address |
| Contact Name | text | Full name of decision-maker (or blank if generic) |
| Contact Title | text | First name or short title for personalisation |
| Email | text | Primary email for outreach |
| LinkedIn URL | URL | LinkedIn profile or company page URL |
| Phone | text | Phone number (if known) |
| Email Status | text | New / Contacted / In Sequence / Warm / In Conversation / Opted Out / Bounced / Parked / Client |
| Last Email # Drafted | number | Which email they last had drafted (0 if none, 1-4 for sequence emails) |
| Date Email 1 Drafted | date | Date Email 1 was drafted |
| Date Email 2 Drafted | date | Date Email 2 was drafted |
| Date Email 3 Drafted | date | Date Email 3 was drafted |
| Date Email 4 Drafted | date | Date Email 4 was drafted |
| LI Status | text | LinkedIn status (LI Request Sent / LI Message 2 Sent / LI Message 3 Sent / LI Message 4 Sent / Company Page Only / blank) |
| LI Request Date | date | Date LinkedIn connection request was sent |
| LI Message 2 Date | date | Date LinkedIn message 2 was sent |
| LI Message 3 Date | date | Date LinkedIn message 3 was sent |
| LI Message 4 Date | date | Date LinkedIn message 4 was sent |
| Notes | text | Free-form notes |
| Size Fit | text | **Northants only.** Size description (e.g. Small to medium / Open to larger commercial) |
| Reply Outcome | text | **Northants only.** Summary of any reply received |

### Status Transitions (Allowed)

- New -> Contacted (after Email 1)
- Contacted -> In Sequence (after Email 1 response window passes)
- In Sequence -> Warm (on warm reply)
- In Sequence -> Opted Out (on opt-out reply)
- In Sequence -> Bounced (on bounce)
- In Sequence -> Parked (after Email 4, no response, plus 14-day window)
- Warm -> In Conversation (only Andy sets this)
- In Conversation -> Client (only Andy sets this)

Mark-Lite can set: Contacted, In Sequence, Warm, Opted Out, Bounced, Parked.
Only Andy can set: In Conversation, Client. If Mark-Lite finds these set, do not overwrite.

---

## Tab 2: Opportunities

All leads found across all sources.

| Column | Type | Description |
|---|---|---|
| Project Name | text | Name of the project |
| Town/Location | text | Location of the project |
| Description | text | Brief description of the project |
| Relevant Trades | text | Which trade(s) this lead is relevant for |
| Trade Confidence | text | **Northants only.** Confidence level per trade (Explicit / Inferred) |
| Job Size | text | **Northants only.** Small / Medium / Large |
| Source | text | Where the lead was found (PlanIt / Tender / Council / Manual) |
| Date Found | date | When the lead was discovered |
| Use By | date | Lead expiry date |
| Used In Email To | text | Company name (from Companies tab) if allocated and sent |
| Status | text | Available / Allocated / Sent / Expired |
| Contact Name | text | Decision-maker name (if known) |
| Contact Role | text | Role/title of the contact |
| Contact Company | text | Company the contact works for (e.g. developer, not the prospect) |
| Contact Email | text | Decision-maker email (if known) |
| Contact LinkedIn | URL | Contact's LinkedIn profile URL |

### Status Transitions (Allowed)

- Available -> Allocated (when matched to a prospect)
- Allocated -> Sent (when used in an approved email)
- Allocated -> Available (if prospect opts out or bounces; lead freed for reuse)
- Any -> Expired (after Use By date)

No lead can be used twice for the same prospect.

---

## Tab 3: Outreach_Log

Every email Mark-Lite drafts (and sends, after graduation).

| Column | Type | Description |
|---|---|---|
| Date Drafted | date | Date of draft |
| Company Name | text | Prospect (from Companies tab) |
| Contact Name | text | Who the email is addressed to |
| Email Address | text | Email address used |
| Email # | number | 1 / 2 / 3 / 4 / Re-engagement / Skip-gap |
| Subject Line Used | text | Email subject line |
| Projects Included | text | Lead/project names included in the email |
| Status | text | Pending Review / Approved / Edited / Rejected / Sent |
| Reply Summary | text | Summary of any reply received |
| Follow-up Action | text | Next step based on the reply |

Every drafted email creates a row, regardless of whether it's sent. Status columns update as the draft progresses through review and, if approved, sending.

---

## Tab 4: LinkedIn_Tasks

Manual tasks for Andy to action outside of email.

| Column | Type | Description |
|---|---|---|
| Date Prepared | date | When Mark-Lite prepared this task |
| Prospect Name | text | Company name |
| Contact Name | text | Who to contact |
| LinkedIn URL | URL | Profile URL for the contact |
| Task Type | text | Connection request / Message / Research |
| Message Text | text | The message to send (pre-written by Mark-Lite) |
| Status | text | Pending / Done / Skipped |

Mark-Lite can add rows and set Status=Pending. Only Andy changes Status to Done or Skipped.

---

## Tab 5: Daily_Batches

Batch assignments by day.

| Column | Type | Description |
|---|---|---|
| Day | text | Day of the week this batch is for (e.g. Monday) |
| Batch Order | number | Position in the day's batch |
| Prospect Name | text | Company name |
| Tier | text | **Warwickshire only.** Prospect tier (A / B) |
| Trade | text | **Northants only.** Primary trade |
| Size Fit | text | **Northants only.** Size description |
| Employee Count | number | Number of employees |

> **Note:** Northants Daily_Batches has columns: Day, Batch Order, Prospect Name, Trade, Size Fit, Employee Count. Warwickshire Daily_Batches has columns: Day, Batch Order, Prospect Name, Tier, Trade, Employee Count. The first three and last columns are shared; the middle columns differ by region.

---

## Schema Integrity Rules

1. Never add columns. If information doesn't fit, flag it to Andy in Slack.
2. Never rename columns or tabs.
3. Never change column order.
4. Never delete rows. Status changes reflect what happened; rows persist.
5. If a tracker is read and has columns or tabs that don't match this schema, STOP. Escalate to Slack. Do not write.
6. If a column you expect is empty where it shouldn't be (e.g. a Companies row with no email), flag it in the daily report, do not fill it in from inference.
7. Dates are UK format (DD/MM/YYYY) in the sheet. Parse accordingly.

## Updating This Schema

Only Andy updates this file. If Mark-Lite believes the schema needs changing (e.g. a new status that genuinely doesn't fit existing options), propose the change in Slack. Do not edit tracker-schema.md autonomously.
