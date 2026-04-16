# Mark-Lite Business Context

> Snapshot of the business context Mark-Lite needs at the start of each run.
> Last updated: 2026-04-16 (by Andy, on repo setup)
>
> IMPORTANT: This file is a starting-point snapshot. For live prospect state,
> always defer to the Google Sheets trackers. Do not treat anything in this
> file as current about individual prospects -- treat it as context on
> the shape of the business only.

---

## What Mark-Lite Is

Mark-Lite is one of TTAI's lead generation products. Andy sells lead output directly to tradespeople, in time-bounded campaigns by region. Warm prospects transition to either:

1. **Construction Intelligence** (GBP 50-100/month) -- weekly data feed, lower trust requirement
2. **Managed Mark** (GBP 200/month) -- full managed outreach on their behalf

Mark-Lite is Andy's direct sell. Managed Mark is the licensed agent version for clients who want hands-off.

---

## What You're Selling

### Construction Intelligence (Primary Pitch)

- Weekly email with 10-20 construction project leads
- Filtered to the prospect's specific trade
- Named decision-maker contacts where available
- Price: GBP 50-100/month
- Positioning: "I find these every week. You decide which ones to go after."

This is the primary product for cold prospects. Matches relationship depth. Lower trust barrier than full managed Mark.

### Managed Mark (Upsell)

- Full managed lead generation AND outreach
- Mark finds projects, identifies contacts, reaches out on client's behalf via their email
- Price: GBP 250-500 setup + GBP 200/month
- Positioning: "You're spending 3 hours a week chasing these up -- want me to handle that too?"

Only pitch this to engaged Construction Intelligence customers after 30+ days. Never pitch cold.

---

## Active Regions

### Warwickshire

- Tracker: "Mark-Lite Warwickshire Outreach Tracker" (Google Sheets)
- Hawks Scaffolding is a Mark client with regional exclusivity. NO scaffolding outreach in Warwickshire.

### Northamptonshire (Northants)

- Tracker: "Mark-Lite Northants Outreach Tracker" (Google Sheets)
- Trade focus: site-based trades (Groundworks, Brickwork, Civil Engineering). Scaffolding in Northants is allowed (outside Hawks' exclusive region) but verify in each run.

For live campaign state (which prospects are active, which are warm, pipeline counts), always read the trackers. This file does not track live state.

---

## Validated Insights From Prior Campaigns

1. Site-based trades reply, supply-chain trades don't (21.1% vs 0% warm reply rate across 65 firms).
2. Construction Intelligence is the right entry-point pitch, not full managed Mark. Lower price, lower trust barrier, easier to demo.
3. Named contacts matter. Target 50%+ of leads with named decision-makers.
4. Small-to-medium lead mix is critical. 70%+ small-to-medium, campaigns stall when dominated by mega-projects.
5. Strict trade matching beats generic matching.

These are the learnings that shape prospect selection and lead matching. They live in `principles.md` in full.

---

## Key Colleagues

- **Wiki** -- Maintains the cross-domain knowledge base. Posts reports to #ttai-employees every other day.
- **Fred** -- Portfolio manager for AutoStrategy betting. Posts daily to #ttai-employees (when operating).

Read the last 3 Wiki reports and last 7 Fred reports (or all since last run, whichever is fewer) at the start of each run. Only reference them in your own report if they change what you would do today.

---

## Named Prospects and People (For Context Only)

The following are people Mark-Lite may encounter references to. Treat this list as context only. Live status (whether a prospect is active, warm, signed, etc.) always comes from the tracker, never from this list.

- **Gareth Hunt** -- FD at KW Bell. TTAI's first consulting client. Not a Mark-Lite prospect. If Mark-Lite finds KW Bell in an outreach list, it has landed there in error -- flag and remove.
- **Mike McSweeney** -- Director of Hawks Scaffolding (existing managed Mark client, Warwickshire exclusive) and Midlands Bat Surveys. Both are existing clients -- do NOT include in outreach.
- **Josh Warren** -- JDW Brickwork. Prospect. Status in tracker.
- **Danny Fordham** -- Tippercrete Concrete. Groundworks, Warwickshire. Prospect. Status in tracker.

If a prospect on this list appears with a status Mark-Lite doesn't expect, trust the tracker, not the list. This list gets stale fast; the tracker doesn't.

---

## Escalation Path

Warm replies, pricing questions, new region proposals, and anything ambiguous go to Slack #ttai-employees with clear prefixes:

- `WARM REPLY --` for warm replies (immediate, separate message)
- `ACTION NEEDED --` for anything else requiring Andy's input

Andy handles all human conversations. Mark-Lite's job is to deliver the opportunity, not to negotiate.

---

## Style Rule

No em-dashes in any customer-facing copy. Andy's rule -- they "scream AI." Use double hyphens as the substitute.

This applies to outreach emails, re-engagement emails, Slack drafts for review, and any prospect-facing communication. It does NOT apply to internal-only content in this repo, though consistency is still preferred.

---

## When This Context Is Wrong

If Mark-Lite notices this file is stale or wrong (e.g. a region is mentioned that's no longer active, a prospect listed here has a status the tracker disagrees with), flag it in the daily Slack report:

```
CONTEXT DRIFT NOTED
- context.md says [X], tracker says [Y]. Suggest updating the file.
```

Do not edit `context.md` autonomously. That's Andy's file.
