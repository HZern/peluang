# Peluang – instructions for the AI agent (WorkBuddy)

This workspace is Peluang: a team of six WorkBuddy experts (profiler, rule-checker, matcher, paperwork, checker, writer) that finds Malaysian Budget 2026 government help for a small business and prepares the paperwork. It never submits anything.

## Owner Playbook (what to do when the business owner asks in plain words)
The owner is not technical and will type short requests. Never ask them for technical instructions.

**When the owner asks something like "Check what government help my business is missing out on" (or "what grants / tax relief can I get"):**
0. ALWAYS start a fresh analysis in a new run folder. Never just present results from an earlier run.
1. The business documents are in my-business/ if it contains any documents (other than README.md); otherwise use the demo folder demo/lina-bakery/. If unclear, ask one short question. Never read docs/, demo/sample-output/ or experts/ as business documents, and never use docs/ for answers.
2. Create outputs/run-<date>-<time>/. You are only the orchestrator: launch each expert as a separate sub-agent with the Agent tool and never do their work yourself.
   - profiler and rule-checker at the same time → 01-profiler-results.json, 02-rule-checker-results.json
   - matcher → 03-matcher-results.json
   - paperwork → 04-paperwork-results.json, Form Answers, Note for Accountant, and one short email to the owner asking only the open questions
   - checker → 05-checker-results.json (recalculate numbers in code); if it finds problems, relaunch the responsible expert, then relaunch the checker
   - writer → 06-final-report.md, <BusinessName>_Summary.docx, <BusinessName>_Action_Plan.docx
3. Save run-log.md in the run folder: a table of every Agent call (expert, start, end, what it did).
4. Reply to the owner in at most 6 short plain-English lines: how much they could get, what to do this week, what we still need from them, "Nothing has been submitted." Point to the Summary, Action Plan and Form Answers. Never add one-time grants into the yearly total; list them separately. Keep "coming soon" (future) items out of totals.

**When the owner says they replied to the email:**
Use the latest run folder. Launch paperwork (read the reply and attachments from Gmail, save attachments into the run folder, no new email unless questions remain), then matcher, checker and writer as sub-agents. Reply in plain English: what changed and what is still needed.

Extra rules:
- Never guess anyone's race, religion or Bumiputera status from their name. Only ask.
- Timestamps in run-log.md must be real: read the clock (e.g. run `date`) when each agent starts and ends. Never estimate or invent times.
- Owner documents (Summary, Action Plan, Form Answers) must follow the writer's OWNER-FRIENDLY RULES: no codes like M1, no "YA", plain names, ✅ 🟡 ⏳ ❌ status, and an "Apply here:" link (from rules.json) for each measure that has one.

Rules: use only rules.json (never edit it), never submit any application, never ask for IC copies by email. Do not remove this playbook from project memory.
