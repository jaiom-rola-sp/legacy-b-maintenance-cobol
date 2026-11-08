# legacy-b-maintenance-cobol

Demo legacy system for [REPLIC8](https://github.com/jaiom-rola-sp/REPLIC8): the old maintenance software of "Subsidiary B", an oilfield services company. Written in COBOL (GnuCOBOL, fixed format). All data is made up.

- `src/MAINT.cbl`: the program. `data/`: fixed-width data (`requests.dat`, `wells.dat`, `techs.dat`, `history.dat`).
- 9 read-only operations: `GET-REQUEST`, `LIST-OPEN-REQUESTS`, `LIST-SITE-REQUESTS`, `GET-WELL`, `GET-SERVICE-HISTORY`, `GET-TECHNICIAN`, `FIND-AVAILABLE-TECHS`, `CALC-DOWNTIME-COST` (barrels/day x $88 x days), `GET-WELL-RISK` (score 0 to 100, LOW to CRITICAL).
- Written to look like code many people changed over 20 years: a change log, release 2 commands behind a second dispatcher with `GO TO`, `PERFORM ... THRU` exit paragraphs, 88-level flags, commented-out formulas, unused fields and a dead report paragraph. The original two operations give exactly the same answers as before.
- Demo story: `GET-WELL-RISK WELL-ID=W-44` is CRITICAL (80); `CALC-DOWNTIME-COST WELL-ID=W-44 DAYS=7` is $443,520.00; `FIND-AVAILABLE-TECHS SITE=PERMIAN SKILL=ELECTRICAL` returns Maria Alvarez (T-101).
- Line protocol: the first stdin line is the command, then `KEY=VALUE` lines, then `END`. Output is `KEY=VALUE` lines; `BEGIN-ITEMS` starts a list and `--` closes each item.
- Shared keys with the inventory system: part ID (for example `PMP-2210`) and site region (for example `PERMIAN`).

## Self-heal rehearsal

Rename the paragraph `GET-REQUEST` (and its `WHEN "GET-REQUEST"` line) to `FETCH-REQUEST`. The old wrapper then fails its contract test, which is what REPLIC8's repair is meant to fix.
