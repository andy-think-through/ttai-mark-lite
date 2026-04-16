# Mark-Lite Decision Log

> Append-only reasoning audit trail. Newest entries at the top.

---

## 2026-04-16 Daily Run (third run, Routine platform)

### Exploitation (80%)
- Drafts posted: 0 (4 drafts from the earlier run at 13:34 are still awaiting Andy's review)
- Drafts approved / sent: 0
- Drafts edited: 0
- Drafts rejected: 0
- Replies processed: none (no new prospect replies since Danny Fordham on 13 Apr)
- Tracker updates: none (write blocker still active -- no Google Sheets write tools available)
- Pipeline status: unchanged from earlier run today

### Pipeline Snapshot (read-only, from native Google Sheets)

**Warwickshire (26 prospects):**
- 7 Electrical -- all at Email 4, sequence complete (supply-chain trade, no further action per principles)
- 5 HVAC -- 4 at Email 2, 1 opted out (supply-chain trade, no further action)
- 5 Roofing -- all at Email 4, sequence complete (supply-chain trade)
- 4 Groundworks -- 2 Replied (J&M, SRK), 1 at Email 4 complete (A Valley Plant), 1 warm (Tippercrete -- Andy handling, CI sample sent 14 Apr, no reply ~54hrs)
- 2 Brickwork -- both at Email 4, sequence complete (M Carty, Kimben)
- 2 Drainage -- 1 opted out (A-Line), 1 at Email 4 complete (Drains Are Us)
- Site-trade re-engagement candidates: A Valley Plant, M Carty, Kimben (sequences ended 28-36 days ago)

**Northants (39 prospects):**
- 4 Groundworks -- all at Email 3 in tracker (Email 4 drafted today, awaiting approval): Hewlett, MBH, NR Groundworks, Brennan
- 5 Civil Engineering -- 2 stuck at Email 1 (Prestige, L4, no CE leads), 1 at Email 2 (MMK, same blocker), 2 at Email 4 complete (Gladstone, T&C)
- 6 Scaffolding -- 5 at Email 4 complete, 1 warm (R8 Scaffolding -- Andy handling)
- 5 Roofing -- all at Email 2 (supply-chain trade, no further planning-data outreach per principles)
- 7 Electrical -- 5 at Email 4, 1 at Email 3, 1 Not Started (supply-chain trade)
- 4 HVAC -- all at Email 2 (supply-chain trade)
- 3 Brickwork -- 1 warm/client (JDW), 1 at Email 4 complete, 1 Not Started
- 5 Drainage -- various stages (supply-chain trade)

**Total active pipeline:** 65 prospects
- Active site-trade prospects requiring action: 4 (Groundworks Email 4, awaiting approval)
- Warm/In Conversation: 3 (Tippercrete, R8 Scaffolding, JDW -- all Andy handling)
- Site-trade completers eligible for re-engagement: ~8 (needs Andy input)
- Supply-chain completers: ~30+ (no further action per principles)
- CE firms blocked on lead supply: 3

### Exploration (20%)
- Analysis done: Tracker schema verification
- Experiments proposed: none
- Cross-domain signals: Read Wiki reports from today. Key signal -- Wiki notes April 18-28 is a "critical convergence window" with 6 decision points in 10 days. Mark-Lite's re-engagement batch results (18-19 Apr) are part of this.

### Decisions Made
- **No new drafts this run:** Earlier run today posted all 4 overdue Groundworks Email 4 drafts. No other prospects are due for new emails today. Roofing, Electrical, HVAC, and Drainage firms in both regions are supply-chain trades and per principles should not receive further planning-data outreach.
- **Tracker schema appears to match:** Reviewed the native Google Sheets trackers (created today by Andy, IDs 1BkZvJRbd5KEbsjVhxcRThMbIpt_skHAzxc6lIDr-1Ag and 1aRDnWj9GsbUWIxuLx84dt_SHFUoSv3zmk-coaaQGxt0). Both Companies tabs match tracker-schema.md column structure exactly. The earlier run's "schema mismatch" flag was likely caused by reading .xlsx content snippets vs the native Sheets format, not by an actual schema difference. However, the write blocker remains: no Google Sheets MCP write tools are available in this connector set. Escalating to Slack for Andy.

### Questions for Andy
- Tracker schema resolved? The native Google Sheets versions appear to match the expected schema. But I have no Google Sheets write tools (only Google Drive read). Is there a Google Sheets connector that needs enabling?
- 4 Groundworks Email 4 drafts from the earlier run are awaiting your review (Hewlett, MBH, NR Groundworks, Brennan).
- Re-engagement: Warwickshire site-trade completers (A Valley Plant, M Carty, Kimben) have been 28-36 days since last email. Want me to draft re-engagement emails for them? (These stay drafts-only permanently.)
- CE lead supply: Prestige, L4, and MMK have been stuck 3-4 weeks. No Civil Engineering leads with named contacts available. Keep holding, or propose a skip-gap check-in?

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
