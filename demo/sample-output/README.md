# Sample output: Lina's Bakery (fictional demo business)

**This folder:** a complete run from one sentence typed by the owner: *"Check what government help my business is missing out on."* (11 Oct 2026, 06:01–06:21, six WorkBuddy experts.)

| File | For | What it is |
|---|---|---|
| `Linas_Bakery_Summary.docx` | Owner | One-page results with ✅/🟡/⏳/❌ and apply links |
| `Linas_Bakery_Action_Plan.docx` | Owner | This week's actions and the questions we still need answered |
| `Form_Answers.md` | Owner | Copy-ready answers and documents for each application, plus "Apply here" link |
| `Note_for_Accountant.md` | Accountant | Tax reliefs to claim with figures and workings |
| `Email_to_Owner.txt` | Owner | The email Peluang sent: only the open questions |
| `run-log.md` | Reviewer | Every expert launch with real start/end times (profiler and rule-checker in parallel) |
| `01`–`05-*.json` | Reviewer | Each expert's result file |
| `checker.py` | Reviewer | The code the Checker wrote to recalculate every figure |
| `06-final-report.md` | Reviewer | Full technical report |

**`after-owner-reply/`:** an earlier run after Lina replied to the email ("we never had a digital grant") and attached a September bank statement. Peluang read the reply from Gmail (`04a-owner-answers.json`), moved the digital grant to the full RM4,000, and the Checker recalculated everything and fixed two wrong figures (see `05-checker-results.json`).
