# legacy-b-maintenance-cobol

Demo legacy system for [REPLIC8](https://github.com/jaiom-rola-sp/REPLIC8): the old maintenance software of "Subsidiary B", an oilfield services company. Written in COBOL (GnuCOBOL, fixed format). All data is made up.

- `src/MAINT.cbl`: the program. `data/requests.dat`: fixed-width data.
- Read-only operations: `GET-REQUEST`, `LIST-OPEN-REQUESTS`.
- Line protocol: the first stdin line is the command, then `KEY=VALUE` lines, then `END`. Output is `KEY=VALUE` lines; `BEGIN-ITEMS` starts a list and `--` closes each item.
- Shared keys with the inventory system: part ID (for example `PMP-2210`) and site region (for example `PERMIAN`).

## Self-heal rehearsal

Rename the paragraph `GET-REQUEST` (and its `WHEN "GET-REQUEST"` line) to `FETCH-REQUEST`. The old wrapper then fails its contract test, which is what REPLIC8's repair is meant to fix.
