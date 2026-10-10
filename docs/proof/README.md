# WorkBuddy proof

Screenshots taken while building and running Peluang in the WorkBuddy desktop app (v5.7.6). File names start with the date and time (Malaysia time).

| When | What it shows |
|---|---|
| 10 Oct, evening | Building the rulebook from official sources; creating the six experts |
| 11 Oct 00:49 | WorkBuddy re-checks `rules.json` against the source PDFs and adds 11 missing conditions |
| 11 Oct 01:03 | Targeted rulebook fixes (tax-year range, contract date, info-only fields, Budget 2027 marked "future") |
| 11 Oct 01:07 | Matcher expert rewritten to be generic (rules come only from `rules.json`) |
| 11 Oct 01:52 | Diagnosis: the first fast run had one agent doing every step itself, so we changed the coordinator to launch each expert as a real sub-agent |
| 11 Oct 02:29 | **Real multi-agent run:** 8 expert launches (profiler ∥ rule-checker in parallel), checker sends work back to paperwork and re-checks |
| 11 Oct 03:48–04:01 | **Owner replies by email** → paperwork reads the Gmail reply + attachment → matcher updates → checker recalculates in Python and fixes 2 wrong numbers → writer regenerates |
| 11 Oct 04:42–04:51 | **One-sentence request** ("Check what government help my business is missing out on.") → WorkBuddy dispatches the experts (profiler + rule-checker in parallel), sends the email, replies to the owner in plain English |
| 11 Oct 06:18 | The six experts exported from WorkBuddy into `experts/` (byte-identical copies) |
| 11 Oct 06:01–06:21 | **Final one-sentence run** (the one in `demo/sample-output/`): plain-English answer to the owner with the files attached |
