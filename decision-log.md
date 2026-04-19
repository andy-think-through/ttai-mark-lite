# Mark-Lite Decision Log

> Append-only reasoning audit trail. Newest entries at the top.

---

## 2026-04-19 Daily Run (Saturday)

### Exploitation (80%)
- Drafts posted: 0 (Saturday, no batch day)
- Drafts approved / sent: 0
- Drafts edited: 0
- Drafts rejected: 0
- Replies processed: none (checked Gmail for all 7 prospects emailed on 17/04 -- zero replies)
- Tracker updates: 12 changes staged in pending-tracker-updates.md (includes recovered updates from lost 2026-04-17 run)
- Pipeline status: 7 in active monitoring (4 Email 4 + 3 re-engagement, all sent 17/04), 2 warm (Tippercrete, J&M), 1 warm-lapsed (SRK, pending Andy decision), 1 client (JDW), 1 warm needing research (R8)

### Exploration (20%)
- Analysis done: Reviewed pipeline response patterns. All 7 emails sent 17/04 are within 48-hour response window (still early). Tippercrete CI sample now at 5 days with no reply -- trending cold.
- Experiments proposed: none
- Cross-domain signals: Wiki's April 16 report noted "April 17-28 critical convergence window" with 7 decision points. Re-engagement batch results (expected 18-19 Apr) are now in window. No actionable signal change for today.

### Decisions Made
- Recovered lost pending-tracker-updates.md from April 17 ephemeral branch. Reconstructed all 12 updates from Slack messages and Gmail evidence. Committed to main this time.
- J&M Groundworks status "Replied" -> "Warm": they asked for Andy's details to arrange a call on 04/03. That is unambiguously warm. "Replied" is not a valid schema status. Correcting.
- Tippercrete status "In Sequence" -> "Warm": Danny Fordham replied warm ~13/04. CI sample sent 14/04. Even though CI sample got no reply, the warm reply stands. Status update had been staged on 16/04 but never applied.
- SRK Groundworks: NOT changing status. "Replied" is invalid but needs Andy's explicit decision on whether to Park. Re-raising in Slack.
- JDW -> Client: Andy-directed ("he's signed up to mark"). Staging per Andy's instruction.
- Saturday run: no new outreach. Saturday is not a batch day. Monitoring only.

### Questions for Andy
- SRK Groundworks: "Replied" is not a valid schema status. Recommend Parked (replied ~7 weeks ago, zero engagement since). Awaiting your decision.
- Tippercrete CI sample: 5 days with no reply. Do you want to follow up personally, or should I note this as lapsed?
- Prior pending tracker updates: Cowork apply process has NOT run since migration. All updates from 16/04, 17/04, and 19/04 are accumulating. Please run the Cowork process or advise on an alternative.

---

## 2026-04-17 Daily Run (recovered -- original committed to ephemeral branch and lost)

Note: This entry is reconstructed from Slack messages and Gmail evidence. The original run committed its decision log entry and pending-tracker-updates.md to a feature branch that was cleaned up. This is the repos-are-employee-memory failure mode in action.

### Exploitation (80%)
- Drafts posted: 7 (4 Northants Groundworks Email 4 + 3 Warwickshire re-engagement)
- Drafts approved / sent: 7 (all approved by Andy at 10:58, drafted in Gmail at 11:02, sent by Andy same day)
- Drafts edited: 0
- Drafts rejected: 0
- Replies processed: none new
- Tracker updates: 14 changes staged (lost to ephemeral branch, recovered in 19/04 run)
- Pipeline status: 4 Groundworks completing sequence (Email 4), 3 site-trade re-engagement sent

### Exploration (20%)
- Analysis done: Proposed ML-UPDATE prefix format for Andy to notify status changes (Andy's response pending)
- Experiments proposed: none
- Cross-domain signals: Wiki's April 16 report noted JDW revenue and build week

### Decisions Made
- SRK Groundworks: Recommended Parked (replied ~7 weeks ago, no engagement since). Andy asked "should this be treated as warm or not?" -- Mark-Lite answered "not warm, recommend Parked." No explicit approval received.
- JDW Brickwork: Andy confirmed "he's signed up to mark" -- staged as Client
- Re-engagement emails: Drafted by Mark-Lite (no template existed -- Andy instructed "please draft yourself"). All 3 approved and sent.
- CE firms: Andy instructed "skip for now, we need a better strategy"

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
