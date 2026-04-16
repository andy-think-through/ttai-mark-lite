# Tracker Write Process

> Read this file at the start of every run alongside tracker-schema.md.
> Last updated: 2026-04-16

## The Problem

The Routine has a Google Drive connector (read-only) but NO Google Sheets connector. This means:

- **You CAN read** both trackers via their Google Drive file IDs (see context.md for IDs)
- **You CANNOT write** to the trackers directly

The trackers are .xlsx files that sync to Google Drive via the desktop app on Andy's Mac. A separate Cowork process handles the writes.

## How to Handle Tracker Updates

### Step 1: Track What Needs Updating (During Your Run)

As you work through the daily loop, keep a running list of every tracker change you would normally make:
- Companies tab: status changes, email dates, LI dates, notes
- Opportunities tab: lead allocation, status changes
- Outreach_Log tab: new draft rows
- LinkedIn_Tasks tab: new task rows
- Daily_Batches tab: batch assignments, draft status

### Step 2: Commit Pending Updates to the Repo (End of Run)

At the end of each run, create or overwrite the file `pending-tracker-updates.md` in the repo root with ALL pending changes in this exact format:

```
# Pending Tracker Updates
## Date: [YYYY-MM-DD]
## Run: [scheduled / manual / follow-up]

### Northants Tracker

#### Companies
| Row (Company Name) | Column | Old Value | New Value |
|---|---|---|---|
| Hewlett & Sons | Email Status | In Sequence | Parked |
| Hewlett & Sons | Last Email # Drafted | 3 | 4 |

#### Opportunities
| Row (Project Name) | Column | Old Value | New Value |
|---|---|---|---|
| Billing Aquadrome | Status | Available | Allocated |
| Billing Aquadrome | Used In Email To | | Hewlett & Sons |

#### Outreach_Log (New Rows)
| Date Drafted | Company Name | Contact Name | Email Address | Email # | Subject Line Used | Projects Included | Status |
|---|---|---|---|---|---|---|---|
| 2026-04-17 | Hewlett & Sons | John Hewlett | info@hewlettandsons.co.uk | 4 | Still finding work near you | Billing Aquadrome | Pending Review |

#### LinkedIn_Tasks (New Rows)
[same pattern]

#### Daily_Batches
[same pattern]

### Warwickshire Tracker
[same structure as above, or "No changes" if none]
```

### Step 3: Report in Slack

In your daily Slack report, add a line:
```
Tracker updates: [X] changes staged in pending-tracker-updates.md (awaiting Cowork apply)
```

### Step 4: Cowork Applies the Updates

A separate Cowork session (triggered by Andy or scheduled) will:
1. Read `pending-tracker-updates.md` from the repo
2. Open the local .xlsx files
3. Apply all changes
4. Save (Google Drive desktop app syncs automatically)
5. Delete or clear `pending-tracker-updates.md`

### Important Rules

- **Always include Old Value.** This lets the Cowork process verify it's changing the right cell.
- **One file per run.** Overwrite the previous pending-tracker-updates.md each run. If changes from a prior run haven't been applied yet, they'll be visible in the tracker (the Cowork process didn't run) -- flag this in Slack: "Prior pending updates not yet applied."
- **Never skip the staging step.** Even if there are zero updates, commit the file with "No changes this run" so there's an audit trail.
- **Read the tracker fresh each run.** Don't assume your pending updates were applied. Always check the actual tracker state.

## Connectors Available to You

| Connector | Can Do | Cannot Do |
|---|---|---|
| Gmail | Read replies, send emails (after approval) | -- |
| Google Drive | Read tracker .xlsx files by file ID, search files | Write/update files |
| Slack | Post messages, read messages | -- |
| GitHub (repo) | Read files, commit files | -- |

There is no Google Sheets connector. Do not attempt to use one.
