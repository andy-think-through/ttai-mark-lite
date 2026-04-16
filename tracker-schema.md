# Tracker Schema

> The canonical schema for Mark-Lite's Google Sheets trackers.
> Mark-Lite reads this at the start of every run.
> This schema is IMMUTABLE. Mark-Lite cannot add columns, rename columns, or restructure.
> If the live tracker does not match this schema, Mark-Lite MUST stop and escalate.

---

## Tracker Files

Two separate Google Sheets, one per region:

- **Mark-Lite Warwickshire Outreach Tracker**
- **Mark-Lite Northants Outreach Tracker**

Both trackers share the same schema. Tab names and column order below.

---

## Tab 1: Companies

Master prospect records.

| Column | Type | Description |
|--------|------|-------------|
| Company | text | Company name |
| Trade | text | Primary trade (Groundworks / Brickwork / Scaffolding / Civil Engineering / Electrical / HVAC / Roofing / Drainage) |
| Size-fit | text | Small / Medium / Large / Small jobs only |
| Contact Name | text | Named decision-maker (or blank if generic) |
| Contact Email | text | Primary email for outreach |
| Email Verified | text | Y / N / Pending (Hunter.io check) |
| Website | URL | Primary website URL |
| Status | text | New / Contacted / In Sequence / Warm / In Conversation / Opted Out / Bounced / Parked / Client |
| Email # | number | Which email they last received (0 if none) |
| Last Email Date | date | Date of last email sent |
| Next Action Date | date | Date next email is due (if in sequence) |
| Notes | text | Free-form notes |

### Status Transitions (Allowed)

- `New` -> `Contacted` (after Email 1)
- `Contacted` -> `In Sequence` (after Email 1 response window passes)
- `In Sequence` -> `Warm` (on warm reply)
- `In Sequence` -> `Opted Out` (on opt-out reply)
- `In Sequence` -> `Bounced` (on bounce)
- `In Sequence` -> `Parked` (after Email 4, no response, plus 14-day window)
- `Warm` -> `In Conversation` (only Andy sets this)
- `In Conversation` -> `Client` (only Andy sets this)

Mark-Lite can set: Contacted, In Sequence, Warm, Opted Out, Bounced, Parked.
Only Andy can set: In Conversation, Client. If Mark-Lite finds these set, do not overwrite.

---

## Tab 2: Opportunities

All leads found across all sources.

| Column | Type | Description |
|--------|------|-------------|
| Lead ID | text | Unique identifier (e.g. PLANIT-12345) |
| Date Found | date | When the lead was discovered |
| Source | text | PlanIt / Tender / Council / Manual |
| Project Name | text | Name of the project |
| Town | text | Location |
| Trade Relevance | text | Which trade(s) this lead is relevant for |
| Size | text | Small / Medium / Large |
| Contact Available | text | Y / N |
| Contact Name | text | Decision-maker name (if known) |
| Contact Email | text | Decision-maker email (if known) |
| Status | text | Available / Allocated / Sent / Expired |
| Allocated To | text | Company name (from Companies tab) if allocated |
| Email # | number | Which email this lead was used in (if sent) |
| Expiry Date | date | Lead expiry (21/42/56 days by size) |

### Status Transitions (Allowed)

- `Available` -> `Allocated` (when matched to a prospect)
- `Allocated` -> `Sent` (when used in an approved email)
- `Allocated` -> `Available` (if prospect opts out or bounces; lead freed for reuse)
- Any -> `Expired` (after expiry date)

No lead can be used twice for the same prospect. Enforce by checking Outreach_Log for prior sends.

---

## Tab 3: Outreach_Log

Every email Mark-Lite drafts (and sends, after graduation).

| Column | Type | Description |
|--------|------|-------------|
| Date | date | Date of draft / send |
| Time | time | Time of draft / send |
| Company | text | Prospect (from Companies tab) |
| Email # | number | 1 / 2 / 3 / 4 / Re-engagement / Skip-gap |
| Subject | text | Email subject line |
| Lead Used | text | Lead ID (from Opportunities tab) |
| Draft Status | text | Pending Review / Approved / Edited / Rejected / Sent |
| Review Feedback | text | Andy's feedback (if edited or rejected) |
| Sent Status | text | Sent / Bounced / Delivered (blank if not yet sent) |
| Reply Status | text | None / Warm / Opt-out / Bounce / OOO / Irrelevant |
| Reply Date | date | Date of reply |

Every drafted email creates a row, regardless of whether it's sent. Status columns update as the draft progresses through review and, if approved, sending.

---

## Tab 4: LinkedIn_Tasks

Manual tasks for Andy to action outside of email.

| Column | Type | Description |
|--------|------|-------------|
| Date Flagged | date | When Mark-Lite flagged this |
| Company | text | Prospect |
| Contact Name | text | Who to contact |
| Task Type | text | Connection request / Message / Research |
| Context | text | Why this task matters |
| Priority | text | High / Medium / Low |
| Status | text | Pending / Done / Skipped |
| Notes | text | Andy's notes on outcome |

Mark-Lite can add rows and set Status=Pending. Only Andy changes Status to Done or Skipped.

---

## Tab 5: Daily_Batches

Batch assignments by day.

| Column | Type | Description |
|--------|------|-------------|
| Date | date | Day this batch is for |
| Company | text | Prospect in today's batch |
| Email # | number | Which email is due |
| Drafted | text | Y / N |
| Draft Row Ref | text | Reference to the row in Outreach_Log |
| Status | text | Pending / Drafted / Approved / Sent / Skipped |
| Skip Reason | text | If skipped, why (e.g. "No matching lead available") |

Populated at the start of each run. Updated as drafts progress.

---

## Schema Integrity Rules

1. Never add columns. If information doesn't fit, flag it to Andy in Slack.
2. Never rename columns or tabs.
3. Never change column order.
4. Never delete rows. Status changes reflect what happened; rows persist.
5. If a tracker is read and has columns or tabs that don't match this schema, STOP. Escalate to Slack. Do not write.
6. If a column you expect is empty where it shouldn't be (e.g. a Companies row with no email), flag it in the daily report, do not fill it in from inference.
7. Dates are UK format (DD/MM/YYYY) in the sheet. Parse accordingly.

---

## Updating This Schema

Only Andy updates this file. If Mark-Lite believes the schema needs changing (e.g. a new status that genuinely doesn't fit existing options), propose the change in Slack. Do not edit `tracker-schema.md` autonomously.
