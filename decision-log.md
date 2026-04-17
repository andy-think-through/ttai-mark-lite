# Mark-Lite Decision Log

> Append-only reasoning audit trail. Newest entries at the top.

---

## 2026-04-17 Follow-Up Run (Draft Approval + Gmail Drafts)

### Context

Andy posted in #ttai-employees: "mark-lite emails all approved, please draft in my gmail". This covers all 7 drafts posted across the 2026-04-16 and 2026-04-17 runs.

### Exploitation (80%)
- Drafts posted: 0 (this was a follow-up run, not a scheduled run)
- Drafts approved: 7 (all approved by Andy in batch)
- Gmail drafts created: 7
- Replies processed: none this run
- Tracker updates: 7 new Outreach_Log rows (Status = Approved), 4 Northants Companies updates (Last Email # 3->4, Date Email 4 Drafted set)
- Pipeline status: unchanged from prior run

### Emails Drafted in Gmail

**Warwickshire (re-engagement):**
1. Kimben Construction LLP (David Richards, info@kimben.co.uk) -- Bordon Hill Nurseries
2. M Carty Brickwork Ltd (Mitchell Carty, info@coventrybricklayers.co.uk) -- Triumph Trade Park
3. A Valley Plant (John McCarthy, info@avalleyplant.uk) -- 34 Apartments Rugby

**Northants (Email 4):**
4. Hewlett & Sons Groundworks Ltd (John Hewlett, info@hewlettandsons.co.uk) -- Overstone Hall
5. MBH Construction Ltd (Anthony Lally, enquiries@mbh-construction.com) -- Ecton Brook
6. N R Groundworks Ltd (Nigel Roberts, enquiries@nrgroundworks.co.uk) -- 21 Townhouses
7. Brennan Building & Civil Engineering Ltd (Robert Brennan, enquiries@bbandce.co.uk) -- Modular Housing

### Exploration (20%)
- None this run (follow-up only)

### Decisions Made
- Classified Andy's message as "clear instruction" -- batch approval of all 7 pending drafts
- Created Gmail drafts (not sent) per Andy's request -- he'll review and send from Gmail directly
- Staged all tracker updates in pending-tracker-updates.md for Cowork to apply
- Used Slack draft post dates for Outreach_Log Date Drafted (2026-04-17 for all, as the Gmail drafts were created today)

### Questions for Andy
- None

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
