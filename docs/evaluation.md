# Evaluation: Peluang on Lina's Bakery (demo business)

**How we measured:** before running any agent, we wrote down the correct answer for every measure by hand from the official sources (BSN FAQ/terms, LHDN rates, Budget 2026/2027 documents). These "golden answers" were kept **outside** the agents' workspace so the agents could never see them. Each run's output was then compared line by line.

The demo business has **six planted traps** a careful advisor should catch:

| # | Trap | What a good agent should do |
|---|---|---|
| 1 | Owner wrote "something during COVID?" about past grants | Ask: a previous **digital** grant would block most of the RM4,000 grant (except e-invoicing) |
| 2 | Only one month of bank statements | Not a blocker: BSN accepts audited accounts **or** management accounts **or** 2 months of statements |
| 3 | Quote doesn't say the supplier is a government-appointed provider | Tell the owner to confirm before applying |
| 4 | No IC copies in the folder | List as "owner provides at submission"; never request ID by email |
| 5 | Profit ≠ taxable income | Label the tax figure a rough estimate, "confirm with your accountant" |
| 6 | A hawker grant that sounds relevant | Mark not eligible (a Sdn Bhd shop is not a street vendor) |

## Results per measure

Two runs are scored:
- **Run A, the final one-sentence run** (11 Oct, 06:01–06:21, default model): the owner typed only *"Check what government help my business is missing out on."* Output is in [`demo/sample-output/`](../demo/sample-output/).
- **Run B, after the owner's email reply** (11 Oct, 02:00 run + 03:16 follow-up): shows the answers changing once Lina replied. Output is in [`demo/sample-output/after-owner-reply/`](../demo/sample-output/after-owner-reply/).

| Measure | Hand-checked answer | Run A (before reply) | Run B (after reply) |
|---|---|---|---|
| Digital grant (Geran Digital PMKS MADANI) | Needs something → ready after reply; RM4,000 (RM1,200 if a previous digital grant) | 🟡 Needs one thing: asks about a previous grant; RM4,000, or RM1,200 if yes ✅ | Full **RM4,000**; only open step: confirm the supplier is an appointed provider ✅ |
| Hawker grant (Geran Digital Penjaja MADANI) | Not eligible | ❌ Not eligible (street vendors only) ✅ | Not eligible ✅ |
| SME income tax rates | Automatic; ≈ RM8,415 less tax | ✅ RM14,025 vs RM22,440 → RM8,415 ✅ | RM8,415 (after checker fix) ✅ |
| E-invoicing deduction | Automatic (unconfirmed) | ✅ ≈ RM360 on the RM2,400 module; paid invoice needed ✅ | ≈ RM360, unconfirmed ✅ |
| Stamp duty exemption | Only **new** contracts from 1 Jan 2026 (the 2 planned hires) | ✅ RM20: the 2 new hires only ✅ | "6–8 contracts, depends on dates" ⚠️ |
| GGSM4 financing guarantee | Optional (unconfirmed): halal status unknown | 🟡 Needs info: asks about halal / Bumiputera status (asks, never guesses) ⚠️ label differs, reasoning right | Same ⚠️ |
| Budget 2027 tax cut | Coming soon, not counted | ⏳ Coming soon, excluded from totals ✅ | ✅ |
| Budget 2027 minimum wage | Coming soon (MSME exempt) | Exempt, excluded from totals ✅ | ✅ |

**Run A: 7 of 8 exactly right, 1 partly right (label only), 0 wrong.** Run B: 6 exact, 2 partly right, 0 wrong.

| Planted trap | Caught? |
|---|---|
| 1 Previous grant | ✅ Asked by email; after Lina replied "never had a digital grant", the grant moved to the full RM4,000 |
| 2 One bank statement | ✅ Not treated as a blocker |
| 3 Appointed provider | ✅ Flagged: confirm before applying |
| 4 IC copies | ✅ "Provide when applying, do not email" |
| 5 Tax estimate | ✅ "Estimate, confirm with your accountant" |
| 6 Hawker grant | ✅ Not eligible, with reason |

## Self-validation: mistakes the Checker caught on its own

The Checker expert recalculates every figure **in code** and sends errors back to the expert responsible:

| What was wrong | Found by | Fixed to |
|---|---|---|
| Tax saving written as RM8,375 | Checker (Python: 0.24×93,500 − 0.15×93,500) | **RM8,415** |
| Guarantee fee RM270 a year (0.75% × RM36,000) | Checker, reading the rulebook ("0.75% p.a., **minimum RM500**") | **RM500** |
| Yearly total mixed in 2027 "future" savings | Checker (future items must not be counted) | Immediate total separated from "coming soon" |
| Unconfirmed measure presented as definite | Checker | "Unconfirmed – verify with LHDN/accountant" added |
| Quote expiring in 7 days not prioritised | Checker | Digital grant moved to priority #1 |
| Matcher counted 3 staff earning ≤ RM3,000; payroll shows 6 (Run A) | Checker, recounting the payroll in code | Corrected to 6 (savings figure unaffected: only new contracts count) |

## Time and cost (WorkBuddy credits)

| Run | Setup | Time | Credits |
|---|---|---|---|
| 1 | Single agent doing all steps, long outputs | ~24 min | ~119 |
| 2 | Real multi-agent run: 8 expert launches incl. checker fix loop | ~27 min | ~197 |
| 3 | Owner's email reply processed (paperwork → matcher → checker → fix → writer) | ~41 min | ~180 |
| 4 | One-sentence request on a free model (Hy3) | ~9 min | 0 |
| 5 | **Final one-sentence request** (Run A, default model): 6 experts, real timestamps in run-log.md | **~20 min** | see proof |

A consultant or the owner doing this by hand would need to read ~10 official documents in two languages, check 30+ conditions and prepare the paperwork, typically hours to days. Peluang does it unattended in under half an hour.

## Known issues / next steps

- **Stamp duty:** fixed in Run A (only new contracts counted) after the profiler was told never to drop dates; Run B still shows the older behaviour.
- **Free model (Hy3):** follows the one-sentence playbook and launches experts, but is less strict (made-up log times, ignores formatting rules). Use the default (Auto) model for real use.
- **Grant windows:** first-come-first-served grants can close mid-year; a scheduled weekly rulebook re-check is the natural next step.
