# Mark-Lite Decision Log

> Append-only reasoning audit trail. Newest entries at the top.

---

## 2026-04-17 Follow-Up Run (Andy's 4-item reply)

### Context

Follow-up run responding to Andy's replies to the 4 action items from the morning scheduled run. This is the first interaction loop between Andy and Mark-Lite on the Routine platform.

### Exploitation (80%)
- Drafts posted: 3 (re-engagement emails for A Valley Plant, M Carty Brickwork, Kimben Construction)
- Drafts approved / sent: 0 (awaiting Andy's review)
- Drafts edited: 0
- Drafts rejected: 0
- Replies processed: none new this run
- Tracker updates: 5 changes staged in pending-tracker-updates.md (JDW -> Client, 3 lead allocations, 3 outreach log rows)
- Pipeline status: JDW moved to Client (Andy's confirmation). SRK status recommendation pending Andy's response.

### Exploration (20%)
- Analysis done: none (follow-up run, not scheduled)
- Experiments proposed: none
- Cross-domain signals: none new

### Decisions Made

- **SRK Groundworks: recommended Parked, not Warm.** Andy asked whether SRK (replied ~7 weeks ago, no engagement since) should be treated as warm. Recommended Parked with note about prior reply. Reasoning: "Warm" should mean active/recent interest, not historical. A 7-week-old reply with no follow-up has gone cold. Any future re-engagement email stays permanently in Andy's review queue per the warm-reply rule. Awaiting Andy's confirmation.

- **Re-engagement emails drafted without template.** Andy confirmed no re-engagement template exists and instructed me to draft myself. Drafted 3 emails following the established voice (language rules, package language, no em-dashes, 4-5 sentences). Each includes a fresh lead not previously sent to that prospect. These remain permanently drafts-only per the rules. If Andy approves these, the approach could become the basis for a formal re-engagement template.

- **JDW Brickwork set to Client.** Andy confirmed Josh Warren signed to Mark, met Tuesday, building Mark next week. Staged the update. Noted that the Wiki report from 16/04 had signals (JDW revenue moved to invoiced, build week mentioned) but didn't explicitly flag the status change for Mark-Lite. Proposed an ML-UPDATE prefix convention in Slack to prevent this gap recurring.

- **Prior pending updates not found.** The morning scheduled run reported staging 14 changes in pending-tracker-updates.md, but no such file was found in the repo. Either the earlier session didn't commit successfully or committed to a different branch. Flagged in the pending updates file. May need reconstruction.

### Questions for Andy
- SRK Groundworks: Parked or keep at a different status? (posted in Slack)
- ML-UPDATE convention for prospect status changes: Option A (Slack prefix) or Option B (wiki repo access)? (posted in Slack)
- Prior pending updates from morning run: were the 14 changes applied or lost?

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
