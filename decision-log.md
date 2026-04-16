# Mark-Lite Decision Log

> Append-only reasoning audit trail. Newest entries at the top.

---

## 2026-04-16 First Run (Routines, Drafts-Only)

### Exploitation (80%)
- Drafts posted: 0 (blocked -- no templates in repo)
- Drafts approved / sent: 0
- Drafts edited: 0
- Drafts rejected: 0
- Replies processed: none new since 13 Apr (Danny Fordham warm reply already handled by Andy)
- Tracker updates: none (blocked -- schema mismatch and xlsx format)
- Pipeline status: ~24+ total across both regions (estimate from Drive content snippets), 1 warm (Andy handling), 1 opted out, ~12 in re-engagement monitoring window (ends 18-19 Apr)

### Exploration (20%)
- Analysis done: Full connector audit, tracker format assessment, Gmail review of re-engagement batch status
- Experiments proposed: none (first run, focused on infrastructure readiness)
- Cross-domain signals: Read Wiki's Slack reports from today. Key items:
  - Wiki confirmed Tippercrete (Danny Fordham) very warm, replied twice within 19 min, CI sample delivered 14 Apr
  - JDW Brickwork converted (invoice TTAI-004, GBP 500) -- direction-of-initiation hypothesis: cold -> CI tier, inbound -> managed Mark
  - Revenue position stronger than wiki showed (GBP 3,188.20 invoiced vs GBP 938.20 previously displayed)
  - Wiki flagged Apr 18-28 as convergence window (re-engagement results, Tippercrete response, JDW build, AccXel discovery)
  - Fred last reported 13 Apr, may be stalled during NBA playoffs

### Decisions Made
- **Stopped at tracker read, did not write**: Live trackers are .xlsx on Drive with different column structure than tracker-schema.md. Per rules: schema mismatch = stop and escalate. Correct decision -- writing to a mismatched schema risks data corruption.
- **Did not draft emails**: Templates directory missing from repo. Per rules: missing template = do not improvise. Escalated to Slack.
- **Did not send any emails**: Drafts-only mode. No drafts to send.
- **Classified Gmail inbox**: Only Mark-Lite-relevant reply was Danny Fordham (13 Apr, already handled by Andy). Re-engagement batch (12 firms, 13 Apr) has zero replies at day 3 -- still within monitoring window.

### Questions for Andy
1. Convert trackers from .xlsx to native Google Sheets? Or provide alternative access method?
2. Is tracker-schema.md the target schema (to be migrated to), or should it be updated to match existing tracker structure?
3. Add email templates to templates/ in the repo
4. Create reports/ and campaigns/ directories (or confirm I should create them)

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
