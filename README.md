### SQL + Gemini Workflow (with Schedule) — Submission Notes

**Goal**: Filter a tiny job list for titles containing "Engineer" using Google Gemini, then output a clean table of `jobTitle` and `company`. A simple schedule is included so it can run automatically.

**Files to submit**:  
- Exported workflow JSON: `n8n-job-sql-gemini-node.json`  
- One screenshot: `Set Output` node showing a successful run (2 rows)  
- This README (2–6 sentences per requirement)

**Inputs**:  
- Manual Trigger (for testing) and Schedule Trigger (for automatic runs).  
- SQL node returns 3 sample rows via UNION SELECT; no tables required.  
- Gemini node uses your existing “Google Gemini(PaLM) Api account” credential.

**Processing/Decision**:  
- Build Prompt embeds the SQL rows into one prompt.  
- Google Gemini returns only jobs matching “Engineer”.  
- Code in JavaScript parses Gemini’s text into items.  
- Set Output keeps only `jobTitle` and `company` for a simple result.

**Outputs**:  
- Final node (`Set Output`) lists the filtered jobs as a table with two columns.

**Schedule**:  
- Add rule in `Schedule Trigger` (e.g., Every 60 minutes, or daily 09:00).  
- Wire `Schedule Trigger` → `SQL: Sample Jobs` (keep Manual Trigger for tests).  
- Turn workflow Active for the schedule to run.

**How I tested**:  
1. Executed via Manual Trigger.  
2. Verified `SQL: Sample Jobs` → `Build Prompt` → `Google Gemini` outputs text.  
3. Confirmed `Code in JavaScript` shows items with `jobTitle` and `company`.  
4. `Set Output` displays two rows (“Software Engineer”, “QA Engineer”); took the screenshot.


