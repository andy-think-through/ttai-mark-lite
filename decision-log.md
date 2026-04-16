# Mark-Lite Decision Log

> Append-only reasoning audit trail. Newest entries at the top.

---

## 2026-04-16 Daily Run (4th scheduled run -- first to commit)

### Context

This is the first day of Mark-Lite running as a Routine. Four runs triggered today. The first three (12:37, 13:34, 14:16) posted to Slack but did not commit to the repo. This run is the first to persist state.

### Exploitation (80%)
- Drafts posted: 0 this run (4 Northants Groundworks Email 4 drafts posted at 13:33-13:34, still awaiting Andy's review)
- Drafts approved / sent: 0
- Drafts edited: 0
- Drafts rejected: 0
- Replies processed: none new since Danny Fordham (13 Apr). Re-engagement batch (12 firms, sent 13 Apr) at day 3 of 5 -- zero replies.
- Tracker updates: 1 status change staged (Tippercrete: In Sequence -> Warm). 5 items flagged for Andy's input (status normalisation, blank row cleanup, JDW -> Client).
- Pipeline status:
  - Warwickshire: 26 named prospects. 3 warm/replied (J&M, SRK, Tippercrete). 3 sequence completers (A Valley Plant, M Carty, Kimben -- re-engagement candidates). 2 opted out. 18 supply-chain firms at Email 2-4 (no further action per principles).
  - Northants: 39 named prospects. 4 Groundworks due Email 4 (drafted, pending review). 3 CE stuck at Email 1-2 (no leads). 1 warm (R8). 1 client (JDW). 5 Roofing at Email 2. 6 Electrical at Email 3-4. 4 HVAC at Email 2. 5 Drainage at Email 1-3.

### Exploration (20%)
- Analysis done: Full tracker read of both regions. Identified status normalisation issue ("Replied" variants not in canonical schema). Identified ~180 blank rows in Warwickshire tracker.
- Experiments proposed: none this run.
- Cross-domain signals: Read Wiki's 09:34 report. Key insight: April 18-28 convergence window (re-engagement results, Tippercrete response, JDW build, AccXel discovery). Andy's attention is limited. Keeping reports tight. Fred last reported 13 Apr -- not actionable for Mark-Lite.

### Decisions Made
- Staged Tippercrete status change to Warm (Danny replied 13 Apr requesting a sample, Andy sent CI sample 14 Apr -- this is clearly a warm prospect).
- Did NOT draft new emails this run: 4 Email 4 drafts from 13:34 run still pending Andy's review. No new prospects due for emails.
- Did NOT change "Replied" statuses to "Warm" autonomously: flagged for Andy because "Replied" isn't in the schema and I need confirmation on the intended status for each.
- Did NOT set JDW to Client: only Andy can set that status per schema rules.

### Questions for Andy
1. Approve/edit/reject the 4 Groundworks Email 4 drafts (posted 13:33-13:34 in Slack)
2. Status normalisation: "Replied", "Replied - Warm", "Replied -- Warm" should be normalised to schema values. Confirm J&M and SRK should be "Warm"?
3. JDW Brickwork: Should be "Client" (invoice TTAI-004). Please confirm so Cowork can update.
4. Warwickshire re-engagement: Draft for A Valley Plant, M Carty, Kimben? (all 28-36 days post-Email 4)
5. CE lead supply: Prestige, L4, MMK stuck 3-4 weeks. Skip-gap check-in or keep holding?
6. ~180 blank rows in Warwickshire Companies tab -- safe to delete?
7. Tracker write process: Cowork apply process ready to run, or does it still need setup?

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
