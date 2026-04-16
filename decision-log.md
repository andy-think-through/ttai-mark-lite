# Mark-Lite Decision Log

> Append-only reasoning audit trail. Newest entries at the top.

---

## 2026-04-16 Daily Run (First Operational Run)

### Exploitation (80%)
- Drafts posted: 4 (Northants Groundworks Email 4 batch)
- Drafts approved / sent: 0 (awaiting Andy's review)
- Drafts edited: 0
- Drafts rejected: 0
- Replies processed: none new (last warm reply: Danny Fordham, 13 Apr)
- Tracker updates: none (schema mismatch blocker -- read-only mode)
- Pipeline status: ~22 in sequence across both regions, 2 warm (Tippercrete + R8 Scaffolding, both Andy handling), 1 converted (JDW), 1 opted out (Temp Air), 3 CE firms stuck (no leads), 8 in re-engagement monitoring window (ends 18-19 Apr)

### Exploration (20%)
- Analysis done: Reviewed tracker data across both regions. Identified Warwickshire site-trade completers (A Valley Plant, M Carty, Kimben) as potential re-engagement candidates -- sequences ended 28-36 days ago. Did not action; re-engagement is permanently drafts-only and needs Andy's input.
- Experiments proposed: none this run
- Cross-domain signals: Read Wiki reports in Slack. Wiki noted "April 18-28 is a critical convergence window" with 6 decision points. Relevant to Mark-Lite because re-engagement batch results (18-19 Apr) and Tippercrete CI response fall within this window. No change to today's actions.

### Decisions Made
- Drafted Email 4 for 4 Northants Groundworks prospects despite tracker write being blocked. Rationale: drafts-only mode means nothing is sent anyway, and these prospects are 17 days overdue for Email 4. Better to have drafts ready for Andy's review than wait for tracker resolution.
- Selected leads for Email 4 drafts without full outreach log visibility. Flagged in each draft that Andy should verify leads weren't already used in Email 1-3. Rationale: cannot access full outreach log to check prior allocations; transparency about the gap is better than not drafting.
- Did not draft for Civil Engineering firms (Prestige, L4, MMK). Rationale: no CE leads with named contacts available -- same underlying constraint that caused prior skips. Flagged in report.
- Did not propose re-engagement for Warwickshire site-trade completers. Rationale: re-engagement is permanently drafts-only and the decision to re-engage a segment needs Andy's explicit input.

### Questions for Andy
- Tracker schema: the canonical schema in tracker-schema.md (5 tabs: Companies, Opportunities, Outreach_Log, LinkedIn_Tasks, Daily_Batches) does not match the live trackers (which have a different column structure and only 2-3 visible tabs). Should the live trackers be restructured to match the schema, or should tracker-schema.md be updated to document the actual structure?
- Civil Engineering lead supply: Prestige, L4, and MMK have been stuck for 3-4 weeks. Is there an alternative CE lead source, or should these prospects be put on hold?
- Warwickshire re-engagement: A Valley Plant, M Carty, and Kimben completed their sequences 28-36 days ago with no reply. Should I draft re-engagement emails with the Construction Intelligence pitch?
- Tippercrete: CI sample sent 14 Apr, now at ~48hrs with no reply. Andy is handling directly -- just flagging the timeline.

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
