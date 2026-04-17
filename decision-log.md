# Mark-Lite Decision Log

> Append-only reasoning audit trail. Newest entries at the top.

---

## 2026-04-17 Daily Run (First Routine Run)

### Exploitation (80%)
- Drafts posted: 0 new (4 Email 4 drafts carried forward from 16/04, approved by Andy)
- Gmail drafts created: 4 (Hewlett, MBH, NR Groundworks, Brennan -- all Email 4, Northants Groundworks)
- Drafts approved / sent: 4 approved by Andy on 16/04 / 0 sent (no gmail_send_draft tool available; drafts in Gmail for Andy to send)
- Drafts edited: 0
- Drafts rejected: 0
- Replies processed: none new (checked Gmail -- only a Railway promotional email)
- Tracker updates: 14 changes staged in pending-tracker-updates.md (8 Northants Companies updates, 4 Outreach_Log rows, 2 Warwickshire Companies status changes)
- Pipeline status: Northants 34 in sequence + 2 warm + 3 not started = 39 total. Warwickshire 22 in sequence + 2 replied/warm + 2 opted out = 26 total. Combined active: 58.

### Exploration (20%)
- Analysis done: Read Wiki's last 3 reports. Key signal: April 17-28 critical convergence window (7 decisions in 11 days). Revenue de-concentration happening organically. CE leads confirmed as same structural problem as supply-chain trades.
- Experiments proposed: None this run. Focused on first-run setup and clearing backlog.
- Cross-domain signals: Wiki confirmed Tippercrete CI sample at ~96hrs with no reply. Fred paused, Andy fixing.

### Decisions Made
- **Created Gmail drafts instead of sending directly:** No gmail_send_draft tool available in my connector set. Created 4 drafts in Gmail for Andy to send manually. This is actually consistent with drafts-only mode -- Andy gets a final check in Gmail before hitting send.
- **Skipped today's Thursday batch (Northants):** All 8 prospects are supply-chain trades (5 Electrical at #4, 1 Roofing at #2, 2 Drainage at #1). Per principles, planning data doesn't serve these trades. No leads to match, no drafts to create.
- **Flagged missing re-engagement template:** Andy requested re-engagement emails for Warwickshire completers (A Valley Plant, M Carty, Kimben). No re-engagement template file exists in templates/. Cannot draft without template per prompt rules. Escalated.
- **CE skip confirmed:** Andy said "CE skip for now, we need a better strategy." Prestige, L4, MMK remain stuck at Email 1-2 in Northants.
- **Staged Tippercrete -> Warm:** Prior run identified this but pending updates were never committed. Staging now.
- **Staged J&M Groundworks -> Warm:** Tracker shows "Replied" (not a valid schema status) but notes say "Warm lead." Normalised to Warm.
- **Flagged 973 blank rows in Warwickshire tracker:** Andy instructed deletion. Staged for Cowork process.

### Questions for Andy
1. SRK Groundworks status -- "Replied" with no notes. Warm or something else?
2. JDW Brickwork status -- call scheduled with Josh Warren. In Conversation or Client?
3. Re-engagement template -- please add to templates/ so I can draft for A Valley Plant, M Carty, Kimben.
4. Gmail send capability -- I can create drafts but not send. Is there a gmail_send_draft connector to enable, or do you prefer to send manually?

---

## 2026-04-16 Migration to Routines (Drafts-Only Launch)

### Context

Mark-Lite migrated from Cowork scheduled task to Claude Code Routine. Launch config:

- Runs on Anthropic cloud (no local machine dependency)
- Reports to Slack #ttai-employees (replaces email)
- Uses this repo (`ttai-mark-lite`) as memory
- API trigger enables two-way interaction via Slack bridge bot
- Launching in DRAFTS-ONLY MODE for first two weeks

### Why Drafts-Only for Launch

On review of the first draft of the Mark-Lite prompt, Andy flagged that the original "first run drafts, second run sends" model was too aggressive. Mark-Lite is talking to real prospects with money; the cost of an ill-timed or off-tone email is real (Danny Fordham is actively deciding whether to buy).

The launch model is therefore:

- 14 days minimum in drafts-only mode
- 20 drafts reviewed by Andy
- 90% approval rate without edits
- Explicit graduation command (`GRADUATE MARK-LITE TO SEND MODE`) required to switch to direct-send

Even after graduation, some categories stay drafts-only permanently:
- Emails to prospects Andy has personally spoken to
- Re-engagement emails
- Copy adapted beyond template variable substitution
- Emails to prospects with prior warm replies

### Why Experiments Are Permanently Approval-Gated

The original draft gave Mark-Lite autonomy to "run experiments on live outreach." Andy flagged that this is too much autonomy on live prospects, even after trust is built. A bad experiment tanks reply rates and potentially burns a prospect.

New rule: Mark-Lite proposes experiments in Slack. Andy approves. Mark-Lite runs only after approval. This does not relax after graduation.

### Kill Switch Added

`PAUSE MARK-LITE` (exact text in Slack) halts everything. `RESUME MARK-LITE` unpauses. This is the emergency stop for when something goes wrong.

### Removal Floor Added

"Removal as valuable as addition" stands, but with a floor: 10 prospects minimum, 21 days minimum, clear zero-response pattern required before parking a segment. Prevents reactive pruning on noise.

### Mode 2 Classification Added

The original draft treated every Slack message as an instruction. New rule: classify each message as acknowledgement / command / question / instruction / draft feedback / ambiguous, and act accordingly. Ambiguous goes to "ask before acting."

### Tracker Schema Locked

`tracker-schema.md` added to the repo as the canonical schema. Mark-Lite cannot add columns, rename tabs, or restructure. Schema mismatch = stop and escalate.

### Prior Cowork Version

The predecessor skill ran on Cowork, wrote decision log and reports to local filesystem, sent reports via Gmail. Sent outreach directly from day one. See `andy-think-through/ttai-wiki` -> `operations/mark-lite-employee-SKILL.md` for historical record. That version is deprecated as of this migration.
